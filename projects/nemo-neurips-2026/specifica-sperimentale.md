# Astrazioni performativamente stabili

## Specifica sperimentale

**Titolo di lavoro**: *Performatively stable abstractions: when a learned library produces the evidence that confirms it*

**Target**: NEmo 2026 (Neuro-Symbolic Embodied Intelligence), workshop NeurIPS 2026 — short paper, ≤ 4 pagine, non-archival
**Deadline**: 10 settembre 2026

---

# Parte 0 — Note di comprensione

> Questa parte non fa parte della specifica tecnica. Serve a fissare i punti che generano più confusione, in linguaggio piano. Chi conosce già il progetto può saltarla.

## 0.1 Che differenza c'è tra gli agenti A e B

**Una sola cosa: quante alternative riescono a esaminare prima di decidere.**

Tutto il resto è identico. Stessi ordini in ingresso, stessa libreria, stesso obiettivo (minimizzare i viaggi), stesse azioni disponibili.

Arriva un ordine da 11 pezzi, con carrello da 6. Entrambi gli agenti hanno `lotto_4` in libreria, imparata nella fase iniziale.

**Agente A** esamina tutte le partizioni possibili:

```
6+5        2 viaggi   ← sceglie questa
6+4+1      3 viaggi
5+4+2      3 viaggi
4+4+3      3 viaggi
...
```

**Agente B** ne esamina solo venti, e le esamina **nell'ordine dettato dalla libreria**: i piani che usano `lotto_4` sono i più corti da scrivere nel suo vocabolario, quindi vengono per primi. Nelle sue venti espansioni trova `4+4+3`, `4+4+2+1`, `4+3+4`. **`6+5` non ci arriva**, perché quel ramo era in fondo alla coda.

```
4+4+3      3 viaggi   ← sceglie questa
```

A non è più intelligente. Ha solo il tempo di guardare tutto.

## 0.2 Perché questo produce una divergenza

Ripeti per cinquanta episodi con ordini vari:

| Ordine | Tracce di A | Tracce di B |
|---|---|---|
| 11 | 6, 5 | 4, 4, 3 |
| 7 | 6, 1 | 4, 3 |
| 12 | 6, 6 | 4, 4, 4 |
| 9 | 6, 3 | 4, 4, 1 |
| 6 | 6 | 4, 2 |

**A ha eseguito lotti di dimensione**: 1, 3, 5, 6
**B ha eseguito lotti di dimensione**: 1, 2, 3, 4

B non ha **mai** eseguito un lotto da 5 o da 6. Non perché non gli siano stati chiesti — gli sono arrivati gli stessi ordini di A. Perché il suo modo di eseguirli non li produce.

## 0.3 Perché B resta bloccato

Il sistema impara guardando le proprie tracce.

- **A** vede tanti lotti da 6 → impara `lotto_6` → ora ha due macro a dimensione diversa → scatta la regola *"se ho due macro identiche tranne che per il numero, forse il numero è un parametro"* → propone `trasporta_lotto(oggetto, q)` → MDL accetta (il suo buffer ha sei dimensioni distinte) → **promosso**
- **B** vede lotti da 4 ovunque e residui sparsi troppo rari → resta con una sola macro → la regola non scatta → lo schema **non viene nemmeno proposto**

## 0.4 Le due quantità da non confondere

```
k_ordini    quanti conteggi distinti il mondo ha offerto      (input)
k_buffer    quante dimensioni di lotto compaiono nelle tracce (output)
```

`k_buffer` **non è un parametro**: è ciò che risulta. Per A le due curve coincidono. Per B divergono: `k_ordini` sale, `k_buffer` resta piatto.

> **La divergenza tra `k_ordini` e `k_buffer` è la misura più diretta del fenomeno.** Ed è calcolabile dall'agente su se stesso, senza sapere quale sia l'ottimo.

## 0.5 "Ma il budget lo imposti tu"

Sì. È un parametro dell'esperimento. La domanda giusta non è chi decide il numero venti, ma **se quel vincolo rappresenti qualcosa di reale**.

Un pianificatore reale non può enumerare tutte le alternative — nel toy le partizioni sono decine, in un magazzino vero sono astronomiche. Quindi ogni sistema **si ferma prima**, e deve decidere cosa guardare per primo. La risposta universale, da HTN in poi, è: *ciò che è esprimibile con le astrazioni che hai*. È la ragione per cui si costruisce una libreria.

> Il numero venti è arbitrario. **Il fatto che esista un limite non lo è.**

E ciò che l'esperimento non impone è la catena che ne segue: che B non esegua mai lotti da 6, che quindi non impari `lotto_6`, che quindi la regola non scatti. Quella è **conseguenza**, non progetto. Potrebbe non verificarsi — ed è per questo che l'esperimento ha senso.

## 0.6 Il risultato non è "guarda tutto"

A non è realistico: nessun sistema vero può enumerare tutte le alternative. **A serve come metro di misura, non come raccomandazione.** È il righello contro cui si quantifica il danno, come si misura l'errore di un'approssimazione confrontandola con la soluzione esatta senza per questo suggerire di usare la soluzione esatta.

Il risultato utilizzabile viene dalla **condizione C**: stesso budget stretto di B, ma varietà fin dall'inizio. C non si blocca.

> Se non puoi permetterti la ricerca ampia — e non puoi — allora **la varietà dell'esperienza iniziale determina se potrai correggerti**.

## 0.7 Non è una linea, è una griglia

Le tre condizioni variano **due cose diverse**:

| | budget | esperienza iniziale |
|---|---|---|
| **A** | largo | povera |
| **B** | stretto | povera |
| **C** | stretto | **ricca** |

- **A vs B**: stesso ambiente, budget diverso → isola l'effetto delle risorse
- **B vs C**: stesso budget, ambiente diverso → isola l'effetto della povertà iniziale

```
                    budget stretto      budget largo
esperienza povera   ← blocco qui →          ok
esperienza ricca         ok                 ok
```

Facendo variare entrambi con continuità si ottiene una **mappa**: una regione di blocco e un confine. Non "sotto 30 non generalizza", ma "sotto 30 **e** con almeno tanta povertà iniziale".

## 0.8 Cosa succede se il grafico è una degradazione lineare

Sarebbe un risultato debole: *meno risorse, peggio* è ovvio.

Il risultato forte richiede una **transizione netta** — sopra una soglia tutti si riprendono, sotto nessuno. E ancora meglio se il confine corrisponde a un valore fisso di `k_buffer` **indipendentemente da come ci si è arrivati**, per budget largo o per varietà alta. In quel caso:

> Non conta quanto cerchi né quanto è vario il mondo. Conta quanta varietà finisce nelle tue tracce, e la soglia è questa.

## 0.9 Dove sta esattamente la parte di machine learning

In un punto solo: **come B decide quali venti alternative guardare**.

Nella variante ENUM è una regola scritta a mano (ordina per lunghezza di codifica). Nella variante LEARN è un piccolo modello addestrato sulle partizioni **effettivamente eseguite**, che campiona venti proposte invece di enumerarle.

E qui il meccanismo diventa più diretto: il modello di B è stato addestrato su cento episodi di `4+4+...`, quindi campiona lotti da quattro **non perché costino meno da scrivere, ma perché il 6 è quasi assente dal suo training set**.

| | Regola (ENUM) | Modello (LEARN) |
|---|---|---|
| Perché `6+5` non emerge | costa molto in codifica | il modello non l'ha mai visto |
| Chi ha scritto il criterio | il progettista | nessuno — è appreso |
| Corrispondenza col reale | approssimazione | è ciò che accade davvero |

