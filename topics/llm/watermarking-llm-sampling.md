# Dal campionamento dei token al watermarking (SynthID-Text)

## 1. Come un LLM sceglie il token successivo

Il modello, per ogni posizione, produce un vettore di **logit**: uno scalare per ogni token del vocabolario, ottenuto proiettando lo stato finale del residual stream (dopo normalizzazione) attraverso la matrice di unembedding `W_U`.

```
logits = final_norm(h_last) @ W_U     # [d_model] @ [d_model, |V|] -> [|V|]
```

I logit non sono probabilità: possono essere negativi e non sommano a 1. Si convertono con la **softmax**:

```
p_i = exp(z_i) / sum_j exp(z_j)
```

Il rapporto tra due probabilità dipende solo dalla **differenza** dei logit, in modo esponenziale:

```
p_a / p_b = exp(z_a - z_b)
```

Per questo un divario di logit anche modesto (es. 9-10) produce un rapporto di probabilità enorme (decine di migliaia): la distribuzione, pur essendo definita su tutto il vocabolario (50k+ token), è spesso concentrata quasi tutta su un solo token (esempio classico: "The capital of Germany is" → "Berlin" con p ≈ 0,9997).

## 2. Il campionamento vero e proprio

`rng.choice(vocab_indices, size=1, p=probs)` è la riga che gira davvero in produzione, una volta per ogni token generato.

**Meccanismo (inverse transform sampling / "roulette pesata")**

1. Si costruiscono le somme cumulate delle probabilità: ogni token possiede un intervallo `[cumulata_precedente, cumulata_i)` dentro il segmento [0,1).
2. Si estrae un numero uniforme `u` in [0,1).
3. Si cerca (ricerca binaria, `searchsorted`, O(log|V|)) in quale intervallo cade `u`: quel token è il risultato.

La probabilità che `u` cada nell'intervallo di un token è, per costruzione, esattamente la lunghezza di quell'intervallo — cioè la sua probabilità softmax. Quando un token domina (es. Berlin al 99,97%), il suo intervallo occupa quasi tutto il segmento: il campionamento stocastico diventa **di fatto indistinguibile da un argmax deterministico**, pur restando formalmente casuale.

## 3. Temperatura

Si divide ogni logit per `T` prima della softmax:

```
p_i = exp(z_i / T) / sum_j exp(z_j / T)
```

Non altera l'ordine dei token, ma riscala tutte le differenze tra i logit: T < 1 le amplifica (concentra la massa sul vincitore), T > 1 le comprime (appiattisce la distribuzione).

**Trucco di stabilità numerica (e di comprensione):** si sottrae il massimo `z_max` da tutti i logit prima di esponenziare — operazione lecita perché la softmax è invariante per traslazione (`softmax(z) = softmax(z + c)` per qualsiasi costante c). Dopo la sottrazione tutti gli esponenti sono ≤ 0: il token massimo ha sempre esponente 0 (quindi termine = 1), tutti gli altri hanno esponente negativo. Questo evita overflow e rende evidenti i due limiti:

- **T → 0⁺**: per il token massimo il termine resta 1; per tutti gli altri, `(z_i - z_max)/T → -∞`, quindi il termine → 0. Risultato: distribuzione one-hot (= argmax). Il decadimento è **esponenziale** in 1/T: con un gap di ~9 e T=0.1 il rapporto è già sotto la precisione di un float64.
- **T → ∞**: ogni `z_i/T → 0`, quindi ogni termine → 1 e la distribuzione tende all'**uniforme** (1/|V|). Il decadimento verso l'uniforme è però solo **polinomiale** (∝ 1/T) — molto più lento del collasso verso l'argmax.

