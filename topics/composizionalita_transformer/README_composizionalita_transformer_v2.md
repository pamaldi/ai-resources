# Composizionalità nei Transformer
## Dove finisce il riuso di primitive apprese e dove inizia la costruzione di un nuovo algoritmo?

## 1. Domanda di ricerca

I transformer generalizzano oltre gli esempi esatti osservati durante il training. La domanda di questo progetto non è quindi se generalizzino in assoluto, ma **quando primitive computazionali già apprese possano essere riutilizzate e organizzate in una procedura nuova**.

L'aritmetica decimale offre un banco di prova controllabile perché permette di separare con precisione:

- disponibilità delle primitive;
- recupero delle primitive nel contesto corretto;
- compatibilità delle rappresentazioni;
- routing dell'informazione;
- memoria temporanea dei risultati intermedi;
- accumulo posizionale;
- propagazione del riporto.

La domanda centrale è:

> **Se un transformer possiede già tutte le primitive necessarie per un algoritmo, riesce a combinarle spontaneamente quando incontra una nuova combinazione strutturale di quelle primitive?**

Il caso principale sarà:

\[
\text{addizione multi-cifra}
+
\text{sottrazione multi-cifra}
+
\text{moltiplicazione a una cifra}
\;\longrightarrow?\;
\text{moltiplicazione multi-cifra}
\]

Il progetto non mira a dimostrare che "i transformer sono" o "non sono" composizionali in senso globale. Mira a **localizzare la frontiera del riuso algoritmico**.

---

# 2. Perché il formato del task è una variabile sperimentale

Un transformer autoregressivo è addestrato a predire il token successivo.

Se durante il training il modello osservasse soltanto:

```text
7 * 8 = 56
4 * 9 = 36
```

ma non incontrasse mai una sequenza della forma:

```text
37 * 24 =
```

un eventuale fallimento potrebbe avere almeno due spiegazioni:

1. il modello non sa comporre le primitive necessarie;
2. il modello non ha generalizzato alla nuova **forma distribuzionale della richiesta**.

Questo confonderebbe composizionalità e format generalization.

Per evitare il problema, tutte le operazioni useranno un **formato unificato**.

Esempio:

```text
NUM OP NUM = NUM
```

con `OP` appartenente a:

```text
+
-
*
```

Il modello vedrà quindi durante il training:

```text
37 + 24 = 61
37 - 24 = 13
7 * 8 = 56
```

e al test:

```text
37 * 24 =
```

Il formato sintattico è già noto.

Il token `*` è già noto.

Il significato comportamentale di `*` è già appreso sui numeri a singola cifra.

La novità è la **combinazione tra operatore noto e operandi di lunghezza maggiore**.

Questa sarà la condizione principale.

---

# 3. Primitive richieste dalla moltiplicazione

Per:

\[
A=\sum_i a_i10^i
\]

e

\[
B=\sum_j b_j10^j
\]

la moltiplicazione posizionale richiede prodotti parziali:

\[
p_{ij}=a_i b_j
\]

che contribuiscono alla colonna:

\[
k=i+j
\]

L'accumulo locale può essere scritto come:

\[
s_k=\sum_{i+j=k}p_{ij}+r_{k-1}
\]

con:

\[
c_k=s_k\bmod 10
\]

e:

\[
r_k=\left\lfloor \frac{s_k}{10}\right\rfloor
\]

Il task richiede quindi almeno quattro componenti distinguibili.

### P1 — prodotti a singola cifra

\[
a_i b_j
\]

### P2 — routing posizionale

Associare ogni prodotto:

\[
p_{ij}
\]

alla colonna corretta:

\[
k=i+j
\]

### P3 — accumulo

Sommare un numero variabile di contributi nella stessa colonna.

### P4 — carry propagation

Trasferire correttamente il riporto tra colonne successive.

A queste va aggiunta una quinta componente, particolarmente importante alla luce di Bai et al.:

### P5 — cache e retrieval dei prodotti parziali

Il modello deve non soltanto calcolare un prodotto parziale, ma renderlo disponibile nel punto della computazione in cui verrà utilizzato.

Il problema può quindi richiedere una struttura interna di:

\[
\text{compute}
\rightarrow
\text{cache}
\rightarrow
\text{retrieve}
\rightarrow
\text{accumulate}
\]

Questa componente è distinta dal semplice routing posizionale.

---

