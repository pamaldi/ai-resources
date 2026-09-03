# Note di lettura — *A Mathematical Framework for Transformer Circuits*

**Elhage, N., Nanda, N., Olsson, C., Henighan, T., Joseph, N., Mann, B., Askell, A., Bai, Y., Chen, A., Conerly, T., DasSarma, N., Drain, D., Ganguli, D., Hatfield-Dodds, Z., Hernandez, D., Jones, A., Kernion, J., Lovitt, L., Ndousse, K., Amodei, D., Brown, T., Clark, J., Kaplan, J., McCandlish, S. & Olah, C. (2021).** *A Mathematical Framework for Transformer Circuits*. Transformer Circuits Thread, Anthropic — 22 dicembre 2021.

https://transformer-circuits.pub/2021/framework/index.html

---

# 0. Perché leggere questo paper

È una delle voci più trasversali dell'archivio: compare nelle bibliografie su [composizionalità](../composizionalita-transformer/bibliografia.md), [content-drift](bibliografia-drift-mechint.md), [reasoning](../reasoning/bibliografia-ragionata.md) e [interpretability](bibliografia.md). Vedi anche [bibliografia trasversale §2](../../bibliografia-trasversale.md).

Il suo valore principale non è un singolo risultato sperimentale, ma il **vocabolario matematico e concettuale** che introduce o rende operativo:

- **residual stream** come canale di comunicazione;
- teste di attenzione come contributi **indipendenti e additivi**;
- distinzione fra circuito **QK** e circuito **OV**;
- **virtual weights**;
- **path expansion**;
- composizione fra teste tramite **Q-, K- e V-composition**;
- **induction heads** nei modelli a due layer.

> **Idea-guida:** invece di chiedere soltanto *«che cosa attiva questo neurone?»*, il paper prova a chiedere *«quale algoritmo end-to-end implementano questi pesi?»*.

## Limite fondamentale da ricordare dall'inizio

Il paper studia soprattutto **toy transformers decoder-only attention-only**: niente MLP, niente bias espliciti e LayerNorm trattata in modo semplificato. Gli esempi principali hanno **zero, uno o due layer**.

Questa è una semplificazione molto forte. Non significa che gli MLP non contino: significa esattamente il contrario. Gli autori li rimuovono perché sono più difficili da analizzare e perché, una volta fissati i pattern di attenzione, le teste diventano molto più trattabili con algebra lineare.

> **Quindi:** il paper fornisce un *framework* per capire circuiti transformer, non una spiegazione completa di un moderno LLM.

**Dove sono arrivato:** §—

---

# 1. Come usare queste note

Le note sono divise in quattro livelli, da non confondere:

- **[PAPER]** — ciò che il paper sostiene o formalizza;
- **[INTUIZIONE]** — modello mentale utile per capire;
- **[ESEMPIO]** — numeri inventati a scopo didattico;
- **[LIMITE]** — punto in cui l'intuizione smette di essere letterale.

Convenzioni personali:

- `?` = da chiarire;
- `!` = punto da riportare in bibliografia;
- `→` = collegamento ad altro materiale dell'archivio.

---

# 2. Prima di tutto: i numeri che useremo

Per capire il transformer senza perdersi nelle formule, userò quasi sempre **GPT-2 Small come esempio dimensionale**.

> **Attenzione:** GPT-2 Small serve qui solo per capire le dimensioni. Il paper di Elhage et al. studia soprattutto modelli *attention-only* molto più semplici.

I numeri da ricordare sono pochi:

| Simbolo | Valore di esempio | Significato |
|---|---:|---|
| `n_vocab` | **50 257** | numero di token possibili |
| `n_pos` | **5** nell'esempio | numero di token della frase corrente |
| `d_model` | **768** | dimensione del residual stream per ogni token |
| `n_head` | **12** | teste di attenzione per layer |
| `d_head` | **64** | dimensione interna di una testa |
| `d_mlp` | **3 072** | dimensione interna dell'MLP |

La relazione più utile è:

```text
12 teste × 64 dimensioni = 768 dimensioni
n_head      d_head          d_model
```

E la regola più importante di tutte è:

> **ogni componente può fare calcoli interni a 64 o 3072 dimensioni, ma ciò che viene risommato nel residual stream deve tornare a 768 dimensioni.**

## Convenzione delle dimensioni

In queste note userò vettori-riga.

```text
vettore [1×768]  @  matrice [768×64]  =  vettore [1×64]
```

Per cinque token contemporaneamente:

```text
matrice [5×768]  @  matrice [768×64]  =  matrice [5×64]
```

Il primo numero indica **quante posizioni/token** stiamo seguendo; il secondo indica **quanti numeri descrivono ciascuna posizione**.

---

# 3. Il transformer in una frase

Un transformer fa essenzialmente questo:

> **trasforma ogni token in un vettore, fa comunicare i token tramite l'attenzione, elabora l'informazione, ripete il processo e infine trasforma l'ultimo vettore in probabilità sul token successivo.**

Con la frase:

```text
"La capitale della Germania è"
```

abbiamo cinque token. Lo schema completo, senza ancora entrare nei dettagli, è:

```text
5 token
  │
  │ embedding
  ▼
H₀  [5×768]
  │
  ├──► ATTENZIONE 1 ──► contributo [5×768] ──► +
  │                                                 │
  ▼                                                 │
H₁  [5×768] ◄───────────────────────────────────────┘
  │
  ├──► MLP 1 ─────────► contributo [5×768] ──► +
  │                                                 │
  ▼                                                 │
H₂  [5×768] ◄───────────────────────────────────────┘
  │
  │           ... altri layer ...
  ▼
H_finale [5×768]
  │
  │ prendo solo l'ultima posizione
  ▼
h_ultimo [1×768]
  │
  │ unembedding W_U [768×50 257]
  ▼
logits [1×50 257]
  │
  │ softmax
  ▼
probabilità [1×50 257]
```

Questa è già quasi tutta l'architettura.

---

# 4. Passo 1 — dai token ai vettori

Il tokenizer converte il testo in token.

## 4A. Che cos'è davvero un token

Un token **non è una parola**. È un pezzo di testo scelto da un algoritmo, e i pezzi non coincidono con le unità linguistiche.

L'algoritmo si chiama **BPE** (*byte pair encoding*) e funziona così: si parte dai singoli caratteri e si fondono ripetutamente le coppie più frequenti nel corpus, finché non si raggiunge il numero di unità desiderato. Per GPT-2:

```text
50 000  unità trovate dall'algoritmo sul corpus
   256  una per ogni possibile byte (garantisce di poter scrivere qualsiasi cosa)
     1  il token speciale <|endoftext|>
───────
50 257  = n_vocab
```

Il risultato è che **le parole frequenti sono un token solo, quelle rare vengono spezzate**:

```text
"cane"          →  1 token
"Germania"      →  1 token
"anticostituzionalmente"  →  4-5 token
```

Tre conseguenze che spiegano comportamenti altrimenti misteriosi:

**Lo spazio fa parte del token.** `" cane"` (con spazio davanti) e `"cane"` sono **token diversi**, con id diversi e vettori diversi. È il motivo per cui il modo in cui spezzi un prompt cambia i risultati.

**Il modello non vede le lettere.** Riceve id di token, non caratteri. Chiedergli quante `r` ci sono in `"strawberry"` è chiedergli di riflettere su qualcosa che nella sua rappresentazione non esiste — deve ricostruire l'ortografia dal significato, non leggerla.

**I numeri vengono spezzati in modo arbitrario.** `"1234"` può diventare `"123"` + `"4"`, oppure `"12"` + `"34"`, a seconda di cosa era frequente nel corpus. Due numeri simili possono avere tokenizzazioni completamente diverse.

> → È esattamente il motivo per cui il dossier [composizionalità nei Transformer](../composizionalita-transformer/bibliografia.md) impone la **tokenizzazione per-cifra** negli esperimenti aritmetici: con la tokenizzazione di default non si può separare "il modello non sa fare l'addizione" da "il modello non riesce a vedere le cifre".

[LIMITE] Il vocabolario BPE viene costruito su un corpus prevalentemente inglese. Le altre lingue vengono spezzate più finemente: la stessa frase in italiano occupa più token che in inglese, e quindi costa di più e consuma più contesto.

[ESEMPIO]

```text
"La"  "capitale"  "della"  "Germania"  "è"
  │        │           │          │        │
  └────────┴───────────┴──────────┴────────┘
                 5 token
```

