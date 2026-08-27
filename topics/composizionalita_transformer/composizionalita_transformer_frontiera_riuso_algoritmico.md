# Composizionalità nei Transformer: caratterizzare la frontiera del riuso algoritmico

## Il problema

I large language model generalizzano. Questo è un fatto empirico: producono output sensati su input mai osservati esattamente durante il training e mostrano capacità di trasferimento, analogia e generalizzazione fuori distribuzione in numerosi domini. La domanda interessante non è quindi semplicemente *se* generalizzano, ma **quale tipo di generalizzazione realizzano, attraverso quali rappresentazioni e fino a quale distanza strutturale dal training**.

Una parte crescente della letteratura sulla mechanistic interpretability suggerisce che nei transformer molte variabili semanticamente o funzionalmente rilevanti siano rappresentate in modo strutturato nel residual stream e possano, in alcuni casi, essere decodificate linearmente e collegate causalmente al comportamento del modello. Questo rende plausibile parlare, con la dovuta cautela, di **primitive rappresentazionali o computazionali apprese**.

Ma il possesso di primitive individuali non implica automaticamente la capacità di **riutilizzarle e combinarle per costruire un algoritmo nuovo**.

Un essere umano che conosce:

- la somma;
- il valore posizionale delle cifre;
- i prodotti tra singole cifre;
- la propagazione del riporto;

possiede, almeno in linea di principio, tutti gli ingredienti necessari per eseguire una moltiplicazione multi-cifra con l'algoritmo posizionale.

La domanda centrale di questo progetto è quindi:

> **Quando primitive computazionali già apprese diventano componenti riutilizzabili di un algoritmo mai mostrato direttamente durante il training?**

Più concretamente:

\[
\text{Addition}
+
\text{Subtraction}
+
\text{Single-digit multiplication}
\;\longrightarrow?\;
\text{Multi-digit multiplication}
\]

L'obiettivo non è stabilire se "i transformer sono composizionali" in senso assoluto, ma **caratterizzare sperimentalmente e meccanicisticamente la frontiera tra riuso riuscito e fallimento compositivo**.

---

## Perché la domanda è difficile

I transformer mostrano numerosi comportamenti che possono apparire composizionali. Un modello può:

- combinare fatti appresi separatamente;
- applicare strutture sintattiche a vocaboli nuovi;
- trasferire schemi a configurazioni non osservate;
- generalizzare lungo alcune dimensioni del problema.

Tuttavia, il successo su un esempio nuovo non permette da solo di distinguere tra:

1. **interpolazione in uno spazio rappresentazionale ben strutturato**;
2. **riuso di primitive apprese**;
3. **composizione sistematica di primitive secondo una struttura computazionale nuova**.

Una possibile spiegazione di parte della generalizzazione apparentemente composizionale è infatti che il caso di test cada in una regione delle rappresentazioni sufficientemente ben coperta dal training da non richiedere la costruzione di una procedura realmente nuova.

Per distinguere queste possibilità servono split sperimentali nei quali il caso di test sia nuovo **non solo a livello di input**, ma rispetto a una proprietà strutturale controllata.

### Carry-chain holdout

L'addizione multi-cifra fornisce un primo test.

La catena di riporto introduce una dipendenza locale:

\[
r_k = f(a_k,b_k,r_{k-1})
\]

dove il riporto a una posizione dipende dal risultato della posizione precedente.

Il training set può essere costruito eliminando sistematicamente tutti gli esempi con catene di riporto di lunghezza maggiore o uguale a 3.

Il test può poi contenere catene di lunghezza 4, 5 o superiore.

Se il modello generalizza correttamente, questo costituisce **forte evidenza comportamentale di generalizzazione composizionale lungo la struttura del carry**.

Il claim diventa ancora più forte se l'analisi meccanicistica mostra che lo stesso circuito responsabile della gestione locale del riporto viene riutilizzato nelle catene più lunghe.

In questo modo:

\[
\text{behavioural evidence}
+
\text{circuit evidence}
\]

permettono di distinguere una generalizzazione strutturale da un semplice successo su input nuovi.