È letteralmente come funzionano gli agenti oggi: un agente LLM che accumula skill genera piani condizionati sulle skill in contesto e sulla propria storia. Non enumera nulla — campiona da una distribuzione plasmata da ciò che ha già fatto.

## 0.10 I tre controlli che passano e falliscono comunque

| Controllo | Cosa garantisce | Cosa non vede |
|---|---|---|
| **Verifica** | la macro è corretta **dove è applicabile** | che l'applicabilità dichiarata sia giustificata |
| **MDL** | la macro comprime **i dati osservati** | che i dati osservati siano rappresentativi |
| **Performance** | il sistema fa il suo lavoro | che potrebbe farlo meglio |

Nessuno dei tre è sbagliato. Sono tutti **condizionati su qualcosa che il sistema ha contribuito a determinare**.

> Correttezza, parsimonia e performance sono tutte condizionate sui dati che il sistema ha prodotto. Nessuna è una garanzia di generalizzazione. Serve una quarta proprietà, che nessuno misura: **la giustificazione dell'astrazione nell'esperienza osservata**.

## 0.11 Se il meccanismo di astrazione esiste già, esistono agenti autonomi?

No, e le due cose non sono in contraddizione.

Ciò che esiste sono **motori di induzione** molto bravi (DreamCoder scopre la moltiplicazione dall'addizione; STEVIE scopre il fold; Stitch comprime in modo ottimo). Ma operano in condizioni molto particolari:

- il corpus è dato, curato e vario
- le primitive sono date
- **offline**: vedono tutto insieme, comprimono una volta
- domini giocattolo, nessuna percezione, nessun obiettivo proprio

Perché siano agenti mancano quattro cose, nessuna risolta: il **grounding** (dal flusso continuo ai simboli), la **scelta degli obiettivi**, il **regime online** (decidere con evidenza parziale, senza tornare indietro), la **scala**.

E i sistemi in produzione — gli agenti LLM con skill library — sembrano autonomi ma **ereditano** le astrazioni invece di scoprirle: sanno cos'è un ciclo o una procedura perché erano già nel corpus di addestramento. Il dato di SkillsBench (skill umane +16 punti, skill scritte da LLM guadagno nullo) è la misura di questa differenza.

> Questo lavoro studia il punto di rottura tra i due regimi. Non "come si scopre un'astrazione" — risolto. Ma **cosa succede al meccanismo quando lo si toglie dal laboratorio**, che è ciò che separa un motore di induzione da un agente.

## 0.12 Il punto di forza, e il suo caveat

**Nessuno misura `k_buffer`.** La letteratura misura proprietà del *risultato*: quante astrazioni, quanto comprimono, quanto migliorano le performance. Questa è una proprietà dell'*esperienza*, calcolabile dall'interno, che media due fattori diversi e ha una soglia prevedibile analiticamente.

**Il caveat**: vale se il diagramma di fase mostra una soglia netta. Se mostra una degradazione graduale, il contributo si riduce a "meno risorse fanno peggio", che non basta.

> È il gate del pilot a stabilire se il punto di forza esiste. Per questo `k_buffer` va misurato fin dal primo pilot, non trattato come metrica accessoria.

---

# Parte I — Il problema

## 1. Il contesto

Un agente che opera in un ambiente per lungo tempo si trova a ripetere sequenze di azioni simili. Una famiglia di metodi — dal *library learning* nella sintesi di programmi al *option discovery* nel reinforcement learning — propone che l'agente estragga da queste ripetizioni delle **astrazioni riusabili**: macro-azioni, skill, option, funzioni di libreria. L'astrazione viene poi usata per pianificare, e i piani diventano più corti perché espressi in un vocabolario più ricco.

Questo processo è tipicamente descritto come un **ciclo**:

```
l'agente agisce
    → raccoglie tracce
        → estrae astrazioni dalle tracce
            → le usa per pianificare
                → agisce diversamente
                    → raccoglie tracce diverse
                        → ...
```

Nella letteratura questo ciclo è considerato **virtuoso**: le astrazioni scoperte in un'iterazione fungono da impalcatura per comportamenti più complessi nell'iterazione successiva, e ogni giro amplia le capacità dell'agente. È un'assunzione esplicita e documentata empiricamente: agenti che eseguono il ciclo esplorano ambienti in un ordine di grandezza meno passi di agenti che non lo fanno.

## 2. L'osservazione che motiva questo lavoro

Il ciclo ha una proprietà che merita attenzione: **l'astrazione non si limita a descrivere l'esperienza dell'agente, contribuisce a produrla.**

Una volta che una macro è in libreria, i piani che la usano sono più economici da rappresentare e più rapidi da trovare. L'agente tende quindi a produrre comportamenti che la impiegano. Le tracce risultanti contengono quella macro in abbondanza. Al giro successivo, il criterio di apprendimento — qualunque esso sia — osserva dati in cui quella macro è chiaramente utile, e la conferma.

Il ciclo, in altre parole, può chiudersi su se stesso.

Questo è problematico quando l'astrazione è stata promossa **prematuramente**, cioè sulla base di un'esperienza non ancora rappresentativa. Il caso paradigmatico:

> Un agente osserva cento episodi in cui deve trasportare esattamente quattro oggetti. Impara la macro `lotto_4`. È una buona macro: comprime le tracce, funziona, supera qualunque verifica.
>
> Poi cominciano ad arrivare ordini da sette, undici, tre oggetti. La macro corretta sarebbe stata `trasporta_lotto(oggetto, q)` — parametrica nella quantità. Ma `lotto_4` è già in libreria, i piani che la usano sono i primi a essere trovati, e l'agente continua a decomporre gli ordini in gruppi da quattro anche quando non conviene.
>
> Le tracce che genera contengono ancora prevalentemente lotti da quattro. Il criterio di apprendimento continua a confermare `lotto_4`.

**Nessun passaggio contiene un errore.** Il criterio di compressione calcola correttamente. Il pianificatore produce piani validi. La verifica passa: la macro fa esattamente ciò che promette su tutto ciò che l'agente esegue.

E tuttavia l'agente è bloccato in un vocabolario subottimale, e non ha alcun segnale interno che glielo dica.

## 3. La domanda di ricerca

> **Esiste un regime in cui un'astrazione promossa prematuramente genera l'evidenza che la conferma, impedendo o rallentando la propria correzione?**

E, se esiste:

- **Quando?** Sotto quali condizioni di forza della retroazione e di povertà dell'esperienza iniziale?
- **Come?** Attraverso quale meccanismo specifico?
- **È rilevabile?** Le metriche interne al sistema lo segnalano, o il blocco è invisibile dall'interno?

## 4. Tre cose che vanno tenute distinte

Il rischio principale di un lavoro del genere è dimostrare qualcosa di più debole di quel che si annuncia. Tre fenomeni si assomigliano e non sono la stessa cosa.

### 4.1 Curriculum bias — `dati → astrazione`

L'agente vede dati poco vari all'inizio e impara di conseguenza. Vero, noto, poco interessante. **Non richiede alcun ciclo**: basta un ordine di presentazione sfavorevole.

### 4.2 Lock-in rappresentazionale — `astrazione → scrittura della traccia → astrazione`

L'astrazione cambia il modo in cui l'esperienza viene registrata nel buffer. Se ogni volta che l'agente usa `lotto_4` la traccia contiene il simbolo `lotto_4`, non sorprende che `lotto_4` risulti frequente.

Questo è **quasi tautologico**, ed è la trappola principale nel disegno di questo esperimento. Un revisore lo identifica subito.

### 4.3 Autoconferma performativa — `astrazione → comportamento fisico → dati → astrazione`

L'astrazione cambia **cosa l'agente fa nel mondo**: quali azioni primitive esegue, quali stati visita, quanto costa. Le tracce risultanti differiscono a livello di azioni primitive, non solo di notazione.

**È questo il fenomeno da dimostrare**, e il requisito che ne discende governa l'intero disegno del dominio:

> Decomposizioni diverse dello stesso compito devono produrre **sequenze primitive e stati fisicamente diversi**.

## 5. Il vocabolario

Il fenomeno appartiene a una famiglia già formalizzata in un altro contesto — quello della **predizione performativa**, dove si studia il fatto che distribuire un modello predittivo può cambiare la distribuzione che il modello vuole predire. Il caso di scuola è la banca che stima un alto rischio di insolvenza, assegna un tasso alto di conseguenza, e con ciò aumenta davvero il rischio: una profezia che si autoavvera.

Da lì si prendono in prestito due nozioni, che useremo senza dimostrare nulla:

- una configurazione è **performativamente stabile** se è un punto fisso del riaddestramento: la distribuisci, ti riaddestri sui dati che induce, e riottieni la stessa configurazione
- una configurazione è **performativamente ottimale** se minimizza il costo su una distribuzione di valutazione esterna

Il fatto centrale è che **le due non coincidono**. Un sistema può essere perfettamente stabile — nessun segnale di errore, nessun incentivo interno a cambiare — e trovarsi in un punto peggiore di dove potrebbe essere.

L'obiettivo empirico di questo lavoro è **misurare la distanza tra i due nel library learning online**.

## 6. Cosa questo lavoro non fa

- **Non propone una cura.** Caratterizza un regime.
- **Non batte una baseline.** Non c'è nessun sistema con cui competere: il sistema studiato è deliberatamente il più semplice possibile, perché è uno strumento di misura, non un contributo.
- **Non afferma che il fenomeno sia sconosciuto.** Esistono precedenti in RL, nell'apprendimento continuo e nella letteratura performativa. Il contributo è mostrare una forma **complementare e più difficile da rilevare**: il fallimento avviene mentre le metriche interne dicono che tutto va bene.

---

# Parte II — Il dominio

## 7. Requisiti di disegno

Il dominio deve soddisfare quattro vincoli, e ciascuno risponde a un rischio specifico.

| Requisito | Perché |
|---|---|
| Decomposizioni diverse dello stesso compito hanno **conseguenze fisiche diverse** | altrimenti si dimostra §4.2 invece di §4.3 |
| Esiste una **metrica esterna** al vocabolario dell'agente | altrimenti la valutazione è circolare: la libreria rende economici i propri simboli |
| L'ottimo è **noto per costruzione** | serve la baseline contro cui misurare il gap |
| Il chunk prematuro è **plausibile**, non ovviamente sbagliato | se fosse sempre pessimo, l'agente avrebbe un segnale netto e il fenomeno non emergerebbe |

## 8. L'ambiente

Un robot di magazzino con un **carrello di capacità limitata** `C` (default 6).

### 8.1 Azioni primitive

```
vai_a(Luogo)          spostamento tra deposito e scatola
carica(Oggetto)       mette un oggetto nel carrello; fallisce se il carrello è pieno
scarica               deposita un oggetto dal carrello nella scatola
verifica              controllo finale
```

Il vincolo di capacità è **l'elemento centrale del disegno**: è ciò che rende le decomposizioni fisicamente non equivalenti.

### 8.2 Ordini e piani

Un **ordine** è una coppia `(Oggetto, N)`: riempire la scatola con `N` unità di `Oggetto`.

Poiché il carrello contiene al massimo `C` oggetti, un ordine da `N > C` richiede più viaggi. Un **piano** è una partizione:

```
N = q₁ + q₂ + … + qₘ        con ogni qᵢ ≤ C
```

Ogni lotto `qᵢ` si esegue come:

```
vai_a(deposito), carica × qᵢ, vai_a(scatola), scarica × qᵢ
```

### 8.3 Le decomposizioni non sono equivalenti

Per un ordine da 11 unità con `C = 6`:

```
6 + 5       →  2 viaggi,  22 azioni di carico/scarico
4 + 4 + 3   →  3 viaggi,  22 azioni di carico/scarico
11 × 1      → 11 viaggi,  22 azioni di carico/scarico
```

Stesso numero di oggetti spostati, **numero di viaggi diverso**. Sequenze primitive diverse, stati intermedi diversi, costo diverso.

### 8.4 Costo fisico

```
C_fisico(piano) = n_viaggi × 2 × w_move + 2 × Σ qᵢ
```

con `w_move = 10` (default), abbastanza alto da far dominare il numero di viaggi.

Poiché `Σ qᵢ = N` è fissato dall'ordine, **minimizzare il costo fisico equivale a minimizzare il numero di lotti**.

> **Conseguenza**: l'ottimo fisico per un ordine `N` usa esattamente `⌈N/C⌉` lotti. Noto per costruzione, zero ambiguità.

**Test da implementare il primo giorno:**

```python
for N in range(2, N_max + 1):
    assert min(len(p) for p in all_partitions(N, C)) == ceil(N / C)
```

Se il costo fisico è definito male, tutto il resto misura la cosa sbagliata.

### 8.5 Il chunk prematuro è localmente utile

Questo è il dettaglio che rende il fenomeno realistico. Con `C = 6`, un agente che partiziona sempre in lotti da 4:

| N | Partizione | Viaggi | Ottimo | Regret |
|---|---|---|---|---|
| 2 | 2 | 1 | 1 | 0 |
| 3 | 3 | 1 | 1 | 0 |
| 4 | 4 | 1 | 1 | 0 |
| 5 | 4+1 | 2 | 1 | **1** |
| 6 | 4+2 | 2 | 1 | **1** |
| 7 | 4+3 | 2 | 2 | 0 |
| 8 | 4+4 | 2 | 2 | 0 |
| 9 | 4+4+1 | 3 | 2 | **1** |
| 10 | 4+4+2 | 3 | 2 | **1** |
| 11 | 4+4+3 | 3 | 2 | **1** |
| 12 | 4+4+4 | 3 | 2 | **1** |

> Il chunk **non è cattivo**: è ottimo per alcuni conteggi (4, 7, 8), subottimo per altri, e in modo irregolare. È precisamente per questo che sopravvive — l'agente non riceve mai un segnale netto e consistente che sia sbagliato.

La struttura del regret in funzione di `N` è un dato da riportare nel paper, non un dettaglio.

## 9. Il flusso di ordini esterni

La sequenza di compiti che il mondo presenta all'agente. **Deve essere identica in tutte le condizioni sperimentali**: è il vincolo che rende valido ogni confronto.

### 9.1 Parametri

```
seq_len     ordini nella vita dell'agente        default 500
N_range     intervallo dei conteggi              default [2, 12]
C           capacità del carrello                default 6
objects     oggetti distinti                     default 5
schedule    evoluzione della distribuzione di N
k_poor      lunghezza della fase povera          default 100
```

### 9.2 Schedule

| Nome | Descrizione |
|---|---|
| `poor_then_rich` | primi `k_poor` ordini tutti con `N = 4`; poi `N` uniforme su [2,12] |
| `rich` | `N` uniforme su [2,12] fin dall'inizio |
| `poor_forever` | `N = 4` sempre |
| `slow_drift` | `N` concentrato su 4, varianza crescente linearmente |

### 9.3 Gli oggetti variano sempre

In ogni schedule l'oggetto cambia da un ordine all'altro. Questo serve a un fine preciso: il sistema deve avere **una dimensione lungo cui astrarre correttamente fin dall'inizio**. `Oggetto` è un parametro legittimo, osservato variare, e la macro che lo espone è giustificata.

Così, quando il sistema fallisce, il fallimento riguarda specificamente `q` — non l'astrazione in generale.

### 9.4 Verifica dell'identità dei flussi

```python
def make_stream(schedule, k_poor, seed, seq_len, N_range, objects):
    ...   # deterministico in (schedule, k_poor, seed)

def stream_hash(stream):
    return sha256(repr(stream).encode()).hexdigest()

# prima di ogni run della griglia:
assert stream_hash(stream) == expected[(schedule, k_poor, seed)], \
       "il flusso di ordini è divergente: esperimento invalido"
```

> Se le condizioni ricevono flussi diversi, l'intero confronto è privo di significato — e **non ce ne si accorgerebbe guardando i risultati**. Da implementare il primo giorno.

---

# Parte III — Il sistema

Il sistema è deliberatamente minimale. Non è l'oggetto di studio: è lo strumento di misura. Ogni elemento non necessario a far emergere o a diagnosticare il fenomeno è stato rimosso.

## 10. Rappresentazione delle astrazioni

### 10.1 La macro

In questo dominio una macro è completamente descritta da due campi:

```python
@dataclass(frozen=True)
class Macro:
    name: str
    q: int | None      # int  → chunk a dimensione fissa
                       # None → schema parametrico
```

- `Macro("lotto_4", q=4)` — **chunk**: trasporta esattamente 4 unità
- `Macro("trasporta_lotto", q=None)` — **schema**: trasporta `q` unità, con `q` argomento

L'oggetto è argomento in entrambi i casi.

> **La distinzione chunk/schema — che è il cuore del fenomeno studiato — si riduce a `q is None`.**

Nessun DSL generale, nessun lambda calcolo, nessuna anti-unificazione su termini arbitrari. Da dichiarare apertamente nel paper come semplificazione deliberata: il dominio ha una sola forma di astrazione possibile, e questo è ciò che lo rende diagnostico.

### 10.2 Vincolo semantico

Lo schema parametrizza la **dimensione del lotto**, non il totale dell'ordine:

```
trasporta_lotto(Oggetto, q)        con  1 ≤ q ≤ C
```

Un'astrazione che accettasse `q = 11` con `C = 6` sarebbe semanticamente invalida: nessun singolo lotto può superare la capacità del carrello. Il livello dell'ordine resta la partizione, decisa dal proponente.

| | Struttura per N = 11 | Viaggi |
|---|---|---|
| **Schema** | `trasporta_lotto(o,6) ; trasporta_lotto(o,5)` | 2 |
| **Chunk prematuro** | `lotto_4(o) ; lotto_4(o) ; [3 primitive]` | 3 |

## 11. Il criterio di apprendimento: MDL

Il principio di minima lunghezza di descrizione. L'ipotesi migliore è quella che permette di descrivere i dati nel modo più breve possibile, **contando anche la lunghezza dell'ipotesi stessa**:

```
J(H, D) = L(H) + L(D | H)
```

Il secondo termine da solo premierebbe la memorizzazione; il primo la punisce. È il criterio standard del library learning, e usarlo invariato è deliberato: **il fenomeno deve emergere con il criterio che tutti usano**, non con una variante costruita ad hoc.

### 11.1 Costo di codifica dei dati

```python
def encoding_len(plan, lib, C):
    v = log2(N_PRIMITIVES + len(lib))        # bit per simbolo del vocabolario
    total = 0.0
    for it in plan:
        if isinstance(it, MacroCall):
            total += 2 * v                   # simbolo della macro + oggetto
            if lib[it.name].q is None:
                total += log2(C)             # l'argomento q, solo per lo schema
        else:
            total += (2 + 2 * it.q) * v      # vai_a × 2, carica × q, scarica × q
    return total
```

### 11.2 Costo della libreria

```python
def L_H(lib, C, fold_overhead):
    v = log2(N_PRIMITIVES + len(lib))
    return sum(
        (2 + 2*C) * v + fold_overhead if m.q is None    # definizione con repeat
        else (2 + 2*m.q) * v                            # definizione a q fisso
        for m in lib.values()
    )
```

Il vocabolario cresce a ogni promozione: `log₂(|V|)` aumenta, e il costo si ripercuote su tutta la libreria. È questo che penalizza la proliferazione di chunk.

### 11.3 L'asimmetria di invocazione

Un dettaglio che **emerge dalla formula e non è imposto**, ma che avrà un ruolo diagnostico:

```
invocare  lotto_4(o)                costa   2v
invocare  trasporta_lotto(o, 4)     costa   2v + log₂(C)
```

**Il chunk specializzato è più economico da invocare dello schema istanziato allo stesso valore**, perché non deve trasmettere l'argomento.

Conseguenza non ovvia: anche dopo che lo schema è stato promosso, la generazione dei piani può continuare a raggiungere prima quelli basati sul chunk. È il meccanismo che rende plausibile la diagnosi *proposer non-use* (§16.3), e va misurato, non assunto.

### 11.4 La predizione a priori

Il costo della famiglia di chunk cresce linearmente nel numero di conteggi distinti `k`; quello dello schema è costante. Esiste quindi un punto di pareggio:

```
k* ≈ fold_overhead / c_macro
```

> **Sostituire i valori effettivi del proprio `L_H`, calcolare `k*`, scriverlo e datarlo prima di eseguire qualunque codice.**

Una predizione numerica formulata prima dell'esperimento e poi confermata è una forma di argomentazione più forte di qualunque figura, e in questa letteratura è rara.

## 12. Il proponente

Il proponente genera i piani candidati. È **il canale attraverso cui la libreria influenza il comportamento**, quindi è il componente su cui si concentra il disegno sperimentale.

### 12.1 Un principio non negoziabile

> **Il criterio di scelta finale è il solo costo fisico.** Nessun termine simbolico compare nell'obiettivo, in nessuna variante.

Questo evita l'obiezione più seria che si può fare a un esperimento del genere: *avete messo nell'obiettivo la preferenza che produce il risultato*. Il robot non preferisce i piani più corti da scrivere. Preferisce quelli che costano meno viaggi. La libreria influenza **quali piani vengono trovati**, non quali vengono preferiti.

### 12.2 Variante ENUM — ricerca sotto budget

Il proponente primario. Ricerca su partizioni, con priorità data dalla lunghezza di codifica nella libreria corrente e un limite di nodi espandibili.

```python
def plan_enum(order, lib, budget, C):
    obj, N = order
    best_plan, best_phys = None, inf
    expanded = 0
    frontier = [(0.0, [], N)]                    # (priorità, parziale, residuo)

    while frontier and expanded < budget:
        _, partial, rem = heappop(frontier)
        expanded += 1
        if rem == 0:
            c = physical_cost(partial)
            if c < best_phys:
                best_plan, best_phys = partial, c
            continue
        for it in successors(obj, rem, lib, C):
            new = partial + [it]
            heappush(frontier, (encoding_len(new, lib, C), new, rem - it.q))

    return best_plan, expanded, (expanded >= budget)
```

Tre proprietà, che costituiscono l'intero disegno:

| Proprietà | Effetto |
|---|---|
| priorità = lunghezza di codifica | la libreria determina **l'ordine di esplorazione** |
| valore restituito = costo fisico minimo | **nessun termine simbolico nell'obiettivo** |
| budget tronca la ricerca | la libreria determina **cosa viene trovato in tempo** |

Con `lotto_4` in libreria e budget stretto, la partizione `4+4+3` viene raggiunta molto prima di `6+5`, perché il suo prefisso ha lunghezza di codifica minima. Non è imposto: cade fuori dalla funzione di priorità.

**Parametro di retroazione**: `B`, il numero di nodi espandibili.

- `B = ∞` → ricerca esaustiva, la libreria non influenza l'esito → **nessun ciclo**
- `B` piccolo → l'esito dipende dall'ordine di esplorazione, quindi dalla libreria → **ciclo pieno**

> Il budget è un **vincolo di risorse, non una preferenza**. E il legame con il dominio è diretto: la pianificazione gerarchica esiste precisamente perché la ricerca è limitata.

### 12.3 Variante LEARN — proponente generativo

La seconda condizione. Serve a mostrare che il fenomeno non dipende dal particolare meccanismo di retroazione, e a collegare il risultato ai sistemi reali.

**Il modello**: autoregressivo sulle partizioni. Dato `(oggetto, N, libreria)`, predice `q₁`, poi `q₂ | q₁`, e così via fino a esaurire `N`.

```
architettura   GRU o transformer minimo: 2 layer, hidden 64
input          embedding di (N residuo, lotti già scelti, macro disponibili)
output         distribuzione su q ∈ {1 … min(C, N_residuo)}
training       cross-entropy sulle partizioni EFFETTIVAMENTE ESEGUITE
```

> **Volutamente piccolo.** Un modello ad alta capacità memorizzerebbe il buffer, e il fenomeno diventerebbe un artefatto di capacità invece che una proprietà del ciclo.

```python
def plan_learn(order, lib, model, k_samples, C):
    cands = [model.sample_partition(order, lib, C) for _ in range(k_samples)]
    cands = [c for c in cands if is_valid(c, order, C)]
    if not cands:
        cands = [greedy_fallback(order, C)]
    return min(cands, key=physical_cost)      # criterio: solo costo fisico
```

**Parametro di retroazione**: `k_samples`.

- `k` grande → si copre lo spazio, il modello conta poco
- `k = 1` → si esegue ciò che il modello propone

**Riaddestramento**: fine-tuning incrementale a ogni intervallo di promozione, sulle partizioni eseguite.

### 12.4 Perché LEARN è la versione realistica

| | ENUM | LEARN |
|---|---|---|
| Meccanismo | *la libreria decide cosa trovo prima* | *ho eseguito lotti da 4, quindi campiono lotti da 4* |
| Origine del vincolo | imposto dal progettista | emerge dalla distribuzione appresa |
| Corrispondenza con i sistemi reali | approssimazione | è ciò che accade con un proponente generativo |
| Controllabilità | alta | media |
| Diagnosticità | alta | ridotta |

Nei sistemi che operano oggi — inclusi gli agenti basati su modelli linguistici, dove il proponente è un modello condizionato sulle astrazioni disponibili in contesto — la retroazione ha la forma di LEARN. ENUM è il modo di studiarla in condizioni controllate.

### 12.5 I due canali di retroazione

In LEARN il ciclo si chiude in **due punti distinti**:

```
(i)   libreria → codifica dei piani → probabilità di generazione     [presente anche in ENUM]
(ii)  traiettorie eseguite → training del proponente → piani campionati    [solo LEARN]
```

Si possono ablare separatamente:

| Condizione | Canale (ii) |
|---|---|
| `retrain_incremental` | **attivo** — il modello accumula il passato |
| `retrain_from_scratch` | **spezzato** — riaddestrato da zero sul buffer completo a ogni intervallo |
| `retrain_recent_only` | **attenuato** — solo sugli ultimi `W` episodi |

Se il blocco sparisce con `from_scratch`, il canale (ii) è causale. È un'analisi che ENUM non permette.

### 12.6 Esplorazione

```
con probabilità 1 − ε   → il piano prodotto dal proponente
con probabilità ε       → una partizione ammissibile scelta a caso
```

`ε` fisso e **identico in tutte le condizioni** (default 0.1).

**Da loggare comunque**: entropia delle partizioni scelte, numero di dimensioni di lotto distinte esplorate.

> La riduzione dell'esplorazione *effettiva* è parte del meccanismo performativo e va misurata, non nascosta. Non si deve mai affermare che le condizioni hanno "esplorazione identica": hanno **esplorazione esplicita identica**.

## 13. Proposta e promozione delle macro

Identiche in entrambe le varianti. Ogni `promotion_interval` episodi (default 25):

```python
def propose(buffer, lib, C, oracle=False):
    cands = []

    # 1. chunk: la dimensione di lotto più frequente non ancora in libreria
    counts = Counter(it.q for ep in recent(buffer) for it in ep.plan)
    for q, n in counts.most_common():
        if not any(m.q == q for m in lib.values()) and n >= MIN_SUPPORT:
            cands.append(Macro(f"lotto_{q}", q=q))
            break

    # 2. candidato strutturale: ≥ 2 chunk a q diverso → proponi lo schema
    fixed = [m for m in lib.values() if m.q is not None]
    if len(fixed) >= 2 and not any(m.q is None for m in lib.values()):
        cands.append(Macro("trasporta_lotto", q=None))

    # 3. oracle: rendi disponibile lo schema per decreto (condizione diagnostica)
    if oracle and not any(m.q is None for m in lib.values()):
        cands.append(Macro("trasporta_lotto", q=None))

    return cands
```

**Promozione**: `verify(cand)` superata **e** `ΔJ(cand) < 0` → entra in libreria.

**Verifica**: esecuzione della macro su configurazioni tenute da parte, confronto con l'espansione primitiva.

**Le promozioni sono irreversibili** nella condizione principale. È una condizione sperimentale, non una tesi sulla natura dei simboli; il controllo di reversibilità è in §18.

> **Da dichiarare nel paper**: questa è una regola di proposta mirata al dominio, non anti-unificazione generale. È onesto, e risparmia due giorni di implementazione che non aggiungerebbero nulla al risultato.

Nota che **la regola 2 rende testabile una delle ipotesi diagnostiche**: se l'agente bloccato non arriva mai ad avere due chunk a dimensione diversa, il candidato strutturale non si attiva mai. La frequenza di attivazione di quella regola è la misura che discrimina.

## 14. `ΔJ_remove` — distinguere autoconferma da inerzia

Se una macro non può essere rimossa, la sua permanenza non dimostra nulla: potrebbe restare semplicemente perché la rimozione è vietata.

Serve quindi una misura che risponda a: **il criterio di apprendimento vorrebbe ancora questa macro, dati i dati che essa stessa ha contribuito a generare?**

```python
def delta_J_remove(macro_name, lib, buffer, C):
    reduced = lib.without(macro_name)
    J_full = L_H(lib, C, FOLD) + sum(
        encoding_len(ep.plan, lib, C) for ep in buffer)
    J_red  = L_H(reduced, C, FOLD) + sum(
        encoding_len(reparse(ep.trace, reduced, C), reduced, C) for ep in buffer)
    return J_red - J_full          # > 0 → rimuoverla peggiorerebbe
```

> **Il punto sottile è `reparse`**: non si ri-pianifica. Si **ri-codifica la stessa traccia primitiva** con la libreria ridotta. La semantica è *dati i dati che ho, MDL vorrebbe questa macro?* — e per rispondere il comportamento va tenuto fisso.

Il reparse è un problema di copertura minima su una sequenza di lotti: greedy, poche righe.

| Osservazione | Interpretazione |
|---|---|
| `ΔJ_remove > 0` | **autoconferma vera**: la macro è ancora MDL-favorevole sui dati che ha indotto. Il sistema è a un punto fisso |
| `ΔJ_remove < 0` | **inerzia meccanica**: la persistenza è dovuta al divieto di rimozione, non alla convenienza |
| schema presente ma chunk dominante nell'uso | **proposer non-use** |

Questa misura è ciò che rende difendibile la parola *performativo*. Senza di essa sarebbe un'etichetta apposta a un fatto meccanico.

Va loggata a ogni intervallo di promozione, per ogni macro, in entrambe le varianti.

---

# Parte IV — Il disegno sperimentale

## 15. Le condizioni

### 15.1 Griglia ENUM (primaria)

```
B          ∈ {∞, 500, 200, 100, 50, 20, 10}        7 valori
ε          0.1 fisso
schedule   ∈ {poor_then_rich, rich, poor_forever, slow_drift}
k_poor     ∈ {50, 100, 200}                        solo per poor_then_rich
semi       10 per cella
```

### 15.2 Griglia LEARN (secondaria)

```
k_samples  ∈ {1, 3, 10, 30, 100}                   5 valori
retrain    ∈ {incremental, from_scratch}           2 valori
schedule   ∈ {poor_then_rich, rich}                2 valori
k_poor     100 fisso
semi       15 per cella
```

> Griglia più piccola, più semi. L'addestramento introduce varianza da inizializzazione e ordine dei batch: servono più ripetizioni per lo stesso potere statistico.

### 15.3 Le tre condizioni diagnostiche

Estratte dalle griglie, sono quelle che vanno nella tabella principale del paper.

| | ENUM | LEARN | schedule | Esito atteso |
|---|---|---|---|---|
| **A** — nessuna retroazione | `B = ∞` | `k = 100` | poor_then_rich | scopre lo schema dopo l'arrivo della varietà |
| **B** — retroazione forte | `B = 20` | `k = 1` | poor_then_rich | **bloccato** |
| **C** — esperienza ricca | `B = 20` | `k = 1` | rich | scopre lo schema |

**La logica del contrasto:**

- **A vs B** isola l'effetto della retroazione, a esperienza esterna ed esplorazione esplicita identiche
- **B vs C** isola l'effetto della povertà iniziale, a retroazione ed esplorazione identiche

Se entrambe le differenze sono nette:

> **La retroazione non causa il blocco. Lo rende irreversibile quando l'esperienza iniziale è povera.**

Nessuno dei due fattori da solo è sufficiente. È la formulazione precisa del risultato.

## 16. La diagnosi

Se il blocco esiste, può avere meccanismi distinti. Separarli è probabilmente il contributo più originale del lavoro, perché trasforma un risultato binario in una spiegazione.

### 16.1 I quattro meccanismi

| Meccanismo | Descrizione |
|---|---|
| **Evidence starvation** | il comportamento poco vario non genera mai gli esempi che innescherebbero il candidato → **lo schema non viene mai proposto** |
| **MDL rejection** | lo schema viene proposto, ma sui dati autoindotti `ΔJ` non è favorevole → **non viene promosso** |
| **Proposer non-use** | lo schema viene promosso, ma il proponente continua a raggiungere prima i piani basati sul chunk (§11.3) → **promosso e inutilizzato** |
| **Inerzia meccanica** | la macro resta solo perché la rimozione è vietata → **non è autoconferma** |

### 16.2 La condizione `oracle_proposal`

Per separare i primi tre: a ogni intervallo di promozione, `trasporta_lotto(o, q)` viene reso disponibile come candidato **indipendentemente da cosa il proponente avrebbe generato**. La valutazione MDL e la verifica restano invariate.

| Osservazione con oracolo | Meccanismo |
|---|---|
| Lo schema viene promosso e usato | il blocco era nella **generazione dei candidati** |
| Lo schema viene rifiutato da `ΔJ` | il blocco è nella **valutazione MDL sui dati indotti** |
| Promosso ma non usato nei piani | il blocco è nel **proponente** |

### 16.3 Una complicazione specifica di LEARN

In LEARN, "il candidato non è stato proposto" può significare *la rete non l'ha campionato*, che è una categoria a sé. Va distinta loggando le **distribuzioni campionate**, non solo il piano scelto.

## 17. Valutazione — protocollo congelato

```
TRAINING                            TEST
B / k_samples come da condizione    B_eval / k_eval fissi, uguali per tutti, FINITI
ε come da condizione                ε_eval = 0 (deterministico)
libreria aggiornata                 libreria congelata
proponente aggiornato               proponente congelato
ordini dallo schedule               test set fissato in anticipo
```

> **`B_eval` e `k_eval` devono essere finiti.** Con ricerca illimitata anche l'agente con `lotto_4` trova `6+5`: il gap collassa a zero per tutti, e si misurerebbe soltanto che ogni libreria contiene le primitive.

### 17.1 Tre quantità distinte

**(a) Costo di vita.** Costo fisico totale sostenuto durante l'apprendimento. Cosa l'agente ha realmente speso.

**(b) Generalità rappresentazionale.** Proprietà della libreria in sé, indipendenti dall'uso:
- presenza dello schema parametrico
- copertura dei valori di `q` rappresentati
- lunghezza MDL su un **corpus esterno bilanciato**, indipendente da ciò che l'agente ha generato

**(c) Prestazione operativa del sistema libreria–proponente.** Con proponente, parametri e test set identici per tutti:
- costo fisico totale
- **numero di viaggi** — la misura più leggibile
- regret su valori di `N` mai osservati in training
- transfer fuori dominio: `N ∈ [13, 30]`
- struttura del regret in funzione di `N`

> **Sul nome**: non "qualità della libreria". Una libreria contiene sempre le azioni primitive e non è quindi intrinsecamente incapace di produrre il piano ottimo — lo diventa **quando usata da un proponente a risorse limitate**. La metrica riguarda il sistema, non la libreria isolata.

### 17.2 Il gap performativo

```
gap = costo_fisico(sistema appreso, test set) − costo_fisico(ottimo, test set)
```

Nel vocabolario introdotto in §5: ciò che la condizione B trova è **performativamente stabile** — ottimo rispetto alla distribuzione che ha indotto — mentre lo schema è **performativamente ottimale**. Il gap è la distanza tra i due.

> **Il risultato centrale**: la libreria è stabile rispetto ai dati che ha contribuito a produrre, ma peggiore su una distribuzione di valutazione esterna e fissata in anticipo.

## 18. Controlli e ablazioni

- [ ] **Ordini identici verificati per hash** tra tutte le condizioni — se differiscono, l'esperimento è invalido
- [ ] **`ΔJ_remove`** loggato a ogni intervallo, per ogni macro, in entrambe le varianti
- [ ] **Condizione `oracle_proposal`** (§16.2)
- [ ] **ENUM contro LEARN**: il fenomeno compare in entrambi? Se sì, non dipende dal meccanismo
- [ ] **Ablazione dei due canali** (§12.5): `incremental` contro `from_scratch`
- [ ] **Controllo di reversibilità**: variante con promozioni revocabili. Se il fenomeno sparisce, l'irreversibilità è causale — ed è un risultato in sé
- [ ] **Ablazione del candidato strutturale**: senza la regola 2 di §13, qualcuno arriva allo schema?
- [ ] **Sensibilità a `ε`**: {0.05, 0.1, 0.2}
- [ ] **Sensibilità a `C`**: {4, 6, 8}
- [ ] **Sensibilità al `promotion_interval`**: {10, 25, 50}
- [ ] **Sensibilità alla codifica di `L(H)`**: due schemi alternativi, per verificare che il fenomeno non dipenda da una costante scelta
- [ ] **Capacità del modello LEARN**: hidden {32, 64, 128} — il fenomeno non deve dipendere dalla capacità

## 19. Logging

Una riga JSONL per episodio:

```json
{"t":142, "order":["bottiglia",11], "batch_sizes":[4,4,3],
 "phys_cost":83, "n_trips":3, "optimal_trips":2, "regret":1,
 "proposer":"enum", "nodes_expanded":20, "budget_truncated":true,
 "encoding_len":12.4, "lib":["lotto_4"], "L_H":31.2,
 "explored_random":false}
```

Per LEARN, in aggiunta: `sampled_partitions` (tutte, non solo la scelta), `model_entropy`, `train_loss`.

Una riga per intervallo di promozione:

```json
{"t":150,
 "proposed":["lotto_3","trasporta_lotto"],
 "rejected":[{"cand":"trasporta_lotto","reason":"delta_J","value":4.1}],
 "promoted":["lotto_3"],
 "delta_J_remove":{"lotto_4":8.3,"lotto_3":1.2},
 "structural_candidate_fired":true}
```

> **I candidati rifiutati sono metà del risultato.** Mostrare *cosa* il sistema ha considerato e scartato, e *perché*, è ciò che rende la scoperta ispezionabile.

Da questi log escono tutte le figure senza rieseguire nulla.

## 20. Figure

**F1 — Diagramma di fase.** Forza della retroazione sull'asse x (`B` per ENUM, `k_samples` per LEARN), `k_poor` sull'asse y, colore = probabilità di raggiungere lo schema, mediata sui semi. Due pannelli affiancati. **Figura principale.**

**F2 — Comportamento fisico.** Istogramma delle dimensioni di lotto scelte nelle condizioni A e B, **a parità di ordini esterni**. È la dimostrazione visiva non contestabile che il comportamento fisico è cambiato.

**F3 — Prestazione operativa.** Costo fisico sul test set congelato in funzione della retroazione, curve separate per schedule.

**F4 — Diagnosi.** Distribuzione delle run bloccate tra i quattro meccanismi.

**F5 — `ΔJ_remove` nel tempo.** Mostra se il chunk resta MDL-favorevole sui dati che ha indotto.

**F6 (solo LEARN) — Ablazione dei canali.** `incremental` contro `from_scratch`, a parità di tutto il resto.

---

# Parte V — Posizionamento e portata

## 21. Rapporto con la letteratura

| Lavoro | Relazione |
|---|---|
| **Machado, Barreto, Precup, Bowling (JMLR 2023)** — ciclo ROD | formalizzano il ciclo rappresentazione → astrazione → rappresentazione e lo dichiarano **virtuoso**; documentano anche un fallimento in regime online, attribuito al **sottocampionamento** delle option. Il nostro è **complementare**: l'astrazione è usata con successo, e proprio per questo si conferma |
| **Perdomo, Zrnic, Mendler-Dünner, Hardt (ICML 2020)** — performative prediction | stesso fenomeno in forma generale; parametri continui, punti fissi ben definiti. Qui: **simboli discreti, promozioni sticky, dipendenze tra macro** |
| **Nikishin et al. (ICML 2022)** — primacy bias | commitment prematuro nei pesi; la cura è il reset periodico |
| **Dohare, Sutton et al.** — loss of plasticity | meccanismo strutturalmente analogo: soluzioni a rango basso che restringono lo spazio delle soluzioni successive. Qui il restringimento avviene **nel vocabolario**, quindi è dicibile e ispezionabile |
| **Stitch (POPL 2023), DreamCoder (PLDI 2021)** | forniscono il meccanismo di compressione che usiamo; il loro passo MDL è **offline e one-shot** |
| Lavori recenti su certificati per librerie auto-evolutive | osservano che il passo MDL di Stitch è one-shot e che il loop di DreamCoder non ha garanzie di convergenza; propongono **una cura senza aver caratterizzato il fenomeno** |
| Bounded / resource-rational planning | il proponente a budget è nella loro tradizione; qui il vincolo di risorse interagisce con un vocabolario che evolve |

## 22. Il claim

> Il ciclo rappresentazione → astrazione → rappresentazione è stato formalizzato e assunto virtuoso. Mostriamo che quando la generazione dei piani è limitata da risorse — la ragione stessa per cui esiste la pianificazione gerarchica — il vocabolario appreso orienta la generazione, i piani generati producono comportamento, e il comportamento produce le tracce che confermano il vocabolario. Il fenomeno compare sia con un proponente enumerativo a budget sia con un proponente generativo addestrato sulle traiettorie passate. Caratterizziamo il regime, distinguiamo quattro meccanismi di blocco, e osserviamo che le tecniche di reset dei parametri non si trasferiscono direttamente a commitment simbolici con macro dipendenti.

**Da non affermare**, in nessuna forma:

- "nessuno ha guardato questo fenomeno" — falso e smontabile in una riga
- "reset e pruning non sono applicabili ai simboli" — le librerie simboliche si possono revisionare; il punto è che la revisione è costosa in presenza di dipendenze
- "le condizioni hanno esplorazione identica" — hanno esplorazione **esplicita** identica

## 23. Rilevanza per il workshop

Il tema (a) del workshop riguarda il **long-horizon planning**: apprendere, revisionare e verificare modelli d'azione simbolici. Il motivo conduttore dichiarato è l'**affidabilità**, con esplicito riferimento alle precondizioni allucinate e ai domain model fragili come problema di sicurezza.

Un'astrazione performativamente stabile è precisamente un modello d'azione che l'agente **continua a confermare perché ha smesso di generare l'esperienza che lo smentirebbe**. La verifica non lo intercetta: la macro è corretta su tutto ciò che l'agente esegue. È un **fallimento invisibile ai criteri di correttezza esistenti**.

C'è inoltre un collegamento diretto con i sistemi che operano oggi. Gli agenti basati su modelli linguistici che costruiscono librerie di skill riusabili eseguono esattamente questo ciclo, con un proponente generativo, senza criteri di giustificazione delle astrazioni e senza meccanismi di revisione. La variante LEARN mostra che in quel regime la retroazione è **più diretta**, non meno: il modello non ha alcun accesso ai piani che l'agente non ha mai eseguito.

## 24. Limiti

Da dichiarare esplicitamente nel paper, prima che lo faccia un revisore.

- **Dominio singolo e artificiale.** Il fenomeno è dimostrato in un ambiente costruito perché possa emergere. Non è evidenza che si manifesti nei sistemi reali, ma che *possa* manifestarsi sotto condizioni identificabili.
- **Una sola forma di astrazione.** Il dominio ammette solo la parametrizzazione della dimensione del lotto. Domini più ricchi hanno più dimensioni astraibili, e le interazioni tra di esse non sono studiate.
- **Regola di proposta mirata.** Non anti-unificazione generale: una regola scritta per questo dominio.
- **Il fold è fornito.** Il progettista che sceglie i primitivi compie metà del lavoro induttivo. Il fenomeno studiato è che il sistema, **potendo** parametrizzare, in certi regimi non lo fa.
- **Nessuna cura proposta.** Il lavoro caratterizza; non risolve.

## 25. Esiti possibili

| Esito | Pubblicabile? |
|---|---|
| Transizione netta, `ΔJ_remove > 0`, in **entrambe** le varianti | **sì** — risultato pieno |
| Transizione solo in ENUM | sì, dichiarando che dipende dal meccanismo |
| Transizione solo in LEARN | sì, e più interessante: il budget era un'approssimazione insufficiente |
| Degradazione graduale della prestazione operativa | sì, risultato più debole |
| Blocco con meccanismo identificato dalla diagnosi | **sì** — forse l'esito migliore |
| Solo inerzia meccanica (`ΔJ_remove < 0`) | **no** — è irreversibilità, non performatività |
| Metriche interne cattive nell'agente bloccato | **no** — è un fenomeno già documentato in letteratura |
| Nessun blocco in nessuna condizione | risultato negativo onesto, ma non automaticamente sufficiente per quattro pagine |
| Blocco anche senza retroazione | **no** — è curriculum bias |

---

# Parte VI — Realizzazione

## 26. Struttura del codice

```
src/
├── domain.py            ordini, partizioni, costo fisico, espansione primitiva
├── dsl.py               Macro, Plan, encoding_len, L_H
├── mdl.py               delta_J, delta_J_remove, reparse
├── propose.py           proposta chunk, candidato strutturale, oracle, verify
├── proposer_enum.py     ricerca a budget
├── proposer_learn.py    modello autoregressivo, training, sampling
├── loop.py              loop online, logging
└── experiment.py        griglia, verifica hash, analisi, figure
tests/
├── test_domain.py       l'ottimo è ⌈N/C⌉ lotti
├── test_mdl.py          monotonia del costo, reparse corretto
└── test_stream.py       determinismo e identità dei flussi
```

| Componente | Righe stimate | Giorni |
|---|---|---|
| domain + dsl + mdl | 300 | 2,5 |
| propose + verify | 120 | 1 |
| proposer_enum | 100 | 1 |
| loop + logging | 120 | 1,5 |
| griglia ENUM + figure | 150 | 2 |
| proposer_learn + training | 200 | 2,5 |
| griglia LEARN + ablazioni | 100 | 1,5 |

**Totale: ~1090 righe, 12 giorni** con la variante LEARN; **~890 righe, 9 giorni** senza.

## 27. Costo computazionale

**ENUM**: 500 episodi × 7 budget × 4 schedule × 3 valori di `k_poor` × 10 semi ≈ 300.000 episodi, ciascuno con una ricerca da al più 500 nodi. **Python puro, una o due ore.**

**LEARN**: 500 × 5 × 2 × 2 × 15 = 150.000 episodi **con training incrementale**. Reti minuscole, CPU sufficiente. **Stimare 3-6 ore.**

> Non ottimizzare nulla prima di sapere se il fenomeno esiste. La cosa peggiore che si possa fare in questa fase è rendere veloce un esperimento che potrebbe non servire.

## 28. Ordine di costruzione

L'ordine **non è negoziabile**.

```
1. domain + planner esaustivo          → assert: ottimo = ⌈N/C⌉ lotti
2. dsl + mdl + propose, OFFLINE        → GATE OFFLINE
3. loop online, B = ∞                  → deve riprodurre il comportamento offline
4. budget finito                       → GATE DEL PILOT
5. griglia ENUM completa + oracle + ablazioni
6. proposer_learn                      → solo DOPO il gate del pilot
7. griglia LEARN + ablazione dei canali
```

> **Perché LEARN va dopo.** Se si costruisce il proponente appreso prima del gate e il sistema non si blocca, **non si sa se il fenomeno non esiste o se il modello è addestrato male**. Con ENUM quell'ambiguità non esiste.

## 29. I due gate

### GATE OFFLINE

Su un corpus fisso e ricco, senza alcun loop: **il sistema arriva a `trasporta_lotto(o, q)`?**

> Se non ci arriva in condizioni ideali — dati vari, nessuna retroazione, nessun vincolo di ricerca — il problema è nel DSL o nella funzione di costo, **non nel fenomeno**. Fermarsi e risolvere prima di procedere.

### GATE DEL PILOT

Con retroazione forte e schedule povero, verificare tre cose:

1. **il sistema si blocca?**
2. **`ΔJ_remove > 0`?**
3. **le metriche interne sono buone mentre quelle esterne sono cattive?**

| Osservazione | Conseguenza |
|---|---|
| Non si blocca | non c'è paper in questa forma |
| `ΔJ_remove < 0` | è inerzia, non autoconferma |
| Anche le metriche interne sono cattive | è un fenomeno già documentato in letteratura, non questo |

> Se il gate non passa, **LEARN non si costruisce**.

## 30. Calendario

| Date | Fase | Uscita |
|---|---|---|
| 4–5 ago | domain + planner fisico | ottimo verificato |
| 6–7 ago | mdl + promozione offline | **GATE OFFLINE** |
| 8–10 ago | loop online, `B = ∞` | riproduce il comportamento offline |
| 11–14 ago | budget finito | **GATE DEL PILOT** |
| 15–19 ago | griglia ENUM, oracle, ablazioni | risultati primari |
| 20–23 ago | proposer_learn + griglia ridotta | conferma o smentita |
| 24–31 ago | analisi, figure, prima stesura | draft completo |
| 1–8 set | revisione, repository pubblico | pronto |
| **9 set** | **submission** | non il 10 |

## 31. Struttura del paper

Quattro pagine.

| Sezione | Spazio | Contenuto |
|---|---|---|
| **Introduzione** | 0,5 p | Il ciclo è formalizzato e assunto virtuoso. Chiediamo quando è vizioso |
| **Setup** | 0,75 p | Dominio, proponente a risorse limitate, MDL. Perché le partizioni sono fisicamente diverse |
| **Il fenomeno** | 1 p | A vs B vs C. Stessi ordini, comportamento diverso. **F2** |
| **Il meccanismo** | 1 p | Diagnosi a quattro vie, `ΔJ_remove`, ENUM vs LEARN. **F1** |
| **Limiti e portata** | 0,5 p | §24, più la predizione per sistemi con proponente generativo |
| Riferimenti | 0,25 p | |

**Due accorgimenti:**

- **Il titolo nomina il metodo, non il toy.** Non *A study of a warehouse domain* ma *The problem with online library learning*. Il dominio è lo strumento; il bersaglio è la classe di metodi.
- **Generalizzare oltre il caso studiato.** Arrivare esplicitamente a: *qualunque sistema che apprende astrazioni online e genera piani con risorse limitate*. Senza quel passo il lavoro resta un aneddoto.

**Dare un nome al dominio.** Rende il lavoro citabile e discutibile a voce.

## 32. Il primo passo

`domain.py` e il planner esaustivo. Verificare che l'ottimo fisico sia `⌈N/C⌉` lotti.

Poi `mdl.py` e la promozione offline su corpus ricco.

**Due giorni.** Se `trasporta_lotto(o, q)` emerge in condizioni ideali, l'esperimento ha una base su cui poggiare. Altrimenti si torna alla funzione di costo prima di scrivere qualunque altra cosa.