Ogni token viene usato per cercare una riga nella matrice degli embedding:

```text
W_E = tabella embedding [50 257 × 768]
```

Per un singolo token:

```text
token id
   │
   │ lookup in W_E [50 257×768]
   ▼
embedding [1×768]
```

Per cinque token:

```text
5 token
   │
   │ lookup
   ▼
H₀ [5×768]

        768 numeri per token
       ◄──────────────────►
      ┌────────────────────┐
tok 1 │                    │
      ├────────────────────┤
tok 2 │                    │
      ├────────────────────┤
tok 3 │       H₀           │   = [5×768]
      ├────────────────────┤
tok 4 │                    │
      ├────────────────────┤
tok 5 │                    │
      └────────────────────┘
       ▲
       │
   5 posizioni
```

[INTUIZIONE] Ogni riga è una **scheda di 768 numeri** associata a un token.

In un GPT-style, allo stato iniziale viene aggiunta anche informazione sulla posizione:

```text
token embedding     [5×768]
+
position embedding  [5×768]
=
H₀                  [5×768]
```

[PAPER] Nei toy model di Elhage et al. il meccanismo posizionale è gestito diversamente, quindi questo schema serve per capire un GPT-style generale, non va attribuito letteralmente ai modelli del paper.

## 4B. Perché serve l'informazione posizionale

Il punto non è ovvio e vale la pena fermarcisi: **l'attenzione, da sola, non ha alcuna nozione di ordine.**

Guarda cosa calcola una testa (§11):

```text
z = α₁·v₁ + α₂·v₂ + α₃·v₃ + ...
```

È una **somma**. E una somma non sa in che ordine sono arrivati gli addendi: `3 + 5` e `5 + 3` danno la stessa cosa. I pesi `α` a loro volta vengono da confronti `q · k`, che dipendono dal **contenuto** dei vettori, non da dove si trovano.

[ESEMPIO] Senza informazione posizionale, per il modello queste due frasi sarebbero composte dagli stessi identici vettori:

```text
"il gatto morde il cane"
"il cane morde il gatto"
```

Stessi token, stesso insieme, stesse `k` e stesse `v`. Il modello non avrebbe **nessun modo** di distinguerle — eppure significano il contrario.

Per questo la posizione va **iniettata dentro i vettori stessi**, prima che l'attenzione li veda:

```text
token embedding     [5×768]   "quale parola sono"
+
position embedding  [5×768]   "in che punto della frase mi trovo"
=
H₀                  [5×768]   "quale parola sono, e dove"
```

Da quel momento `"gatto"` in posizione 2 e `"gatto"` in posizione 5 sono **vettori diversi**, e query e key possono tenerne conto.

[INTUIZIONE] L'attenzione tratta la frase come un *insieme* di token. Il position embedding è ciò che lo trasforma in una *sequenza*.

[LIMITE] La maschera causale (§10) fornisce già un briciolo di informazione sull'ordine — la posizione 2 vede due token, la posizione 5 ne vede cinque — quindi il modello non è del tutto cieco all'ordine anche senza position embedding. Ma è un segnale debolissimo: non basta a distinguere le due frasi dell'esempio.

[NOTA] Esistono modi diversi di iniettare la posizione — embedding appresi (GPT-2), sinusoidi (paper originale), rotazioni delle query/key (RoPE, usato dai modelli recenti). Cambia il *come*, non il *perché*.

---

# 5. Il residual stream, spiegato semplicemente

Il **residual stream** non è un componente separato che “fa” qualcosa. È semplicemente il posto in cui vive lo stato corrente dei token.

Con cinque token:

```text
Residual stream = H [5×768]
```

Ogni componente:

1. legge `H`;
2. calcola un contributo della **stessa dimensione** `[5×768]`;
3. lo somma a `H`.

```text
H vecchio       [5×768]
+
contributo      [5×768]
=
H nuovo         [5×768]
```

Per una sola posizione:

```text
h vecchio       [1×768]
+
contributo      [1×768]
=
h nuovo         [1×768]
```

[ESEMPIO con soli 4 numeri invece di 768]

```text
h vecchio       [1×4] = [2.0, 0.0, 1.0, 0.0]
attenzione      [1×4] = [0.0, 1.5, 0.0, 0.0]
                         --------------------- +
h nuovo         [1×4] = [2.0, 1.5, 1.0, 0.0]
```

Quindi:

> **il residual stream cambia continuamente, ma cambia per somma.**

[INTUIZIONE] Immaginalo come un foglio condiviso: ogni componente legge ciò che c'è già e aggiunge qualcosa.

---

# 6. Le cinque posizioni: una riga per ogni token

Per la frase:

```text
posizione:      1           2          3           4          5
token:         "La"     "capitale"   "della"   "Germania"   "è"
```

lo stato del modello è:

```text
                 ogni riga = [1×768]

"La"          ───────────────────────────────┐
"capitale"    ───────────────────────────────┤
"della"       ───────────────────────────────┤  H = [5×768]
"Germania"    ───────────────────────────────┤
"è"           ───────────────────────────────┘
```

Gli MLP lavorano **riga per riga**. L'attenzione è ciò che permette alle righe di comunicare fra loro.

Una precisazione importante:

> non esistono cinque MLP con pesi diversi. È **lo stesso MLP** applicato a tutte e cinque le righe.

---

# 7. Passo 2 — l'attenzione: far comunicare i token

Questa è la parte più importante.

[INTUIZIONE]

La posizione finale `"è"` può chiedersi:

> «Quale parola precedente mi serve per capire cosa viene dopo?»

Una testa potrebbe dare molto peso a `"Germania"`:

```text
                         peso di attenzione
"La"          [1×768] ─────── 0.02 ─────┐
"capitale"    [1×768] ─────── 0.05 ─────┤
"della"       [1×768] ─────── 0.03 ─────┤
"Germania"    [1×768] ─────── 0.88 ─────┼──► informazione per "è"
"è"           [1×768] ─────── 0.02 ─────┘

pesi = [1×5]
```

Questi `0.02, 0.05, ...` sono **esempi inventati**. Non sono pesi permanenti del modello: vengono calcolati al volo per quella frase.

Per capire da dove arrivano dobbiamo introdurre Q, K e V.

---

# 8. Q, K e V senza complicazioni

Ogni testa legge il residual stream in tre modi diversi.

Per una singola posizione:

```text
h [1×768]
   │
   ├──► W_Q [768×64] ──► q [1×64]   = "che cosa cerco?"
   │
   ├──► W_K [768×64] ──► k [1×64]   = "per cosa sono rilevante?"
   │
   └──► W_V [768×64] ──► v [1×64]   = "che cosa consegno?"
```

Per tutti e cinque i token insieme:

```text
H [5×768]
   │
   ├──► W_Q [768×64] ──► Q [5×64]
   ├──► W_K [768×64] ──► K [5×64]
   └──► W_V [768×64] ──► V [5×64]
```

Quindi una testa comprime temporaneamente ogni token:

```text
768 dimensioni  ──►  64 dimensioni
    d_model             d_head
```

La distinzione più importante è:

- **Q + K decidono DOVE guardare**;
- **V contiene COSA prendere**.

[INTUIZIONE]

- Query = la ricerca che sto facendo.
- Key = l'etichetta con cui posso essere trovato.
- Value = il contenuto che consegno se vengo scelto.

---

# 9. Come Q e K producono i pesi di attenzione

Per capire dove deve guardare `"è"`, la sua query viene confrontata con le key delle posizioni che può vedere.

Per la posizione 5:

```text
q_5 [1×64]
   │
   ├── dot ── k_1 [1×64] ──► score 1 [1×1]
   ├── dot ── k_2 [1×64] ──► score 2 [1×1]
   ├── dot ── k_3 [1×64] ──► score 3 [1×1]
   ├── dot ── k_4 [1×64] ──► score 4 [1×1]
   └── dot ── k_5 [1×64] ──► score 5 [1×1]

insieme: scores_5 [1×5]
```

In forma matriciale, per tutte le posizioni contemporaneamente:

```text
Q [5×64]  @  Kᵀ [64×5]
          │
          ▼
scores [5×5]
```

Perché `[5×5]`?