---

## Il banco di prova principale: aritmetica decimale

L'aritmetica è particolarmente adatta allo studio della composizionalità perché possiede:

- primitive discrete;
- algoritmi noti;
- dipendenze locali esplicite;
- output esattamente verificabili;
- distribuzioni sintetiche completamente controllabili.

La moltiplicazione multi-cifra è particolarmente interessante perché può essere scomposta in primitive più semplici.

Per due numeri:

\[
A = \sum_i a_i10^i
\]

e

\[
B = \sum_j b_j10^j
\]

la moltiplicazione posizionale richiede la costruzione dei prodotti parziali:

\[
p_{ij} = a_i b_j
\]

e il loro accumulo nelle corrette posizioni:

\[
s_k = \sum_{i+j=k} p_{ij} + r_{k-1}
\]

da cui:

\[
c_k = s_k \bmod 10
\]

e

\[
r_k = \left\lfloor \frac{s_k}{10} \right\rfloor
\]

La moltiplicazione richiede quindi almeno tre classi di capacità.

### 1. Prodotti parziali a singola cifra

\[
a_i \cdot b_j
\]

Questa capacità non è richiesta dall'addizione e dalla sottrazione.

Per evitare di confondere **assenza di una primitiva** con **fallimento della composizione**, la condizione sperimentale principale fornirà esplicitamente al modello tutte le moltiplicazioni tra singole cifre durante il training.

Il modello vedrà quindi esempi del tipo:

\[
7\times8=56
\]

\[
4\times9=36
\]

ma **nessuna moltiplicazione tra numeri multi-cifra**.

---

### 2. Accumulo posizionale

I prodotti parziali con lo stesso indice:

\[
i+j=k
\]

devono essere sommati nella stessa posizione di output.

Questo passaggio presenta analogie con i meccanismi di somma posizionale appresi durante l'addizione, ma introduce una differenza importante: il numero di contributi può essere variabile.

Il problema diventa quindi:

> un meccanismo appreso per sommare due contributi posizionali può essere riutilizzato per accumulare un insieme variabile di prodotti parziali?

---

### 3. Propagazione del riporto

La propagazione del riporto è già necessaria per l'addizione multi-cifra.

Il progetto può quindi chiedere se il circuito appreso in quel contesto venga riutilizzato quando il valore da propagare nasce dall'accumulo di prodotti parziali.

Questa è una forma particolarmente chiara di **component reuse**:

\[
\text{carry mechanism learned in addition}
\rightarrow
\text{reuse in multiplication?}
\]

---

# Design sperimentale

## Condizione A — Primitive incomplete

### Training

- addizione multi-cifra;
- sottrazione multi-cifra;
- nessuna moltiplicazione.

### Test

- moltiplicazione multi-cifra.

Questa condizione misura quanto il modello sia capace di sviluppare spontaneamente anche le primitive mancanti.

Un fallimento in questa condizione, tuttavia, **non costituisce da solo evidenza di fallimento compositivo**, perché il modello non ha mai avuto pressione di training per apprendere i prodotti tra singole cifre.

---

## Condizione B — Primitive complete, algoritmo assente

Questa è la condizione sperimentale principale.

### Training

- addizione multi-cifra;
- sottrazione multi-cifra;
- tutte le moltiplicazioni:

\[
0\text{–}9 \times 0\text{–}9
\]

- zero esempi di moltiplicazione multi-cifra.

### Test

Esempi come:

\[
37\times24
\]

\[
317\times42
\]

\[
281\times537
\]

In questa condizione il modello dispone, almeno comportamentalmente, delle principali primitive necessarie:

- somma;
- gestione della posizione;
- carry;
- prodotti tra singole cifre.

La capacità mancante è precisamente la loro **orchestrazione in un nuovo algoritmo**.

Questa condizione consente quindi di separare:

\[
\text{knowledge acquisition}
\]

da

\[
\text{composition / algorithm construction}
\]

---

## Condizione C — Scaffold compositivo

Il training è identico alla Condizione B, ma vengono aggiunti segnali intermedi controllati.