# 4. Design sperimentale A/B/C

## Condizione A — Primitive incomplete

### Training

Formato unico:

```text
NUM OP NUM = NUM
```

Task osservati:

- addizione multi-cifra;
- sottrazione multi-cifra;
- nessuna moltiplicazione.

### Test

Moltiplicazione multi-cifra.

### Interpretazione

Questa condizione misura se il modello sviluppa spontaneamente anche una primitiva non richiesta dal training: la moltiplicazione tra singole cifre.

Un fallimento in A **non è evidenza sufficiente di fallimento compositivo**.

Può semplicemente mancare una primitiva.

---

## Condizione B — Primitive disponibili, combinazione strutturale nuova

Questa è la condizione principale.

### Training

Tutti gli esempi condividono lo stesso schema:

```text
NUM OP NUM = NUM
```

Il training contiene:

- addizione multi-cifra;
- sottrazione multi-cifra;
- tutte le moltiplicazioni tra singole cifre:

\[
0\text{–}9 \times 0\text{–}9
\]

Il modello vede quindi esempi come:

```text
38 + 47 = 85
91 - 36 = 55
7 * 8 = 56
```

ma **nessuna moltiplicazione multi-cifra**.

### Test

```text
23 * 14 =
317 * 42 =
281 * 537 =
```

### Cosa isola

Il modello conosce:

- il formato;
- il token `*`;
- il significato di `*`;
- la moltiplicazione tra singole cifre;
- la gestione di numeri multi-cifra;
- la somma;
- il carry.

Non ha mai osservato l'associazione:

\[
*\;+\;\text{operandi multi-cifra}
\]

Il test misura quindi una forma molto più pulita di **systematic recombination**.

Il contrasto rilevante è:

\[
\text{known operator}
+
\text{known long-number representation}
+
\text{known arithmetic primitives}
\]

contro:

\[
\text{new structural combination}
\]

---

## Condizione C — Scaffold compositivo

La Condizione C parte dalla B ma introduce un'inductive bias o un segnale intermedio.

Possibili varianti:

- supervisione dei prodotti parziali;
- target intermedi;
- running sums;
- decomposizione esplicita delle colonne;
- curriculum controllato;
- loss ausiliaria sulle rappresentazioni intermedie.

La domanda diventa:

> **Qual è il minimo scaffold necessario per trasformare primitive disponibili in una procedura integrata?**

Il confronto:

\[
A \rightarrow B \rightarrow C
\]

separa:

1. acquisizione della primitiva;
2. composizione spontanea;
3. composizione indotta da scaffolding.

---

# 5. Controllo supplementare: generalizzazione in lunghezza

Accanto alla Condizione B principale può essere eseguito un esperimento separato.

### Training

Includere alcune moltiplicazioni:

```text
23 * 4 = 92
17 * 3 = 51
```

### Test

```text
23 * 14 =
317 * 42 =
```

Questo esperimento è utile, ma deve essere interpretato separatamente.

Misura soprattutto:

> **la procedura appresa su moltiplicazioni corte generalizza a lunghezze maggiori?**

È quindi un test di **length/structural generalization**, non il test più puro di composizione da primitive isolate.

---

# 6. Ipotesi meccanicistiche

## H1 — Primitive multiplication retrieval failure

Il modello sa rispondere correttamente a:

```text
7 * 8 =
```

ma durante:

```text
347 * 52 =
```

non recupera internamente la quantità:

\[
7\times2
\]

nel layer, nella posizione o nel formato rappresentazionale richiesto.

### Test

- linear probing dei pairwise partial products;
- interventi causali sulle rappresentazioni candidate;
- confronto tra single-digit multiplication e multi-digit multiplication.

### Interpretazione prudente

Un probe lineare negativo non prova che l'informazione sia assente.

Indica soltanto che essa non è linearmente decodificabile:

- nei layer;
- nelle posizioni;
- nella rappresentazione analizzata.

---

## H2 — Cache DAG failure

Bai et al. mostrano che un modello capace di moltiplicazione può utilizzare l'attenzione per costruire una struttura diretta aciclica che permette di **cachare e recuperare pairwise partial products**.

Il modello della Condizione B potrebbe saper calcolare:

\[
a_i b_j
\]

ma non sapere costruire la struttura temporale necessaria per conservarlo e recuperarlo quando serve.

Questa ipotesi è distinta dal routing.

### Routing failure

Il modello non sa:

\[
(i,j)\rightarrow k
\]

### Cache failure

Il modello sa quale informazione sarebbe necessaria, ma non costruisce il percorso:

\[
\text{compute }p_{ij}
\rightarrow
\text{store}
\rightarrow
\text{retrieve at required timestep}
\]

### Test

- attention pattern analysis;
- path patching;
- causal tracing;
- identificazione delle dipendenze tra timestep;
- confronto con modelli che apprendono la moltiplicazione;
- ricerca di strutture DAG analoghe a quelle osservate nei modelli riusciti.

---

## H3 — Representation / type mismatch

I circuiti appresi per addizione e carry possono essere funzionalmente adatti ma ricevere input con una distribuzione differente.

L'addizione tipica presenta:

- due contributi principali per colonna;
- range specifici di valori intermedi;
- una particolare distribuzione del carry.

La moltiplicazione introduce:

- più contributi;
- prodotti parziali;
- somme intermedie più grandi;
- distribuzioni differenti.

Il circuito può quindi essere disponibile ma non attivarsi nel nuovo contesto.

### Test

Activation patching controllato tra:

- addizione;
- moltiplicazione;
- task sintetici con identici valori intermedi.

Se il patching recupera selettivamente la performance:

\[
\text{component available}
+
\text{interface mismatch}
\]

diventa una spiegazione plausibile.

---

## H4 — Routing / orchestration failure

Il modello può:

- calcolare i prodotti;
- mantenerli disponibili;
- possedere il carry;
- saper sommare;

ma non sapere orchestrare:

\[
(i,j)
\rightarrow
k=i+j
\rightarrow
\text{accumulation order}
\rightarrow
\text{carry}
\]

Il problema è quindi nella **procedura di coordinamento** tra primitive disponibili.

### Test

Costruire task intermedi che separino:

- scelta della coppia;
- posizione di destinazione;
- accumulo;
- ordine di elaborazione.

Interventi causali permetteranno di localizzare il primo passaggio che diverge dal comportamento corretto.

---

# 7. Complexity ladder

La performance sulla moltiplicazione verrà misurata aumentando gradualmente la complessità strutturale.

Esempio:

\[
300\times40
\]

\[
304\times40
\]

\[
304\times42
\]

\[
374\times52
\]

La difficoltà non verrà descritta soltanto attraverso il numero di cifre.

Verranno misurate variabili come:

\[
N_{\text{partial products}}
\]

\[
N_{\text{active digits}}
\]

\[
N_{\text{accumulations}}
\]

\[
D_{\text{carry}}
\]

\[
D_{\text{retrieval}}
\]

La performance potrà quindi essere modellata come:

\[
Accuracy =
f(
N_{\text{partial products}},
N_{\text{accumulations}},
D_{\text{carry}},
D_{\text{retrieval}}
)
\]

Lo scopo è individuare una **frontiera di complessità**, non soltanto un punto di fallimento.

---

# 8. Controlli additivi matched

Ogni livello della complexity ladder avrà un controllo additivo progettato per produrre una struttura di carry comparabile.

Questo controllo è necessario per distinguere:

\[
\text{failure of multiplication-specific composition}
\]

da:

\[
\text{generic carry failure}
\]

Per ogni classe di moltiplicazioni verranno quindi generati esempi di addizione matched rispetto ad almeno:

- profondità della catena di carry;
- numero di posizioni coinvolte;
- grandezza dei valori intermedi, quando possibile;
- lunghezza dell'output.

### Interpretazione

Se il modello fallisce nella moltiplicazione ma mantiene alta accuratezza nei controlli additivi matched:

> il carry da solo non spiega il fallimento.

Se invece la performance degrada in entrambi:

> il collo di bottiglia può essere una limitazione più generale nel trattamento delle dipendenze posizionali o del riporto.

Questo controllo evita di attribuire alla composizione un errore che appartiene invece a una primitiva già presente nel task sorgente.

---

# 9. Carry-chain holdout

L'addizione può essere utilizzata anche come test indipendente di generalizzazione strutturale.

### Training

Escludere esempi con:

\[
D_{\text{carry}}\geq3
\]

### Test

Valutare:

\[
D_{\text{carry}}=4,5,\dots
\]

Un successo costituisce forte evidenza comportamentale di generalizzazione lungo la struttura del carry.

Il claim diventa più forte se l'analisi causale mostra il riuso dello stesso meccanismo locale.