```text
             key 1   key 2   key 3   key 4   key 5
query 1        •       ×       ×       ×       ×
query 2        •       •       ×       ×       ×
query 3        •       •       •       ×       ×
query 4        •       •       •       •       ×
query 5        •       •       •       •       •

             matrice scores [5×5]
```

Ogni riga risponde alla domanda:

> **questa posizione quanto deve guardare ciascuna delle cinque posizioni?**

[PAPER] Nella formula completa gli score vengono divisi per `√d_head` prima della softmax, per evitare che con `d_head` grande i prodotti scalari diventino troppo grandi e la softmax si saturi:

```text
score(i,j) = (q_i · k_j) / √d_head
```

Non cambia la struttura del ragionamento; qui lo ometto nei conti per leggibilità.

[NOTA] Il triangolo di `•` e `×` qui sopra non nasce dal prodotto `QKᵀ` — che di per sé riempirebbe tutta la matrice `[5×5]` — ma dalla **maschera causale**, introdotta nel §10.

---

# 10. La maschera causale

Il modello che predice il prossimo token non può guardare nel futuro.

Per cinque posizioni, la maschera ha dimensione:

```text
mask [5×5]
```

Schema:

```text
             posizione letta
              1  2  3  4  5
query 1       ✓  ×  ×  ×  ×
query 2       ✓  ✓  ×  ×  ×
query 3       ✓  ✓  ✓  ×  ×
query 4       ✓  ✓  ✓  ✓  ×
query 5       ✓  ✓  ✓  ✓  ✓

              [5×5]
```

Dopo la maschera si applica la softmax:

```text
scores [5×5]
   │
   │ mask causale [5×5]
   ▼
scores mascherati [5×5]
   │
   │ softmax riga per riga
   ▼
A = attention pattern [5×5]
```

Ogni riga di `A` contiene pesi non negativi che sommano a `1` sulle posizioni visibili.

---

# 11. Dai pesi ai value: cosa viene realmente trasportato

Ora abbiamo:

```text
A [5×5]    = dove guardare
V [5×64]   = cosa ogni posizione può consegnare
```

Il prodotto è:

```text
A [5×5]  @  V [5×64]
          │
          ▼
Z [5×64]
```

Quindi, per ogni posizione, la testa produce un nuovo vettore a 64 dimensioni.

Per la sola posizione 5:

```text
pesi_5 [1×5]
   @
V [5×64]
   =
z_5 [1×64]
```

[ESEMPIO]

Se i pesi fossero:

```text
[0.02, 0.05, 0.03, 0.88, 0.02]   [1×5]
```

allora:

```text
z_5 [1×64]
 = 0.02·v_1 + 0.05·v_2 + 0.03·v_3 + 0.88·v_4 + 0.02·v_5
```

Poiché `v_4` corrisponde a `"Germania"` e ha peso `0.88`, `z_5` sarà fortemente influenzato dal suo contenuto.

[INTUIZIONE] È questo il senso in cui l'attenzione **porta informazione da una posizione a un'altra**.

---

# 12. W_O: tornare da 64 a 768 dimensioni

Una testa non può sommare direttamente un vettore `[1×64]` al residual stream `[1×768]`.

Serve quindi `W_O`:

```text
z [1×64]
   │
   │ @ W_O [64×768]
   ▼
output testa [1×768]
```

Per tutte le posizioni:

```text
Z [5×64]
   │
   │ @ W_O [64×768]
   ▼
output testa [5×768]
```

Ora la somma è possibile:

```text
H               [5×768]
+
output testa    [5×768]
=
H aggiornato    [5×768]
```

Questa trasformazione completa è:

```text
H [5×768]
   │
   ├── Q [5×64]
   ├── K [5×64]
   └── V [5×64]
          │
QKᵀ ──► A [5×5]
          │
          │ A @ V
          ▼
        Z [5×64]
          │
          │ @ W_O [64×768]
          ▼
output testa [5×768]
          │
          │ + H [5×768]
          ▼
H nuovo [5×768]
```

---

# 13. Dodici teste: cosa succede nel layer

Con GPT-2 Small abbiamo 12 teste.

Ogni testa legge lo stesso residual stream `[5×768]`, ma ha matrici proprie e può cercare relazioni diverse.

```text
                         H [5×768]
                              │
       ┌──────────────┬───────┴───────┬──────────────┐
       ▼              ▼               ▼              ▼
   testa 1         testa 2          ...          testa 12
   d_head=64       d_head=64                     d_head=64
       │              │                               │
       ▼              ▼                               ▼
 out₁ [5×768]    out₂ [5×768]                  out₁₂ [5×768]
       │              │                               │
       └──────────────┴───────────┬───────────────────┘
                                  │ somma
                                  ▼
                       attention output [5×768]
                                  │
                                  │ + H [5×768]
                                  ▼
                         H_attn [5×768]
```

[PAPER] Questa vista “una `W_O` per testa e poi somma” è particolarmente utile per l'interpretabilità meccanicistica, perché rende ogni testa un contributo additivo separato.

[INTUIZIONE] Le teste sono come dodici lettori diversi dello stesso testo: ognuno cerca qualcosa di diverso e aggiunge il proprio contributo.

---

# 14. Passo 3 — l'MLP, spiegato semplicemente

> ⚠️ **Nota di terminologia, importante per leggere altro materiale.** Questo componente ha **due nomi** a seconda della tradizione:
>
> - **MLP** — usato da Elhage et al. e dalla letteratura di mechanistic interpretability;
> - **feedforward layer** / **FFN** — usato dai manuali e dalla maggior parte dei paper (es. Jurafsky & Martin, *Speech and Language Processing*, cap. 7).
>
> **Sono lo stesso oggetto.** In queste note uso "MLP" per coerenza con il paper.
>
> Allo stesso modo, l'attenzione viene talvolta chiamata **token-mixing**, perché è il componente che mescola informazione fra stream di token diversi.

Dopo l'attenzione, in un transformer standard arriva l'MLP.

L'MLP **non mette in comunicazione posizioni diverse**. Applica la stessa trasformazione a ogni riga del residual stream.

Per una posizione:

```text
h [1×768]
   │
   │ @ W_in [768×3072]
   ▼
x [1×3072]
   │
   │ GELU
   ▼
x' [1×3072]
   │
   │ @ W_out [3072×768]
   ▼
mlp_out [1×768]
   │
   │ + h [1×768]
   ▼
h nuovo [1×768]
```

Per cinque posizioni contemporaneamente:

```text
H [5×768]
   │
   │ @ W_in [768×3072]
   ▼
X [5×3072]
   │
   │ GELU
   ▼
X' [5×3072]
   │
   │ @ W_out [3072×768]
   ▼
MLP_out [5×768]
   │
   │ + H [5×768]
   ▼
H nuovo [5×768]
```

[INTUIZIONE]

> **Attenzione = raccoglie informazione anche dalle altre posizioni.**  
> **MLP = elabora ciò che ormai è presente dentro ciascuna posizione.**

Questa frase è volutamente semplice. L'MLP può quindi elaborare anche informazione su `"Germania"` presente nella posizione di `"è"`, purché l'attenzione l'abbia già portata lì.

[PAPER] Nei modelli principali del paper gli MLP vengono rimossi: gli autori studiano transformer **attention-only** proprio per rendere più trattabile l'analisi matematica dei circuiti.

---

# 14B. Perché più di un layer

Attenzione + MLP formano un **blocco**. GPT-2 Small ne impila 12. Ma se ogni blocco fa la stessa cosa, a che serve ripeterla?

## La risposta breve

> **Il layer 2 fa la stessa operazione, ma su un input diverso: legge un residual stream che contiene già quello che il layer 1 ci ha scritto.**

```text
layer 1  legge  H₀   ← solo token + posizione
layer 2  legge  H₁   ← token + posizione + TUTTO CIÒ CHE IL LAYER 1 HA AGGIUNTO
layer 3  legge  H₂   ← ...
```

E questo cambia tutto, perché `Q`, `K` e `V` del layer 2 sono calcolate a partire da `H₁`. Cioè: **dove il layer 2 decide di guardare può dipendere da cosa il layer 1 ha spostato.**

[PAPER] È questo il fenomeno che gli autori chiamano **composizione**, e che classificano in tre tipi (→ §5.1 del paper):

```text
Q-composition   il layer 1 influenza la QUERY del layer 2   → dove cerco
K-composition   il layer 1 influenza la KEY   del layer 2   → per cosa sono trovabile
V-composition   il layer 1 influenza il VALUE del layer 2   → cosa trasporto
```