Possibili scaffold:

- prodotti parziali esplicitati;
- decomposizione per posizione;
- target intermedi;
- esempi di accumulo di prodotti parziali senza mostrare l'intera moltiplicazione;
- curriculum progressivo.

Lo scopo non è semplicemente aumentare l'accuracy.

La domanda è:

> **Qual è la quantità minima di struttura intermedia necessaria perché le primitive già apprese vengano integrate in un algoritmo di moltiplicazione multi-cifra?**

Il confronto:

\[
A \rightarrow B \rightarrow C
\]

permette di distinguere tre problemi diversi:

1. assenza di primitive;
2. incapacità di composizione spontanea;
3. quantità di scaffolding necessaria per innescare la composizione.

---

# Ipotesi meccanicistiche

## Ipotesi 1 — I prodotti parziali non vengono rappresentati o recuperati nel contesto multi-cifra

Anche se il modello sa rispondere correttamente a:

\[
7\times8
\]

non è garantito che, durante:

\[
347\times52
\]

recuperi internamente la rappresentazione:

\[
7\times2=14
\]

nel layer, nella posizione e nel formato necessari all'algoritmo globale.

La distinzione cruciale è quindi tra:

> **possedere una primitiva come capacità isolata**

e

> **renderla disponibile nel contesto computazionale in cui deve essere riutilizzata**.

### Test

Allenare probe sulle attivazioni per determinare se quantità come:

\[
a_i b_j
\]

sono decodificabili durante il forward pass di moltiplicazione.

Un risultato negativo di probing non verrà interpretato come prova definitiva dell'assenza dell'informazione.

Il claim corretto sarà più limitato:

> i prodotti parziali non risultano linearmente decodificabili nelle rappresentazioni, posizioni e layer analizzati.

Il probing dovrà quindi essere combinato, quando possibile, con interventi causali.

---

## Ipotesi 2 — Type mismatch nel residual stream

Il modello può possedere circuiti funzionali per:

- somma posizionale;
- carry propagation;

ma tali circuiti possono essere calibrati su un particolare tipo di input.

Nell'addizione tipica il circuito riceve:

- due operandi;
- somme locali relativamente limitate;
- una particolare distribuzione dei valori intermedi.

Nella moltiplicazione riceverebbe invece:

- un numero variabile di contributi;
- valori intermedi più grandi;
- prodotti parziali;
- distribuzioni di carry differenti.

Il circuito può quindi essere funzionalmente appropriato ma non attivarsi perché l'input cade fuori dal suo regime rappresentazionale abituale.

### Test

Utilizzare activation patching mirato.

Costruire coppie di esempi semanticamente compatibili tra addizione e moltiplicazione e sostituire specifiche attivazioni associate ai circuiti candidati.

Se il patching ripristina selettivamente il comportamento corretto, ciò suggerisce:

\[
\text{meccanismo disponibile}
+
\text{interfaccia incompatibile}
\]

piuttosto che assenza completa del meccanismo.

---

## Ipotesi 3 — Fallimento di routing o orchestrazione

Il modello può:

- conoscere i singoli prodotti;
- saper sommare;
- saper propagare il carry;

ma non possedere una rappresentazione funzionale della procedura che stabilisce:

1. quali coppie \((i,j)\) devono essere considerate;
2. in quale posizione \(i+j\) devono contribuire;
3. in quale ordine i contributi devono essere accumulati;
4. quando il carry deve essere propagato.

In questo caso il collo di bottiglia non è nelle primitive ma nel **routing computazionale**.

---

# Complexity ladder

Per localizzare il punto di rottura, la moltiplicazione verrà studiata attraverso una sequenza controllata di difficoltà.

Per esempio:

\[
300\times40
\]

richiede essenzialmente un solo prodotto parziale non nullo.

Poi:

\[
304\times40
\]

introduce più prodotti.

Poi:

\[
304\times42
\]

introduce prodotti su più posizioni.

Infine:

\[
374\times52
\]

introduce:

- più prodotti parziali;
- accumulo;
- carry;
- interazioni tra posizioni.