Il principio metodologico è:

\[
\text{behavioural OOD evidence}
+
\text{mechanistic reuse evidence}
\]

piuttosto che inferire composizionalità dalla sola accuratezza.

---

# 10. Catena causale da testare

Il task viene scomposto nella seguente pipeline:

\[
\boxed{
\text{Operator recognition}
\rightarrow
\text{Primitive retrieval}
\rightarrow
\text{Partial-product computation}
\rightarrow
\text{Cache}
\rightarrow
\text{Retrieval}
\rightarrow
\text{Positional routing}
\rightarrow
\text{Accumulation}
\rightarrow
\text{Carry}
\rightarrow
\text{Output}
}
\]

L'obiettivo è identificare:

> **il primo stadio causalmente necessario che differisce tra una computazione riuscita e una fallita.**

Un errore sul token finale, da solo, non localizza la causa.

---

# 11. Analisi meccanicistica

La piccola scala del modello permette un'analisi relativamente completa tramite:

- linear probing;
- activation patching;
- path patching;
- attention ablation;
- head ablation;
- MLP ablation;
- causal tracing;
- analisi del residual stream;
- confronto tra circuiti di `+`, `-` e `*`.

Per ogni componente candidato:

1. localizzare l'informazione;
2. verificarne la decodificabilità;
3. misurarne il contributo;
4. intervenire causalmente;
5. verificare il riuso tra task.

La distinzione importante è:

\[
\text{representation}
\neq
\text{causal use}
\neq
\text{cross-task reuse}
\]

---

# 12. Perché modelli piccoli

Un transformer nell'ordine di circa 1–10M di parametri consente:

- training controllato;
- dataset sintetici esaustivi;
- molte repliche con seed differenti;
- patching sistematico;
- ablazioni estese;
- analisi dettagliata delle attention head.

La scelta della piccola scala non implica che il meccanismo trovato debba trasferirsi direttamente ai frontier model.

Modelli più grandi possono sviluppare:

- rappresentazioni differenti;
- circuiti più distribuiti;
- strategie ibride;
- maggiore modularità;
- forme di astrazione assenti nei modelli piccoli.

Il risultato appropriato sarà quindi:

> **una caratterizzazione causale della composizione in un laboratorio transformer controllato.**

L'estensione alla scala sarà una domanda successiva, non una conclusione automatica.

---

# 13. Predizioni distinguibili

## Scenario A — Fallisce già il retrieval

Il modello conosce `7*8` isolatamente, ma l'informazione non viene recuperata nella moltiplicazione multi-cifra.

**Collo di bottiglia candidato:** context-dependent primitive retrieval.

---

## Scenario B — Partial products presenti, cache assente

I prodotti parziali sono rappresentati, ma non emerge una struttura efficace di cache/retrieval.

**Collo di bottiglia candidato:** long-range memory organization.

---

## Scenario C — Cache presente, routing errato

I prodotti vengono mantenuti, ma raggiungono colonne o timestep errati.

**Collo di bottiglia candidato:** orchestration/routing.

---

## Scenario D — Routing corretto, accumulo fallisce

Le quantità giuste arrivano nella posizione giusta, ma il modello non implementa l'accumulo variabile.

**Collo di bottiglia candidato:** composition over variable arity.

---

## Scenario E — Accumulo corretto, carry fallisce

I valori intermedi sono corretti ma il risultato finale degrada con la profondità del carry.

I controlli additivi matched stabiliranno se il problema è multiplication-specific o generale.

---

## Scenario F — B fallisce, C riesce

Le primitive sono disponibili ma serve un inductive bias.

**Domanda quantitativa:** quanto scaffold è sufficiente?

---

## Scenario G — B riesce

Il modello generalizza spontaneamente da:

\[
\text{single-digit } *
\]

a:

\[
\text{multi-digit } *
\]

senza esempi diretti della combinazione.

L'analisi meccanicistica dovrà allora determinare **quali circuiti vengono riusati e quali vengono costruiti ex novo**.

---

# 14. Metriche principali

Oltre all'exact-match accuracy:

### Behavioral

- accuracy per lunghezza;
- accuracy per numero di prodotti parziali;
- accuracy per carry depth;
- accuracy per retrieval depth;
- accuracy per sparsità degli operandi;
- error taxonomy per cifra/posizione.

### Mechanistic