## L'esempio che lo dimostra: le induction head

Questo è il risultato più noto del paper, ed è **la prova che due layer possono ciò che uno non può**.

Il compito: nel testo compare una sequenza, poi ricompare il suo inizio. Il modello deve continuare come la prima volta.

```text
...  [A] [B]  ...........  [A] →  ?
      ↑   ↑                 ↑
      │   └── dopo A veniva B
      │                     └── siamo di nuovo su A
      └── prima occorrenza

                       risposta attesa: B
```

Serve un meccanismo che dica: *«cerca un posto dove il token precedente era A, e copia ciò che c'era lì»*. Questo richiede **due passaggi in sequenza**:

```text
LAYER 1 — "previous-token head"

  Ogni posizione guarda la posizione PRECEDENTE e ne copia
  l'identità dentro di sé.

  posizione di [B]  ──►  ora contiene: "sono B, e prima di me c'era A"
                                                      ▲
                                        informazione che PRIMA non aveva


LAYER 2 — "induction head"

  La posizione finale [A] costruisce la query:
      "chi ha avuto A come token precedente?"

  Le key delle altre posizioni ora dicono "prima di me c'era X",
  perché il layer 1 ce l'ha scritto.

  → match sulla posizione di [B]
  → il circuito OV copia B nell'output
  → il logit di B sale
```

[PAPER] È **K-composition**: le *key* del layer 2 sono costruite su ciò che il layer 1 ha scritto nel residual stream.

## Perché un solo layer non ce la fa

In un modello a un layer, `Q` e `K` vengono calcolate direttamente da `H₀`, cioè da **token + posizione e nient'altro**.

```text
la posizione di [B] contiene solo: "sono B, sto in posizione 7"
```

Non contiene *«prima di me c'era A»*, perché **nessuno ha ancora spostato quell'informazione**. Non esiste una key su cui fare match, quindi il meccanismo è irrealizzabile — non "difficile da imparare": impossibile da rappresentare.

[PAPER] Ciò che un layer solo può fare sono gli **skip-trigrammi** (→ §4.3): *«se A è da qualche parte nel contesto e il token corrente è B, favorisci C»*. Il match è sull'**identità** di un token, mai su una relazione fra token.

> **La differenza in una riga:** un layer può cercare *un token*. Due layer possono cercare *un token che si trova in una certa relazione con un altro token*.

## Il principio generale

Ogni layer aggiunge **un passaggio sequenziale** di:

```text
sposta informazione  →  usa ciò che è stato spostato per decidere il prossimo spostamento
```

[ESEMPIO] Un compito a due stadi:

```text
"Maria ha comprato una casa a Roma. Lei ci abita da"
                                    ↑
     layer bassi:  "lei" → si riferisce a Maria
     layer alti:   usando "Maria", recupera ciò che serve su di lei
```

Il secondo passo **non può avvenire prima** del primo. La profondità è il numero di questi stadi che il modello può concatenare.

[LIMITE] Attenzione a non trasformarlo in una gerarchia pulita del tipo «layer 1 = sintassi, layer 6 = semantica, layer 12 = pragmatica». Non funziona così: le funzioni sono distribuite, i layer si sovrappongono, e lo stesso compito può essere risolto in punti diversi in modelli diversi. Il claim solido è **sequenzialità**, non specializzazione per livello.

[PAPER] La composizione può produrre trasformazioni che si comportano come teste che *non esistono* come modulo nella rete — le **virtual attention heads** (→ §5.7).

---

# 15. Dall'ultimo residual stream alla parola successiva

Dopo tutti i layer abbiamo ancora una matrice della stessa forma:

```text
H_finale [5×768]
```

Per predire il token successivo ci interessa l'ultima posizione:

```text
H_finale [5×768]
      │
      │ prendo la riga 5
      ▼
h_5 [1×768]
```

Poi arriva l'**unembedding**:

```text
h_5 [1×768]
   │
   │ @ W_U [768×50 257]
   ▼
logits [1×50 257]
```

C'è quindi un numero per ogni token del vocabolario.

```text
logits [1×50 257]
   │
   │ softmax
   ▼
probabilità [1×50 257]
```

[ESEMPIO concettuale]

```text
"Berlino"   → probabilità alta
"Roma"      → probabilità più bassa
"tavolo"    → probabilità molto bassa
...
```

## Lo schema completo con tutte le dimensioni

```text
TESTO
"La capitale della Germania è"
        │
        ▼
5 token
        │
        │ embedding W_E [50 257×768]
        ▼
H₀ [5×768]
        │
        │ ATTENZIONE
        │ Q = H W_Q → [5×64]
        │ K = H W_K → [5×64]
        │ V = H W_V → [5×64]
        │ QKᵀ        → [5×5]
        │ softmax    → A [5×5]
        │ A V        → Z [5×64]
        │ Z W_O      → [5×768]
        ▼
+ residual → H [5×768]
        │
        │ MLP
        │ W_in  [768×3072]
        │       → [5×3072]
        │ GELU  → [5×3072]
        │ W_out [3072×768]
        │       → [5×768]
        ▼
+ residual → H [5×768]
        │
        │ ... ripeti per i layer ...
        ▼
H_finale [5×768]
        │
        │ ultima riga
        ▼
h_finale [1×768]
        │
        │ W_U [768×50 257]
        ▼
logits [1×50 257]
        │
        │ softmax
        ▼
probabilità [1×50 257]
```

## In una riga

```text
TOKEN → [768] → ATTENZIONE [64→768] → MLP [3072→768] → ... → LOGITS [50 257]
```

Più precisamente, per una sequenza di 5 token:

```text
[5×768] → attenzione → [5×768] → MLP → [5×768] → ... → [1×50 257]
```

---

# 15D. Generare una frase: il ciclo autoregressivo

Fin qui abbiamo ottenuto **una** distribuzione di probabilità, per **un** token. Ma un modello scrive paragrafi. Come?

**Rifacendo tutto da capo, un token alla volta.**

```text
GIRO 1
  input:  "La capitale della Germania è"        5 token
  forward completo → probabilità [1×50 257]
  si sceglie un token                           → "Berlino"

GIRO 2
  input:  "La capitale della Germania è Berlino"   6 token
  forward completo → probabilità [1×50 257]
  si sceglie un token                              → "."

GIRO 3
  input:  "La capitale della Germania è Berlino."  7 token
  ...
```

Il token scelto viene **appeso all'input**, e il modello riparte da zero su una sequenza più lunga.

```text
        ┌──────────────────────────────┐
        │                              │
        ▼                              │
   [n token]                           │
        │                              │
   forward completo                    │
        │                              │
   logits ultima posizione             │
   [1×50 257]                          │
        │                              │
   softmax → campionamento             │
        │                              │
   nuovo token ──────────────────────► ┘
                                    appeso all'input
```

Tre conseguenze che spiegano molte cose del comportamento degli LLM:

- **Il modello non "pianifica" la frase.** Ogni token è una decisione locale, presa senza sapere come finirà. Quello che sembra un piano è il risultato del fatto che ogni scelta condiziona tutte le successive.
- **Il testo generato rientra come input.** Un errore al giro 3 diventa contesto — vero, per quanto riguarda il modello — al giro 4.
- **La matrice cresce.** `H` passa da `[5×768]` a `[6×768]` a `[7×768]`. Il contesto massimo `n_ctx` (1024 per GPT-2 Small) è il tetto oltre il quale non si può andare.

[NOTA] In pratica non si ricalcola davvero tutto: `K` e `V` delle posizioni già viste non cambiano e vengono riusate (**KV cache**). È un'ottimizzazione, non un cambio di semantica.

→ **Il passo «si sceglie un token»** — campionamento, temperatura, top-k, top-p, seed — è l'oggetto di [watermarking-llm-sampling.md](../fondamenti/watermarking-llm-sampling.md), che comincia esattamente dove questa sezione finisce.

---

# 15E. Da dove vengono i pesi: il training

Tutto il documento fin qui descrive un modello **già addestrato**. Ma `W_Q`, `W_K`, `W_V`, `W_O`, `W_in`, `W_out`, `W_E`, `W_U` sono, all'inizio, **numeri casuali**. Come diventano quelli giusti?

## L'obiettivo è uno solo

> **Dato un testo, predire il token successivo.**