Questa asimmetria (collasso rapido da un lato, appiattimento lento dall'altro) è il motivo per cui in pratica si usano intervalli di T asimmetrici rispetto a 1 (es. 0,3–2), e per cui salire troppo con T fa "degenerare" il testo prima ancora di avvicinarsi all'uniforme vera: la coda enorme di token con probabilità individualmente minuscola, ma numerosissimi, arriva a pesare più del vincitore per pura cardinalità.

L'entropia di Shannon H(T) = -Σ p_i log(p_i) è monotona crescente in T, da 0 (T→0, nessuna incertezza) a log|V| (T→∞, massima incertezza), con quasi tutta la variazione concentrata in una decade centrale attorno a T≈1 — fuori da lì la curva è quasi piatta.

**T = 0** è un caso limite gestito a parte nel codice (si sostituisce con `argmax`), perché la formula dividerebbe per zero.

## 4. Top-k e top-p (nucleus sampling)

Agiscono anch'essi su `probs` prima della `rng.choice`, ma **tagliano** invece di deformare:

- **Top-k**: si tengono i k logit più alti, si azzera il resto, si rinormalizza. Soglia fissa, scollegata da quanto il modello è confidente in quel punto.
- **Top-p**: si ordinano i token per probabilità decrescente e si accumula finché la somma supera p; si tiene solo quel "nucleo". È adattivo: se un token domina al 99,97%, il nucleo con p=0,9 contiene un solo token; su una distribuzione piatta può contenerne centinaia.
- **Min-p** (più recente): si tengono i token con `p_i ≥ p_min * p_max` (soglia relativa al vincitore). Regge meglio delle altre alle temperature alte, perché non dipende dalla massa cumulata (che ad alta T si spalma sulla coda).

**Ordine di applicazione** (es. in `transformers`): temperatura → top-k → top-p. Non è arbitrario: top-p diventa così una rete di sicurezza contro gli eccessi della temperatura alta, non un filtro indipendente.

## 5. Il seed

Il generatore di numeri "casuali" di un computer è in realtà **deterministico**: mantiene uno stato interno, e ogni chiamata applica una formula fissa per produrre il numero successivo e aggiornare lo stato. Il **seed** è il valore da cui parte lo stato.

- Stesso seed → stessa sequenza di numeri uniformi → stessi punti sul segmento → stessi token → stesso testo, bit per bit.
- Seed diverso → sequenza scorrelata, nessuna relazione con la precedente.

Fissare il seed **non rende il modello deterministico nella distribuzione** e non la modifica: fissa solo quale estrazione viene fatta da una distribuzione che resta la stessa, con la stessa incertezza. È diverso da T=0, che invece collassa la distribuzione stessa su un solo punto (lì i "dadi" spariscono davvero; con il seed restano, ma si conosce in anticipo come cadranno).

Serve per riproducibilità (esperimenti, debug, demo): senza seed fisso, ogni esecuzione parte da un punto diverso (tipicamente l'orologio di sistema) e dà output diverso.

## 6. Watermarking — idea di base (schema "seed-based")

Idea: invece di un seed fisso, calcolare un seed **diverso per ogni posizione**, derivato da una chiave segreta e dal contesto precedente:

```
seed_t = hash(chiave_segreta, token_(t-H), ..., token_(t-1))
```

Il seed determina dove cade il punto sul segmento in quella posizione → determina il token estratto. Chi possiede la chiave può ricalcolare i seed su un testo esistente e verificare se i token effettivamente presenti sono statisticamente allineati con ciò che quella chiave avrebbe prodotto: su un testo lungo, l'allineamento casuale con una sequenza determinata da una chiave ignota ha probabilità che crolla esponenzialmente.

Proprietà chiave:
- **invisibile**: si sceglie sempre tra alternative che il modello considerava comunque plausibili;
- **verificabile solo con la chiave**: senza il segreto, la sequenza di seed è indistinguibile da rumore;
- **fragile alle modifiche**: cambiare un token altera i seed delle H posizioni successive (quelle il cui contesto lo include), rompendo il watermark da lì in poi.

**Limite pratico di questo schema**: per verificare, il rilevatore dovrebbe sapere "quale token quel seed avrebbe prodotto" — ma questo richiede di conoscere la distribuzione `p` del modello in quel punto, cioè rifare i forward pass. In un contesto di verifica reale (solo testo, nessun accesso al modello) questo non è praticabile.

## 7. SynthID-Text — tournament sampling

**Dathathri, S., See, A., Ghaisas, S., Huang, P.-S., McAdam, R., Welbl, J., et al. (2024).** *Scalable Watermarking for Identifying Large Language Model Outputs*. Nature 634 — https://www.nature.com/articles/s41586-024-08025-4 (Google DeepMind)

Per rendere la verifica possibile guardando **solo il token presente nel testo**, serve una funzione che dipenda dal token e dal seed, non dalla distribuzione del modello:

```
g_m(x, r) = hash(r, m, x) mod 2      # bit 0/1
```

- `r` = seed della posizione = `hash(chiave, contesto_precedente)` — uguale per tutti i candidati di quella posizione.
- `x` = il token da valutare (un candidato in fase di generazione, il token presente in fase di verifica).
- `m` = indice della funzione/turno ("layer"): serve solo a rendere `g_1, g_2, ..., g_M` **hash indipendenti** tra loro pur partendo dallo stesso `r`. Non ha nulla a che fare con i layer del transformer.

**M** (numero di funzioni g / turni) è un iperparametro scelto da chi implementa il sistema, fisso e identico tra generazione e verifica. Più M → più segnale rilevabile con testi più corti, ma maggiore scostamento dalla distribuzione originale del modello (meno "non distorsivo").

### Generazione — passo per passo

1. Il modello produce la distribuzione `p` normale (**non toccata**).
2. Si campionano `2^M` candidati da `p`, con reinserimento (campionamento ordinario, ripetuto più volte).
3. Si calcola il seed `r` della posizione da chiave + contesto.
4. Si calcolano le M funzioni g sui candidati.
5. **Torneo a eliminazione diretta**: turno 1 usa g_1 e accoppia i candidati a due a due (vince chi ha g=1, pareggio 1-1 o 0-0 risolto a caso), turno 2 usa g_2 sui sopravvissuti, e così via fino a un solo vincitore.
6. Il vincitore è il token emesso.

Esempio con M=2 (4 candidati: grey, dark, wet, windy):
- Turno 1 (g_1): grey (g_1=1) batte dark (g_1=0); wet (g_1=1) batte windy (g_1=0).
- Turno 2 (g_2): tra grey (g_2=0) e wet (g_2=1) vince wet.
- Token emesso: **wet** — anche se non era il più probabile secondo il modello.

Punto importante: il torneo **non** garantisce che vinca il token più probabile in una singola posizione con una chiave fissata — anzi, quasi sempre non è così, ed è proprio da questo scarto che nasce il segnale rilevabile. Ciò che è garantito è che, mediando su tutte le possibili chiavi, la distribuzione risultante coincide con quella originale:

```
E_chiave[ p_torneo(x) ] = p(x)      (proprietà di non distorsione)
```

Per ogni token, essere favorito da una certa chiave in una posizione è compensato dall'essere penalizzato da un'altra chiave (o in un'altra posizione) — mediando, i boost e le penalizzazioni si annullano.

Perché il testo resta comunque di qualità: il torneo può scegliere **solo** tra i candidati effettivamente estratti da `p`, quindi solo tra alternative che il modello considerava già plausibili. Non può mai far vincere un token che il modello giudicava assurdo (avrebbe probabilità pressoché nulla di entrare tra i candidati).

### Esempio numerico: come cambia davvero la distribuzione

La proprietà `E_chiave[p_torneo] = p` è facile da enunciare ma nasconde il punto pratico: **a chiave fissata la distribuzione è alterata, e anche parecchio**. Vale la pena vederlo su un caso minimo — vocabolario di 3 token con `p = (A: 0,70, B: 0,20, C: 0,10)`.

**Formula per M=1.** Si estraggono 2 candidati i.i.d. da `p` e si confrontano con `g_1`. Detta `P_0` la massa totale dei token con g=0:

```
P(x vince) = p_x^2 + 2*p_x * sum_{y!=x} p_y * w(x,y)
```

con `w = 1` se x batte y, `1/2` se pareggiano, `0` se perde. I termini `p_x^2` si cancellano e resta una forma sorprendentemente semplice:

| | fattore di scala |
|---|---|
| token con **g=1** | `p_x -> p_x * (1 + P_0)` |
| token con **g=0** | `p_x -> p_x * P_0` |

L'intuizione: un token con g=0 vince **solo** se l'avversario è anch'esso g=0 (e poi vince il pareggio a monetina), quindi è confinato dentro la sotto-popolazione dei perdenti — da cui il fattore `P_0 < 1`. Un token con g=1 batte tutta la massa `P_0` e pareggia con il resto.

**Le 8 assegnazioni possibili** (ognuna con probabilità 1/8, perché ogni bit g è uniforme e indipendente):

| `(g_A, g_B, g_C)` | `P_0` | A | B | C |
|---|---|---|---|---|
| (1,1,1) | 0 | 70,0% | 20,0% | 10,0% |
| (1,1,0) | 0,10 | 77,0% | 22,0% | 1,0% |
| (1,0,1) | 0,20 | 84,0% | 4,0% | 12,0% |
| (1,0,0) | 0,30 | **91,0%** | 6,0% | 3,0% |
| (0,1,1) | 0,70 | 49,0% | 34,0% | 17,0% |
| (0,1,0) | 0,80 | 56,0% | **36,0%** | 8,0% |
| (0,0,1) | 0,90 | 63,0% | 18,0% | **19,0%** |
| (0,0,0) | 1 | 70,0% | 20,0% | 10,0% |
| **media** | | **70,0%** | **20,0%** | **10,0%** |

Tre osservazioni:

1. **(1,1,1) e (0,0,0) restituiscono `p` intatta**: se tutti i candidati hanno lo stesso bit, ogni scontro è un pareggio e si decide tutto a monetina — il torneo degenera nel campionamento ordinario. È il motivo per cui il segnale nasce dallo *squilibrio* dei bit, non dai bit in sé.
2. **Gli estremi hanno forma chiusa**: massimo `p_x*(2 - p_x) = 1 - (1-p_x)^2` (token con g=1 e tutti gli altri a 0), minimo `p_x^2` (g=0 e tutti gli altri a 1). Qui: A ∈ [49%, 91%], B ∈ [4%, 36%], C ∈ [1%, 19%].
3. **Con M=1 l'ordine non si può ribaltare**: il massimo di B (36%) resta sotto il minimo di A (49%). Il torneo *inclina* la distribuzione, non la stravolge.

**Con M=2** (4 candidati) i vincitori del turno 1 sono i.i.d. tra loro, quindi la stessa formula si itera — è una ricorsione, non un caso nuovo:

```
p^(1) = torneo(p, g_1)   ->   p^(2) = torneo(p^(1), g_2)
```

Con `g_1 = (0,1,1)` e `g_2 = (0,1,1)` (A sfortunato in entrambi i turni):

| | A | B | C |
|---|---|---|---|
| `p` originaria | 70,0% | 20,0% | 10,0% |
| dopo turno 1 (`P_0`=0,70) | 49,0% | 34,0% | 17,0% |
| dopo turno 2 (`P_0`=0,49) | **24,0%** | **50,7%** | 25,3% |

Qui l'ordine **si ribalta**: B supera A. È il compromesso di M visto in concreto (cfr. "Perché più funzioni g aiutano"). La non distorsione continua a valere per induzione: ogni turno conserva la media rispetto al proprio `g_m`, e i `g_m` sono indipendenti tra loro.

**Il segnale che ne deriva.** A parità di assegnazione, la probabilità che il token emesso abbia g=1 è `P_1*(1 + P_0) = 1 - P_0^2`. Mediando sulle assegnazioni si ottiene lo score atteso del rilevatore per M=1:

```
E[score] = 3/4 - (sum_i p_i^2) / 4
```

Nell'esempio `sum p^2 = 0,54` → **E[score] = 0,615** invece di 0,5.

Questa formula chiude il cerchio sul limite del metodo: con distribuzione deterministica (un token a probabilità 1, `sum p^2 = 1`) lo score vale esattamente 0,5 — **nessun watermark possibile**; con distribuzione piatta su vocabolario grande (`sum p^2 -> 0`) tende a 0,75. Il watermark vive dell'entropia della distribuzione: dove il modello non ha scelta, non c'è nulla in cui nascondere il segnale. Da qui l'interazione con temperatura, top-k e top-p (§3-4): ogni intervento che concentra la massa su un solo token riduce anche la capacità di watermarking.

### Verifica — passo per passo

Il rilevatore ha solo: il testo e la chiave. Per ogni token `x_t` del testo:

1. legge il contesto precedente (H token) e ricalcola `r_t` (identico calcolo della generazione);
2. calcola `g_1(x_t, r_t), ..., g_M(x_t, r_t)` — **solo sul token presente**, senza sapere quali altri candidati fossero in gara né rifare il torneo;
3. somma quei bit.

Score complessivo su tutto il testo (T token):

```
score = (somma di tutti i bit su tutte le posizioni) / (M * T)
```

- Testo non watermarkato: i bit g sono statisticamente scorrelati dal contenuto → score tende a **0,5**.
- Testo prodotto dal torneo con quella chiave: i token emessi sono stati sistematicamente selezionati per avere g alti → score **> 0,5**.

Si fissa una soglia (calibrata sui falsi positivi accettabili) e si classifica il testo. Il rumore attorno alla media scala come `1/sqrt(M*T)`: servono nell'ordine di alcune centinaia di token per una rilevazione affidabile; su frasi brevi il test non è conclusivo — non per un difetto implementativo, ma per un limite statistico intrinseco.

### Perché più funzioni g aiutano

Ogni g aggiuntiva è una misura statisticamente indipendente sullo stesso token (indipendente perché l'hash con `m` diverso produce output scorrelati anche a parità di `r` e `x`). Con M misure invece di 1, il rumore scala come `1/sqrt(M*T)` invece che `1/sqrt(T)`: a parità di affidabilità richiesta, serve un testo più corto. Il prezzo è che il torneo diventa più selettivo (un token deve sopravvivere a più turni consecutivi per vincere), quindi ci si allontana un po' di più dal "token più probabile secondo il modello" — lo stesso compromesso di M, visto da un'altra angolazione.

### Due configurazioni nel paper

- **Non distorsiva**: la distribuzione del testo generato è (dimostrabilmente) identica a quella senza watermark; nessuna perdita di qualità misurabile, ma serve testo più lungo per la rilevazione.
- **Distorsiva**: spinge di più sui g alti, rilevabilità superiore a parità di lunghezza del testo, ma introduce un'alterazione misurabile della distribuzione.

**Repeated context masking**: se lo stesso contesto ricorre più volte nel testo, riapplicare lo stesso seed/g produrrebbe ripetizioni innaturali. Il metodo rileva i contesti già visti e in quei punti campiona normalmente (senza torneo), perdendo un po' di segnale ma preservando la naturalezza del testo.

### Confronto riassuntivo dei tre schemi

| Schema | Estrazioni per token | Cosa decide la chiave | Verificabile senza modello? |
|---|---|---|---|
| Seed fisso (es. 42) | 1 | Nulla (riproducibilità pura) | — |
| Seed = hash(chiave, contesto) | 1 | Dove cade il punto sul segmento | No (serve `p` per sapere cosa avrebbe prodotto quel seed) |
| SynthID (torneo) | 2^M | Chi vince gli scontri tra candidati già estratti | Sì (basta valutare g sul token presente) |

Il salto concettuale di SynthID è spostare l'intervento dal "dado" (il seed che sceglie il punto sul segmento) all'"arbitro" (il torneo che seleziona tra più lanci del dado già avvenuti) — è questo spostamento a rendere la verifica possibile guardando solo il testo, e a permettere una garanzia formale di non distorsione (in media sulle chiavi) invece di un compromesso tarato a occhio come nello schema con bonus ai logit — la green list / red list di **Kirchenbauer, J., Geiping, J., Wen, Y., Katz, J., Miers, I. & Goldstein, T. (2023)**, *A Watermark for Large Language Models*, ICML — che aggiunge un bonus δ ai logit dei token con g=1 prima della softmax, distorcendo direttamente e permanentemente la distribuzione.