- probe accuracy;
- causal effect delle ablazioni;
- patching recovery;
- circuit overlap tra task;
- attention-path similarity;
- presenza/assenza di strutture cache/retrieval;
- layer di prima divergenza tra esempi riusciti e falliti.

---

# 15. Controlli metodologici

Per evitare conclusioni fragili:

- più seed;
- più dimensioni del modello;
- dataset bilanciati;
- controllo delle frequenze dei token/operatori;
- stesso formato per tutti i task;
- separazione rigorosa tra training e test strutturale;
- controlli additivi matched;
- confronto tra probe e interventi causali;
- analisi degli errori per complessità, non soltanto accuracy aggregata.

---

# 16. Relazione con lavori precedenti

## Quirke, Neo & Barez

I loro studi su piccoli transformer aritmetici mostrano che modelli autoregressivi possono apprendere circuiti interpretabili per addizione, sottrazione e training mixed.

Questi risultati forniscono:

- un precedente metodologico;
- candidate primitive;
- strumenti di analisi circuitale.

Il presente progetto cambia domanda:

> **una primitiva appresa in un task viene riutilizzata quando compare in una combinazione strutturale nuova?**

---

## Bai et al.

Il lavoro sulla moltiplicazione identifica un meccanismo nel quale l'attenzione costruisce una struttura diretta aciclica per **cachare e recuperare pairwise partial products**.

Questo motiva direttamente H2.

Il loro risultato sull'uso di un segnale ausiliario relativo ai running sums motiva inoltre una variante della Condizione C:

> un inductive bias sulle variabili intermedie può rendere apprendibile una struttura che il training standard non scopre facilmente.

---

## Lindsey et al.

L'analisi di Claude 3.5 Haiku mostra che un modello grande può utilizzare strategie aritmetiche differenti e più ibride rispetto ai piccoli transformer specializzati.

Per questo il progetto non assume:

\[
\text{small-model circuit}
=
\text{frontier-model circuit}
\]

La scala piccola viene utilizzata per ottenere **identificabilità causale**, non per rivendicare universalità del meccanismo.

---

# 17. Deliverable

Il risultato atteso non è:

```text
Transformer compositional: yes/no
```

ma una mappa causale della frontiera:

\[
\text{primitive availability}
\rightarrow
\text{retrieval}
\rightarrow
\text{cache}
\rightarrow
\text{routing}
\rightarrow
\text{accumulation}
\rightarrow
\text{carry}
\]

con l'identificazione del primo passaggio che impedisce — oppure permette — il riuso algoritmico.

Il contributo sarà quindi una risposta sperimentale alla domanda:

> **Quali condizioni trasformano primitive computazionali apprese in componenti riutilizzabili di una procedura nuova?**

---

# 18. Esperimento minimo iniziale

Per evitare di partire con un progetto troppo ampio, la prima versione può essere ridotta a:

### Modello

- decoder-only transformer;
- 2–3 layer;
- 2–4 attention head;
- circa 1–10M parametri.

### Training B

Formato:

```text
NUM OP NUM = NUM
```

Dataset:

- `+` multi-cifra;
- `-` multi-cifra;
- `*` soltanto 1×1 cifra.

### Test

- `*` 2×2;
- `*` 3×2;
- sparse vs dense operands;
- carry basso vs alto.

### Controlli

- addizioni matched per carry;
- più seed.

### Prima analisi

1. accuracy;
2. errori per posizione;
3. probe dei partial products;
4. attention analysis per cache/retrieval;
5. activation patching sulle componenti candidate.

Solo dopo questo primo esperimento conviene introdurre:

- Condizione A;
- Condizione C;
- curriculum;
- loss ausiliarie;
- ablation complete;
- scaling study.

Questo mantiene il progetto falsificabile e realizzabile senza perdere la domanda centrale.

---

# Riferimenti essenziali

- Quirke, P., Neo, C., & Barez, F. (2024). **Arithmetic in Transformers Explained**. arXiv:2402.02619.
- Bai, X., Pres, I., Deng, Y., Tan, C., Shieber, S., Viégas, F., Wattenberg, M., & Lee, A. (2025). **Why Can't Transformers Learn Multiplication? Reverse-Engineering Reveals Long-Range Dependency Pitfalls**. arXiv:2510.00184.
- Lindsey, J. et al. (2025). **On the Biology of a Large Language Model**. Transformer Circuits Thread / Anthropic.