Non c'è nient'altro. Nessuna etichetta scritta a mano, nessuna annotazione: il testo è insieme l'input e la risposta corretta, perché la risposta giusta al token `i` è semplicemente il token `i+1` che c'è già nel testo.

## Una frase da 5 token dà 5 esempi di training, non 1

Questo è il punto che spiega la maschera causale, e chiude un cerchio del §10.

In **inferenza** guardiamo solo l'ultima riga di `H_finale`. In **training** si usano *tutte* le righe:

```text
H_finale [5×768]  →  @ W_U  →  logits [5×50 257]

  riga 1  ("La")        deve predire  →  "capitale"
  riga 2  ("capitale")  deve predire  →  "della"
  riga 3  ("della")     deve predire  →  "Germania"
  riga 4  ("Germania")  deve predire  →  "è"
  riga 5  ("è")         deve predire  →  il token seguente
```

**Cinque predizioni da un solo forward pass.** Ed ecco perché la maschera causale esiste davvero: senza, la riga 2 vedrebbe la riga 3 e leggerebbe la risposta che deve indovinare. La maschera è ciò che rende possibile addestrare su tutte le posizioni **contemporaneamente** senza barare.

[INTUIZIONE] La maschera non serve a "non guardare il futuro" per ragioni filosofiche: serve a poter usare ogni posizione come esempio di training in parallelo.

## La loss

Per ogni posizione si confronta la distribuzione predetta con il token che c'era davvero:

```text
predizione riga 4:   "Berlino" 0.001 · "è" 0.6 · "sono" 0.2 · ...
token corretto:      "è"
```

La **cross-entropy** misura quanto il modello era sicuro della risposta giusta:

```text
loss = − log( probabilità assegnata al token corretto )
```

```text
p("è") = 0,6   →  loss = −log(0,6) = 0,51     buono
p("è") = 0,01  →  loss = −log(0,01) = 4,6     male
p("è") = 1,0   →  loss = 0                    perfetto
```

La loss totale è la media su tutte le posizioni e su tutte le frasi del batch.

## Il ciclo

```text
ripeti milioni di volte:

  1. FORWARD   prendi un batch di testo, calcola le attivazioni
               → loss (un solo numero)

  2. BACKWARD  calcola, per OGNI peso del modello, quanto ha
               contribuito a quella loss (il gradiente)

  3. UPDATE    sposta ogni peso di un pochino nella direzione
               che avrebbe ridotto la loss
```

[INTUIZIONE] Nessuno decide che `W_Q` della testa 7 debba cercare i nomi di paese. Emerge: quella configurazione riduce la loss, quindi il gradiente ce la spinge, milione di passi dopo milione di passi.

## Teacher forcing: training e inferenza non si comportano allo stesso modo

Un dettaglio che sembra tecnico ed è invece concettuale.

In **generazione** (§15D) il modello riceve in input **il proprio output**: sceglie un token, se lo riappende, riparte. Se sbaglia al giro 3, il giro 4 lavora sull'errore.

In **training** no: a ogni posizione il modello riceve sempre la **sequenza corretta**, non le proprie predizioni.

```text
posizione 4 predice "Berlino"  →  SBAGLIATO, doveva essere "è"
                                   │
                     la loss lo registra
                                   │
posizione 5 riceve comunque:  "La capitale della Germania è"
                              (la storia VERA, non quella predetta)
```

Si chiama **teacher forcing**. È ciò che rende possibile addestrare tutte le posizioni in parallelo: se ogni posizione dovesse aspettare la predizione della precedente, il training sarebbe sequenziale e impossibile su scala.

[LIMITE] Ne consegue che **il modello è addestrato in un regime diverso da quello in cui viene usato**. In training non vede mai i propri errori accumularsi; in generazione sì. È una delle spiegazioni proposte per la deriva dei testi lunghi.

## Come si misura: la perplessità

La metrica standard per valutare un modello linguistico è la **perplessità** (*perplexity*), ed è semplicemente:

```text
perplessità = e^(loss media di cross-entropy)
```

Cioè: l'esponenziale della loss. Più bassa, meglio è.

[INTUIZIONE] Si legge come «fra quante alternative equiprobabili il modello sta effettivamente esitando a ogni token». Perplessità 10 ≈ il modello è incerto come se scegliesse a caso fra 10 possibilità.

[LIMITE] Dipende dal tokenizer: due modelli con vocabolari diversi spezzano lo stesso testo in un numero diverso di token, quindi le loro perplessità **non sono confrontabili**. Ha senso solo fra modelli che condividono la tokenizzazione (→ §4A).

[LIMITE] Questo è il **pretraining**. I modelli con cui si parla hanno poi altre fasi (instruction tuning, RLHF) che non cambiano l'architettura ma cambiano molto il comportamento.

## Perché un obiettivo così banale produce comportamenti complessi

Vale la pena dirlo esplicitamente: «predici la parola dopo» sembra troppo poco per giustificare quello che gli LLM fanno.

Il punto è che **per predire bene bisogna aver capito molto**. Completare

```text
"La soluzione dell'equazione 3x + 6 = 12 è x = "
```

richiede di saper risolvere l'equazione. Completare un dialogo richiede di modellare chi parla. L'obiettivo è semplice; **il compito di raggiungerlo non lo è**.

[LIMITE] Questo però non autorizza a dire che il modello "capisce" nel senso in cui capisce una persona. È il punto su cui si separano le posizioni — → [reasoning, nucleo G](../reasoning/bibliografia-ragionata.md), in particolare **McCoy, R. T., et al. (2023/2024).** *Embers of Autoregression: Understanding Large Language Models Through the Problem They Are Trained to Solve*, che sostiene che la performance è predetta dalla probabilità del task sotto la distribuzione di training.

---

# 15A. QK e OV: la versione semplice che serve per il paper

Ora possiamo capire la distinzione del paper senza altra matematica.

Una testa svolge due lavori:

```text
1. QK = DOVE GUARDARE

Q [5×64] @ Kᵀ [64×5]
          ↓
     scores [5×5]
          ↓ softmax
       A [5×5]


2. OV = COSA PORTARE E SCRIVERE

V [5×64]
   │
   │ aggregazione con A [5×5]
   ▼
Z [5×64]
   │
   │ W_O [64×768]
   ▼
contributo [5×768]
```

Quindi:

> **QK sceglie le posizioni. OV determina il contenuto/effetto che viene scritto nel residual stream.**

Questo è uno dei concetti centrali di *A Mathematical Framework for Transformer Circuits*.

---

# 15B. LayerNorm: solo ciò che serve per non confondersi

In un transformer pre-LN, il componente non legge direttamente `H`: legge una versione normalizzata.

```text
H [5×768] ───────────────────────────────► + ──► H' [5×768]
     │                                     ▲
     │                                     │
     └──► LayerNorm [5×768]                │
               │                           │
               ▼                           │
          componente                       │
               │                           │
               └──► output [5×768] ───────┘
```

[INTUIZIONE] Il ramo principale del residual stream continua; il componente lavora su una copia normalizzata e poi aggiunge il proprio contributo.

[PAPER] La LayerNorm viene trattata in modo semplificato nell'analisi. Non serve entrare qui nei dettagli per capire QK, OV e path expansion.

---

# 15C. Pesi e attivazioni: non confonderli

Questa distinzione evita molte confusioni.

```text
PESI DEL MODELLO
W_Q [768×64]
W_K [768×64]
W_V [768×64]
W_O [64×768]
W_in [768×3072]
W_out [3072×768]
...

→ restano fissi durante un singolo forward pass
```

Invece:

```text
ATTIVAZIONI PER QUESTA FRASE
H [5×768]
Q [5×64]
K [5×64]
V [5×64]
A [5×5]
Z [5×64]
...

→ vengono calcolate al volo e cambiano se cambia la frase
```

Durante il training:

```text
FORWARD   → calcola le attivazioni con pesi fissi
BACKWARD  → calcola i gradienti
UPDATE    → modifica i pesi
```

[PAPER] Elhage et al. guardano soprattutto il modello già addestrato e chiedono: **che algoritmo implementano questi pesi?**

---

# 15F. Dove stanno davvero i 124 milioni di parametri

Utile per sapere quale parte del modello si sta guardando quando si guarda qualcosa.

**Per ogni blocco:**