La performance potrà essere analizzata come funzione di variabili strutturali quali:

\[
Accuracy =
f(
N_{\text{partial products}},
D_{\text{carry}},
N_{\text{active digits}},
N_{\text{accumulations}}
)
\]

Questo permette di studiare una **frontiera compositiva continua**, invece di limitarsi alla dicotomia successo/fallimento.

---

# Separare le possibili fonti di errore

L'analisi dovrà distinguere almeno i seguenti livelli:

\[
\boxed{
\text{Primitive availability}
\rightarrow
\text{Primitive retrieval}
\rightarrow
\text{Representation compatibility}
\rightarrow
\text{Routing}
\rightarrow
\text{Accumulation}
\rightarrow
\text{Carry propagation}
\rightarrow
\text{Output generation}
}
\]

Il punto centrale del progetto è identificare **il primo stadio causale in cui il processo fallisce**.

Un semplice errore nell'output finale non è sufficientemente informativo.

---

# Analisi causale

La scala ridotta del modello permette di utilizzare strumenti di mechanistic interpretability che diventano molto più difficili da applicare esaustivamente nei frontier model.

Tra questi:

- linear probing;
- activation patching;
- path patching;
- head ablation;
- neuron / MLP ablation;
- causal tracing;
- analisi delle attention pattern;
- analisi delle rappresentazioni nel residual stream;
- confronto tra circuiti nelle diverse operazioni.

L'obiettivo non è soltanto osservare correlazioni nelle attivazioni, ma costruire una catena di evidenza causale.

Per ogni componente candidata:

1. identificare dove viene rappresentata;
2. verificare se è predittiva;
3. intervenire sulla rappresentazione;
4. misurare l'effetto causale;
5. verificare se lo stesso componente viene riutilizzato in un task nuovo.

---

# Perché usare transformer piccoli

Un modello nell'ordine di circa 1–10 milioni di parametri consente una caratterizzazione molto più completa dei circuiti.

È possibile analizzare sistematicamente:

- layer;
- head;
- posizioni;
- MLP;
- flussi di informazione;
- effetti di patching e ablazione.

Il vantaggio principale non è che un piccolo transformer rappresenti perfettamente un frontier LLM.

Il vantaggio è **l'identificabilità del meccanismo**.

Questo studio deve quindi evitare un claim di transfer diretto del tipo:

> "se la composizione fallisce in un modello piccolo, allora fallirà necessariamente anche in uno grande."

La scala può modificare:

- rappresentazioni;
- circuiti;
- strategie;
- modularità;
- ridondanza;
- capacità emergenti.

I modelli di frontiera possono utilizzare strategie aritmetiche differenti da quelle che emergono nei modelli piccoli specializzati.

La conclusione appropriata è quindi più circoscritta:

> **Il progetto costruisce un laboratorio controllato nel quale è possibile identificare causalmente quando e perché primitive computazionali apprese vengono — o non vengono — riutilizzate per costruire un algoritmo nuovo.**

Studi successivi potranno verificare quali proprietà della frontiera osservata persistano al crescere della scala.

---

# Relazione con i lavori precedenti

Il progetto si colloca all'intersezione tra tre filoni.

## 1. Rappresentazioni interne e linear representation hypothesis

Questa letteratura motiva l'idea che variabili concettuali o computazionali possano essere localizzate e decodificate nelle attivazioni.

Il presente progetto aggiunge una domanda ulteriore:

> una rappresentazione utilizzabile in un task viene automaticamente resa disponibile come componente di un task nuovo?

---

## 2. Mechanistic interpretability dell'aritmetica nei transformer piccoli

Lavori su addizione e altre operazioni mostrano che piccoli transformer possono sviluppare circuiti relativamente interpretabili per:

- rappresentazione delle cifre;
- somme locali;
- gestione della posizione;
- carry propagation.

Questi circuiti costituiscono candidate primitive di cui testare il riuso.

---

## 3. Circuit tracing nei modelli più grandi

Analisi recenti di frontier model suggeriscono che modelli grandi possono utilizzare strategie aritmetiche ibride, differenti dagli algoritmi puliti osservabili in modelli piccoli specializzati.