```text
ATTENZIONE
  W_Q, W_K, W_V   3 × (768 × 768)  =  1 769 472
  W_O                 768 × 768    =    589 824
                                      ──────────
                                       2 359 296

MLP
  W_in            768 × 3072       =  2 359 296
  W_out           3072 × 768       =  2 359 296
                                      ──────────
                                       4 718 592

  totale blocco                    ≈  7 077 888
```

*(le 12 teste non aggiungono parametri: `12 × 64 = 768`, quindi le loro matrici affiancate formano esattamente una `768 × 768` — → §13.)*

**Il totale:**

| Parte | Parametri | Quota |
|---|---:|---:|
| Embedding token `W_E` [50 257×768] | 38,6 M | 31 % |
| Embedding posizionali [1024×768] | 0,8 M | 1 % |
| **Attenzione** (12 blocchi) | **28,3 M** | **23 %** |
| **MLP** (12 blocchi) | **56,6 M** | **46 %** |
| **Totale** | **≈ 124 M** | 100 % |

Tre cose che saltano all'occhio:

**Gli MLP sono il doppio dell'attenzione.** Quasi metà del modello è la parte che il paper di Elhage et al. **rimuove** (→ §17). Il framework è pulitissimo sul 23 %.

**La tabella degli embedding da sola è un terzo del modello.** E in GPT-2 non c'è una `W_U` separata: l'unembedding riusa `W_E` trasposta (*weight tying*). La stessa tabella serve sia a entrare che a uscire.

**I bias e le LayerNorm sono trascurabili** — poche migliaia di parametri per blocco, contro milioni. Ecco perché il paper può ometterli senza sensi di colpa.

---

# 15G. Cosa cambia con la scala

## Cosa resta identico

Tutto quello che hai letto fin qui. Embedding → blocchi (attenzione + MLP) che leggono e scrivono in un residual stream additivo → unembedding → softmax. **Un modello di frontiera e GPT-2 Small fanno la stessa identica sequenza di operazioni.**

## Cosa cresce

```text
                  anno   d_model  n_layer  n_head   d_mlp   n_vocab   n_ctx   parametri
GPT-2 Small       2019      768      12      12     3 072     50 K     1 K      124 M
GPT-2 XL          2019     1600      48      25     6 400     50 K     1 K      1,5 G
GPT-3             2020    12288      96      96    49 152     50 K     2 K      175 G
Llama 3.1 8B      2024     4096      32      32    14 336    128 K   128 K        8 G
Qwen3-0.6B        2025     1024      28      16     3 072    152 K    32 K      0,6 G
Qwen3-32B         2025     5120      64      64    25 600    152 K   128 K       32 G
Llama 3.1 405B    2024    16384     126     128    53 248    128 K   128 K      405 G
```

*(cifre dei modelli aperti da Jurafsky & Martin, cap. 7, fig. 7.24. **Le configurazioni dei modelli proprietari di frontiera non sono pubbliche.**)*

Quattro osservazioni che la tabella rende evidenti:

**`d_head` resta praticamente ferma.** 64 in GPT-2 Small, 128 in GPT-3, 128 in Llama 3.1 (sia 8B che 405B), 64–80 in Qwen3. Cresce il **numero** di teste, non la loro ampiezza: più punti di vista, non punti di vista più larghi.

**La profondità cresce meno della larghezza.** Da GPT-2 Small a Llama 405B: parametri ×3 000, larghezza ×21, profondità ×10. Il grosso è il prodotto fra le due, non una delle due.

**Il vocabolario è cresciuto.** 50 K per tutta l'era GPT-2/GPT-3, 128–152 K nei modelli recenti. Un vocabolario più grande spezza meno le lingue diverse dall'inglese (→ §4A) e accorcia le sequenze.

**Il contesto è esploso.** Da 1 K a 128 K token. Ed è il cambiamento più costoso: la matrice `scores` è `[n_pos × n_pos]`, quindi **il costo dell'attenzione cresce con il quadrato della lunghezza**. Passare da 1 K a 128 K token significa 16 000 volte il lavoro per layer — motivo per cui il contesto lungo ha richiesto tecniche dedicate e non solo hardware più grosso.

**E la regola `d_mlp = 4 × d_model` non vale più.** Qwen3-0.6B ha `3072 = 3 × 1024`, Llama 3.1 8B `14336 = 3,5 × 4096`. Nei modelli con MLP *gated* (SwiGLU) ci sono tre matrici invece di due, quindi si abbassa il moltiplicatore per non far esplodere i parametri.

## Cosa cambia davvero — la parte onesta

[LIMITE] «L'architettura è la stessa» è vero al livello dello schema, non alla lettera. I modelli recenti hanno sostituito diversi pezzi:

| Componente | GPT-2 (2019) | modelli recenti |
|---|---|---|
| posizione | embedding appresi, sommati a `H₀` | **RoPE** — rotazione applicata a `q` e `k` |
| non-linearità MLP | GELU | **SwiGLU** e varianti |
| normalizzazione | LayerNorm | **RMSNorm** |
| attenzione | tutte le teste con `K`,`V` proprie | **GQA** — teste che condividono `K`,`V` |
| densità | tutti i parametri attivi | **Mixture of Experts** — solo una parte attiva per token |

Nessuna di queste cambia la storia che hai letto: sono ottimizzazioni di efficienza e stabilità dentro lo stesso schema. Ma se apri il codice di un modello del 2026 aspettandoti GPT-2 alla lettera, non lo riconosci.

[LIMITE] E soprattutto: **non è cresciuta solo l'architettura, sono cresciuti i dati e le fasi di training.** Gran parte della differenza di comportamento fra GPT-2 e un modello attuale non sta nello schema qui descritto, ma in quanto testo ha visto e in cosa gli è stato fatto dopo il pretraining (→ §15E).

---

# 16. Il punto metodologico: congelare il pattern di attenzione

L'attenzione contiene una softmax, quindi è **non lineare rispetto all'input**.

Per questo non è corretto dire:

> «senza MLP, 12 layer equivalgono a uno».

Anche un attention-only transformer multilayer può implementare computazioni molto più ricche grazie alla softmax e alla composizione fra teste.

[PAPER] La path expansion diventa particolarmente trattabile quando si **fissano i pattern di attenzione**. A quel punto i coefficienti `A^h` vengono trattati come dati e il resto della computazione lungo i path è lineare.

Questa è la formulazione importante:

> **con attention pattern fissati, una testa è una trasformazione lineare; la composizione di tali trasformazioni può essere espansa in percorsi.**

Gli MLP complicano fortemente questa strategia perché introducono una non-linearità position-wise (per esempio GELU) dentro il percorso.

---

# 17. Limite MLP del paper

[PAPER] L'assenza degli MLP è una delle maggiori debolezze esplicitamente riconosciute dagli autori.

Per un GPT-2-like, l'MLP occupa una quota molto grande dei parametri di ogni blocco. Perciò il framework non può essere interpretato come una teoria completa della computazione dei transformer reali.

Sviluppi collegati:

- **Geva et al. (2021)** — *Transformer Feed-Forward Layers Are Key-Value Memories*;
- **Meng et al. (2022)** — *Locating and Editing Factual Associations in GPT*;
- **Elhage et al. (2022)** — *Toy Models of Superposition*;
- lavori successivi su feature e sparse autoencoders.

---

# 18. Mappa del paper — sezione per sezione

Da qui in poi le sezioni seguono la numerazione originale. La riga iniziale è un'**ancora di lettura**, non un riassunto esaustivo.

---

## 1. Summary of Results

[PAPER] Il quadro complessivo: residual stream come canale di comunicazione; teste additive; composizione fra teste; induction heads come caso importante nei modelli a due layer.

**Note:**


---

## 2. Transformer Overview

### 2.1 Model Simplifications

[PAPER] Modelli soprattutto **attention-only**; bias omessi; LayerNorm ignorata nella derivazione principale fino a fattori di scala variabili.

**Da ricordare:** “LayerNorm assorbibile” è una scorciatoia; la normalizzazione della varianza richiede una precisazione.

**Note:**


### 2.2 High-Level Architecture

[PAPER] Decoder-only autoregressivo: token embedding → blocchi residui → unembedding. Attenzione e MLP, nel modello generale, leggono e scrivono nel residual stream.

**Note:**


### 2.3 Virtual Weights and the Residual Stream as a Communication Channel

[PAPER] Poiché molte operazioni sono lineari, si possono comporre matrici adiacenti e ragionare su **pesi virtuali** end-to-end anziché sugli stati intermedi.

[INTUIZIONE] Se A scrive nello stream e B legge quello stesso sottospazio, si può studiare direttamente la trasformazione virtuale A→B.

**Note:**


### 2.4 Attention Heads are Independent and Additive

[PAPER] Le teste di uno stesso layer possono essere viste come contributi separati che vengono sommati nel residual stream.

Questa additività è ciò che consente di attribuire parti dell'output a teste e path distinti.

**Note:**


### 2.5 Attention Heads as Information Movement

[PAPER] Una testa può essere vista come un meccanismo che seleziona posizioni tramite QK e applica una trasformazione OV al contenuto trasportato.

[INTUIZIONE] “sposta informazione” è una buona riformulazione, purché si ricordi che il contenuto viene anche trasformato.

**Note:**


---

## 3. Zero-Layer Transformers

[PAPER] Senza layer di attenzione, il modello può essere letto come una trasformazione diretta token → logits. Questo espone una struttura tipo **bigramma** nelle matrici embedding/unembedding.

**Note:**


---

## 4. One-Layer Attention-Only Transformers

### 4.1 The Path Expansion Trick

[PAPER] Con pattern di attenzione trattati come fissati, i logits possono essere riscritti come somma di contributi lungo differenti percorsi computazionali.

[INTUIZIONE] Invece di seguire un unico vettore “mescolato”, si espande la somma e si chiede quali strade portano un'informazione dall'input ai logits.

**Note:**


### 4.2 Splitting Attention Head Terms into Query-Key and OV Circuits

[PAPER] Separazione fondamentale:

- **QK circuit** → determina *quali posizioni* vengono favorite;
- **OV circuit** → determina *che effetto* ha l'informazione trasportata sui logits / sul residual stream.

**Note:**


### 4.3 Interpretation as Skip-Trigrams

[PAPER] Nei modelli a un layer emergono strutture interpretabili come **skip-trigrammi** del tipo:

```text
A ... B → C
```

Una posizione `B` può cercare un token/context `A` e usare quell'informazione per favorire `C`.

**Note:**


### 4.4 Summarizing OV/QK Matrices

[PAPER] Le matrici virtuali QK e OV permettono di studiare direttamente la computazione end-to-end senza attribuire significato intrinseco ai singoli vettori intermedi `q`, `k`, `v`.

**Note:**


### 4.5 Do We “Fully Understand” One-Layer Models?

[PAPER] Gli autori sottolineano che nemmeno modelli molto piccoli sono completamente compresi. Il framework aumenta la leggibilità, non elimina l'ambiguità interpretativa.

**Note:**


---

## 5. Two-Layer Attention-Only Transformers

### 5.1 Three Kinds of Composition

[PAPER] Una testa del secondo layer può usare l'output di una testa precedente in tre modi concettualmente distinti:

- **Q-composition** — il primo head influenza la query del secondo;
- **K-composition** — influenza la key;
- **V-composition** — influenza il value / contenuto trasportato.

La composizione aumenta fortemente l'espressività rispetto a un singolo layer.

**Note:**


### 5.2 Path Expansion of Logits

[PAPER] La decomposizione dei logits viene estesa al caso a due layer, dove compaiono percorsi che attraversano più teste.

**Note:**


### 5.3 Path Expansion of Attention Scores — QK Circuit

[PAPER] Anche gli **attention score** del secondo layer possono essere espansi in termini dei contributi provenienti dal primo layer.

È qui che Q- e K-composition diventano centrali per capire pattern matching più sofisticato.

**Note:**


### 5.4 Analyzing a Two-Layer Model

[PAPER] Applicazione pratica della decomposizione a un modello a due layer: identificare quali teste e quali termini di composizione spiegano il comportamento osservato.

**Note:**


### 5.5 Induction Heads

[PAPER] Le **induction heads** sono il risultato più noto del lavoro.

Schema intuitivo:

```text
... A B ... A
            ↑
            trova un A precedente
              e usa il contesto precedente
              per favorire B come continuazione
```

Il meccanismo minimo richiede composizione fra teste e diventa disponibile nel modello a due layer studiato dagli autori.

[INTUIZIONE] È una forma di pattern completion in-context: “ho già visto questo prefisso; che cosa veniva dopo?”.

[LIMITE] Non va tradotto in “tutto l'in-context learning è induction heads”. Il paper propone un meccanismo importante e studiabile, non una spiegazione totale dell'ICL moderno.

**Note:**


### 5.6 Term Importance Analysis

[PAPER] Analisi quantitativa di quali termini/path della decomposizione contribuiscono maggiormente alla computazione.

**Note:**


### 5.7 Virtual Attention Heads

[PAPER] La composizione fra teste può produrre trasformazioni che si comportano come una sorta di **testa virtuale**, pur non corrispondendo a un singolo modulo esplicito della rete.

**Note:**


---

## 6. Where Does This Leave Us?

[PAPER] Il caso a due layer mostra quanto la composizione aumenti la ricchezza degli algoritmi implementabili e motiva l'ipotesi che strutture simili continuino a essere rilevanti in modelli più grandi.

**Note:**


---

## 7. Related Work

[PAPER] Collegamento con il programma dei **circuits** sviluppato in precedenza su reti vision (Distill) e con altri approcci al reverse engineering delle reti neurali.

**Note:**


---

# 19. Appendici — cose da ricordare

- notazione delle matrici;
- dettagli sui modelli addestrati;
- gestione della LayerNorm;
- matrici a basso rango;
- dettagli sulle positional embeddings;
- precisazioni sui circuiti QK/OV.

**Note:**


---

# 20. Cinque concetti da saper spiegare senza formule

## 1. Residual stream

È il canale condiviso in cui i componenti leggono e aggiungono informazione. La sua struttura additiva permette di decomporre il calcolo.

## 2. QK circuit

Decide **dove** una testa raccoglie informazione: come query e key determinano il pattern di attenzione.

## 3. OV circuit

Decide **che cosa succede** all'informazione selezionata: quale trasformazione viene scritta nel residual stream e, indirettamente, come cambiano i logits.

## 4. Path expansion

Riscrive la computazione come somma di percorsi end-to-end. È potente perché permette di chiedere quali strade sono realmente importanti.

## 5. Composition

Una testa successiva può usare ciò che una precedente ha scritto. Questo crea circuiti a più stadi e rende possibili meccanismi come le induction heads.

---

# 21. Errori concettuali da evitare

| Formulazione troppo forte | Formulazione migliore |
|---|---|
| “Il paper analizza GPT-2 Small” | Il paper usa toy transformer attention-only; GPT-2 Small è al massimo un riferimento architetturale |
| “h₀ contiene soltanto il token” | Dipende dal meccanismo posizionale; in GPT-2 contiene token + posizione, nel paper la posizione viene gestita diversamente |
| “Ci sono MLP diversi per ogni posizione” | È lo stesso MLP, applicato separatamente a ogni posizione |
| “L'attenzione fa solo copie” | Può approssimare una copia quando un peso domina, ma applica anche la trasformazione OV |
| “La lunghezza della frase sparisce” | L'output mantiene dimensione fissa e i pesi sono normalizzati; la distribuzione può comunque dipendere dal numero di posizioni |
| “La non-linearità sta solo nell'MLP” | Anche la softmax dell'attenzione è non lineare |
| “Senza MLP, 12 layer equivalgono a uno” | Falso in generale: teste di layer diversi possono comporsi e la softmax resta input-dependent |
| “LayerNorm è semplicemente assorbita nei pesi” | Quasi tutta la trasformazione può essere folded, ma resta uno scaling dipendente dall'attivazione |
| “Attenzione = spiegazione” | Il pattern mostra dove la testa pesa le posizioni; per l'effetto servono anche OV, path e interazioni |
| “Induction heads = tutto l'ICL” | Sono un meccanismo importante, non una teoria completa dell'in-context learning |

---

# 22. Domande aperte durante la lettura

*(Qui vanno le domande che il paper lascia realmente aperte, non soltanto i passaggi che devo ancora capire.)*

- ? Quanto del framework sopravvive quando si reintroducono MLP non lineari?
- ? Quanto sono stabili i circuiti identificati rispetto a distribuzioni/input diversi?
- ? Quando una decomposizione descrittiva diventa una spiegazione causale?
- ? Quali induction-like mechanisms persistono nei modelli moderni e su quali scale?
- ? In che misura i path individuali sono interpretabili quando il residual stream è in superposition?