Questo rafforza la necessità di distinguere:

\[
\text{mechanistic result in a controlled model}
\]

da

\[
\text{claim of universal architecture-independent mechanism}
\]

Il primo è l'obiettivo di questo progetto; il secondo non lo è.

---

# Predizioni sperimentali

Il progetto non assume in anticipo che la composizione debba fallire.

Sono possibili diversi esiti.

## Scenario 1 — Composizione spontanea completa

La Condizione B generalizza alla moltiplicazione multi-cifra.

L'analisi mostra:

- recupero dei prodotti parziali;
- riuso dei circuiti di somma;
- riuso dei circuiti di carry;
- routing corretto.

Questo costituirebbe una forte evidenza che un transformer può costruire spontaneamente un nuovo algoritmo combinando primitive già apprese.

---

## Scenario 2 — Primitive presenti, routing assente

Il modello mostra internamente:

- prodotti parziali corretti;
- rappresentazioni numeriche adeguate;

ma fallisce nell'accumulo o nella selezione delle posizioni.

Il collo di bottiglia sarebbe quindi nella **composizione procedurale**.

---

## Scenario 3 — Circuiti riutilizzabili ma interfaccia incompatibile

Il modello possiede i meccanismi necessari, ma questi non ricevono spontaneamente rappresentazioni nel formato corretto.

Il patching riesce a recuperare performance.

Il problema sarebbe quindi interpretabile come:

\[
\text{interface failure}
\]

più che come assenza della capacità.

---

## Scenario 4 — Scaffold minimo sufficiente

La Condizione B fallisce, ma una quantità limitata di training intermedio nella Condizione C produce improvvisamente la generalizzazione.

Questo consentirebbe di stimare **quanto scaffolding serve affinché primitive isolate diventino un algoritmo integrato**.

---

## Scenario 5 — Fallimento a più livelli

È possibile che il modello non sviluppi un singolo collo di bottiglia, ma che la moltiplicazione richieda una riorganizzazione distribuita delle rappresentazioni.

Anche questo sarebbe un risultato informativo, perché mostrerebbe che le primitive apprese nei task sorgente non costituiscono necessariamente moduli indipendenti e plug-and-play.

---

# Il deliverable

Il risultato atteso non è un singolo bit:

\[
\text{compone / non compone}
\]

ma una **anatomia della composizione algoritmica**.

Il progetto mira a descrivere:

1. quali primitive emergono durante l'apprendimento di addizione, sottrazione e moltiplicazione a singola cifra;
2. come tali primitive sono rappresentate;
3. quali primitive vengono riutilizzate in un task nuovo;
4. quali rimangono task-specific;
5. dove avviene il primo fallimento causale;
6. come il fallimento dipende dalla complessità strutturale del problema;
7. quale quantità minima di scaffold rende possibile l'integrazione.

La domanda finale diventa quindi:

> **Non semplicemente: "il transformer sa moltiplicare?"**
>
> ma:
>
> **"Se un transformer possiede tutti i componenti necessari di un algoritmo nuovo, in quali condizioni riesce a riconoscerli come componenti riutilizzabili e a organizzarli spontaneamente in una nuova procedura computazionale?"**

Questa formulazione permette di trasformare la composizionalità da proprietà globale e difficilmente falsificabile a **oggetto sperimentale localizzabile, graduabile e causalmente analizzabile**.

---

# Sintesi della tesi

La tesi centrale del progetto può essere formulata così:

> **La composizionalità nei transformer può essere studiata come capacità di riutilizzare primitive computazionali apprese all'interno di una procedura nuova. Separando disponibilità delle primitive, retrieval, compatibilità rappresentazionale, routing, accumulo e carry propagation, è possibile identificare meccanicisticamente la frontiera tra generalizzazione strutturale e fallimento di composizione.**

Il contributo non consiste quindi nel dimostrare in astratto che i transformer siano o non siano composizionali.

Consiste nel rendere la domanda:

- falsificabile;
- causale;
- graduabile;
- meccanicisticamente interpretabile.