---

# 23. Collegamenti all'archivio

- **Induction heads** → **Olsson, C., et al. (2022).** *In-Context Learning and Induction Heads*. Transformer Circuits Thread — seguito diretto, già in [reasoning](../reasoning/bibliografia-ragionata.md) I.1.
- **QK/OV come metodo** → **Wang, K. R., Variengien, A., Conmy, A., Shlegeris, B. & Steinhardt, J. (2023).** *Interpretability in the Wild: A Circuit for Indirect Object Identification in GPT-2 Small*. ICLR.
- **Limite attention-only / modelli grandi** → **Lindsey, J., et al. (2025).** *On the Biology of a Large Language Model*. Anthropic.
- **Causalità** → **Geiger, A., Lu, H., Icard, T. & Potts, C. (2021).** *Causal Abstractions of Neural Networks*. NeurIPS.
- **Residual stream e logit lens** → [watermarking e campionamento](../fondamenti/watermarking-llm-sampling.md) §1.
- **MLP come memoria / associazioni** → Geva et al. (2021); Meng et al. (2022).
- **Superposition** → Elhage et al. (2022), *Toy Models of Superposition*.

---

# 24. Riassunto finale in una pagina

Il paper propone di leggere i transformer come sistemi di **circuiti** costruiti da componenti che comunicano attraverso un **residual stream additivo**.

Una testa di attenzione può essere scomposta in due metà:

```text
QK: Q [5×64] @ Kᵀ [64×5] → pattern di attenzione [5×5]
OV: V [5×64] → aggregazione → Z [5×64] → W_O [64×768] → contributo [5×768]
```

Poiché gli output delle teste vengono sommati nello stream, è possibile decomporre la computazione in **path** diversi. Se il pattern di attenzione viene trattato come fissato, questi path diventano composizioni lineari di matrici e possono essere analizzati con algebra lineare.

Nei modelli a un layer questa struttura porta a pattern interpretabili come **skip-trigrammi**. Nei modelli a due layer, le teste possono comporsi tramite **Q-, K- o V-composition**, aumentando fortemente l'espressività. Un caso emblematico sono le **induction heads**, che riconoscono pattern ripetuti nel contesto e favoriscono la continuazione osservata in precedenza.

Il contributo più duraturo del paper non è l'idea che i transformer reali siano ormai “spiegati”, ma un modo di porre la domanda:

> **quali componenti comunicano, attraverso quali subspazi e percorsi, per implementare un comportamento osservabile?**

Il limite principale è altrettanto importante: l'analisi più pulita riguarda modelli **attention-only**. Reintrodurre MLP, LayerNorm completa, superposition e la scala dei modelli moderni rende il reverse engineering molto più difficile.

---

# 25. Glossario

*Per la rilettura fra mesi. Le dimensioni sono quelle di GPT-2 Small con una frase di 5 token.*

## Le grandezze

| Simbolo | Forma | Che cos'è |
|---|---|---|
| `n_vocab` | 50 257 | quanti token diversi esistono |
| `n_pos` | 5 | quanti token ha la frase corrente |
| `n_ctx` | 1 024 | massimo di token che il modello può leggere |
| `d_model` | 768 | larghezza del residual stream — quanti numeri per token |
| `n_layer` | 12 | quanti blocchi impilati |
| `n_head` | 12 | quante teste per layer |
| `d_head` | 64 | larghezza interna di una testa (`d_model / n_head`) |
| `d_mlp` | 3 072 | larghezza interna dell'MLP (`4 × d_model`) |

## Le matrici (pesi — fissi dopo il training)

| Simbolo | Forma | Che cosa fa |
|---|---|---|
| `W_E` | [50 257×768] | tabella: token id → vettore |
| `W_Q` | [768×64] | costruisce la **query**: «cosa cerco» |
| `W_K` | [768×64] | costruisce la **key**: «per cosa sono trovabile» |
| `W_V` | [768×64] | costruisce il **value**: «cosa consegno» |
| `W_O` | [64×768] | riporta il risultato della testa alla larghezza dello stream |
| `W_in` | [768×3072] | ingresso dell'MLP |
| `W_out` | [3072×768] | uscita dell'MLP |
| `W_U` | [768×50 257] | vettore finale → un punteggio per token (in GPT-2 è `W_E` trasposta) |

## Le attivazioni (calcolate al volo — cambiano a ogni frase)

| Simbolo | Forma | Che cos'è |
|---|---|---|
| `H` | [5×768] | il **residual stream**: una riga per token |
| `Q`, `K`, `V` | [5×64] | le tre proiezioni, una riga per posizione |
| `scores` | [5×5] | `Q @ Kᵀ` — quanto ogni query combacia con ogni key |
| `A` | [5×5] | il **pattern di attenzione**: scores mascherati + softmax, righe che sommano a 1 |
| `Z` | [5×64] | `A @ V` — il contenuto aggregato, prima di `W_O` |
| `logits` | [1×50 257] | punteggi grezzi sul vocabolario |

## I concetti

| Termine | Significato |
|---|---|
| **residual stream** | il canale condiviso in cui i componenti leggono e **sommano** (§5) |
| **testa di attenzione** | il meccanismo che fa comunicare posizioni diverse (§7–12) |
| **maschera causale** | impedisce a una posizione di leggere quelle successive; serve ad addestrare tutte le posizioni in parallelo (§10, §15E) |
| **MLP** | trasformazione applicata a ogni posizione separatamente, con gli stessi pesi (§14) |
| **circuito QK** | `W_Q` + `W_K` — decide **dove** guardare (§15A) |
| **circuito OV** | `W_V` + `W_O` — decide **cosa** viene scritto (§15A) |
| **composizione** | una testa usa ciò che una testa precedente ha scritto; Q-, K- o V- a seconda di cosa influenza (§14B) |
| **induction head** | il meccanismo a due layer che completa `... A B ... A → B` (§14B) |
| **skip-trigram** | ciò che un layer solo può fare: `A ... B → C`, match sull'identità di un token (§14B) |
| **path expansion** | riscrivere il calcolo come somma di percorsi, possibile se i pattern di attenzione sono congelati (§16) |
| **virtual weights** | comporre matrici adiacenti per studiare la trasformazione end-to-end senza gli stati intermedi |
| **superposition** | il modello rappresenta più caratteristiche di quante dimensioni abbia, in direzioni quasi ortogonali |
| **logit lens** | proiettare uno stato intermedio con `W_U` per vedere la predizione formarsi layer dopo layer |
| **ciclo autoregressivo** | campiona un token, appendilo all'input, rilancia tutto (§15D) |
| **BPE** | l'algoritmo che decide quali pezzi di testo sono token (§4A) |
| **teacher forcing** | in training il modello riceve sempre la sequenza corretta, non le proprie predizioni (§15E) |
| **perplessità** | `e^loss` — la metrica standard; confrontabile solo fra modelli con lo stesso tokenizer (§15E) |
| **KV cache** | riuso di `K` e `V` delle posizioni già calcolate, in generazione (§15D) |

## Sinonimi — per non perdersi leggendo altro materiale

Tradizioni diverse usano nomi diversi per gli stessi oggetti. Questa tabella è quella che serve passando da queste note a un manuale o a un paper.

| In queste note (Elhage et al.) | Altrove (Jurafsky & Martin, paper) |
|---|---|
| **MLP** | **feedforward layer**, **FFN** |
| attenzione | **self-attention**, **token-mixing** |
| `d_head` | `d_k` per query e key, `d_v` per i value (in pratica uguali, e `= d_model / n_head`) |
| `d_mlp` | `d_ff` |
| `n_pos` | `N` |
| `d_model` | `d` |
| `n_head` | `A` |
| `n_layer` | `L` |
| `W_U` | `U`, spesso `= Eᵀ` (weight tying) |
| `W_E` | `E` |
| unembedding + softmax | **language modeling head** |

[LIMITE] Una semplificazione che queste note fanno e i manuali no: qui `d_head = 64` vale per query, key **e** value. In generale sono due grandezze distinte, `d_k` e `d_v`, e `W_O` ha forma `[A·d_v × d]`. Poiché quasi sempre `d_k = d_v = d/A`, le due descrizioni coincidono — ma davanti a `W^O` di forma `[768×768]` invece di `[64×768]` conviene ricordare che è la vista "concatena le teste e poi proietta", equivalente a quella per-testa usata qui (→ §13).
