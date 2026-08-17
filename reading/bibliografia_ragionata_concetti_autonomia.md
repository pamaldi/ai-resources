# Bibliografia ragionata — Concetti, rappresentazioni, autonomia e nuove distinzioni

## Domanda centrale

La domanda che tiene insieme questa bibliografia è:

> **Un sistema può modificare autonomamente il proprio spazio delle rappresentazioni, introducendo nuove distinzioni operative che non erano specificate nel suo vocabolario iniziale, e può autonomamente stabilire che quelle distinzioni sono rilevanti?**

Il problema può essere schematizzato così.

Un sistema parte da un insieme di primitivi:

$$
P_0 = \{p_1,p_2,\ldots,p_n\}
$$

Un sistema puramente combinatorio può costruire strutture molto complesse:

$$
f(p_1,p_2,\ldots,p_n)
$$

ma resta aperta una domanda più forte:

$$
\{p_1,\ldots,p_n\}
\longrightarrow
\{p_1,\ldots,p_n,p_{n+1}\}
$$

dove $p_{n+1}$ non sia semplicemente una combinazione conveniente di elementi già disponibili, ma rappresenti una **nuova distinzione operativa**, capace di modificare il modo in cui il sistema organizza il proprio dominio.

Da qui emergono almeno sette problemi distinti:

1. **Intensione ed estensione** — che cos'è una rappresentazione e che rapporto ha con ciò a cui si applica?
2. **Induzione** — perché proprio una generalizzazione e non un'altra?
3. **Acquisizione dei concetti** — come può comparire un concetto che il sistema non possiede già?
4. **Costruzione di nuove rappresentazioni** — può un sistema passare a uno spazio rappresentazionale più potente?
5. **Grounding e significato** — come acquistano significato le rappresentazioni per il sistema stesso?
6. **Autonomia, agency e normatività** — da dove viene il criterio per cui qualcosa è rilevante, corretto, utile o sbagliato per il sistema?
7. **Emergenza creativa e open-endedness** — può comparire novità che non sia soltanto ricombinazione di possibilità già implicitamente prefissate?

---

# I. Intensione, estensione e struttura della rappresentazione

## 1. Rudolf Carnap — *Meaning and Necessity*

### Perché è importante

Carnap fornisce il punto di partenza logico-semantico della bibliografia.

La distinzione fondamentale è quella tra:

- **estensione**: ciò a cui un'espressione si applica;
- **intensione**: il modo, criterio o regola attraverso cui viene determinata l'estensione.

Questa distinzione permette di formulare una prima versione del problema:

> Un sistema può avere accesso a molti casi estensionali senza possedere per questo il principio intensionale che li organizza.

### Che cosa ci dà

Carnap permette di separare:

$$
\text{insieme dei casi osservati}
$$

da:

$$
\text{regola / concetto che li rende casi dello stesso tipo}
$$

È quindi il fondamento teorico per distinguere **memorizzazione dei casi**, **generalizzazione** e **possesso di un concetto**.

### Che cosa lascia aperto

Carnap descrive la struttura semantica, ma non spiega **come nasca una nuova intensione**.

Non risponde alla domanda:

> Da dove viene il criterio che permette al sistema di vedere casi differenti come istanze della stessa categoria?

---

## 2. Nelson Goodman — *Fact, Fiction, and Forecast*

### Perché è importante

Goodman mostra che i dati non determinano univocamente la regola con cui devono essere generalizzati.

Il celebre problema di *grue* mostra che, dato un insieme finito di osservazioni, sono compatibili molte generalizzazioni differenti.

### Il punto centrale

Dai dati:

$$
D = \{x_1,x_2,\ldots,x_n\}
$$

non segue necessariamente una sola funzione:

$$
f(D)
$$

ma possono essere compatibili molte funzioni:

$$
f_1(D), f_2(D), \ldots, f_k(D)
$$

Il problema non è quindi soltanto imparare dai dati, ma spiegare:

> **Perché il sistema privilegia alcune categorie, proprietà o regolarità rispetto ad altre?**

### Che cosa lascia aperto

Goodman rende evidente il problema della **rilevanza** e della **scelta delle categorie**, ma non spiega da dove provengano nuove categorie.

---

# II. Il problema radicale dell'acquisizione dei concetti

## 3. Jerry Fodor — *The Language of Thought*

### Perché è centrale

Fodor rende il problema estremamente duro.

Se apprendere un concetto significa formulare e testare un'ipotesi, allora per formulare l'ipotesi bisogna possedere già il linguaggio concettuale necessario a rappresentarla.

Si crea quindi un'apparente circolarità:

$$
\text{per apprendere } C
\rightarrow
\text{devo formulare un'ipotesi contenente } C
$$

ma allora:

$$
\text{devo già possedere } C
$$

### Perché è importante per l'AI

La domanda diventa:

> Se l'intero spazio delle ipotesi è già definito dal linguaggio rappresentazionale iniziale, il sistema sta davvero creando nuovi concetti oppure sta soltanto selezionando combinazioni già esprimibili?

### Che cosa lascia aperto

La posizione di Fodor tende verso una risposta nativista: i primitivi concettuali fondamentali non vengono realmente costruiti.

È precisamente la conclusione che la nostra ricerca vorrebbe mettere alla prova.

---

## 4. Massimo Piattelli-Palmarini (a cura di) — *Language and Learning: The Debate between Jean Piaget and Noam Chomsky*

### Perché è importante

Questo volume rende esplicito il conflitto tra due idee molto differenti della cognizione.

Da un lato:

- strutture cognitive che vengono progressivamente **costruite**;

dall'altro:

- strutture fondamentali che devono essere in larga misura **già disponibili**.

La domanda che emerge è:

> **Può una struttura cognitiva costruirne una nuova dotata di capacità rappresentazionali che la struttura precedente non possedeva?**

### Perché è vicino al nostro problema

Qui la questione non è semplicemente apprendere nuovi contenuti.

È capire se sia possibile:

$$
R_0 \rightarrow R_1
$$

con:

$$
\operatorname{ExpressivePower}(R_1)
>
\operatorname{ExpressivePower}(R_0)
$$

### Che cosa lascia aperto

Il dibattito formula magnificamente il problema ma non produce un meccanismo computazionale soddisfacente.

---

## 5. Jean Piaget — *Genetic Epistemology* / *Biology and Knowledge*

### Perché va aggiunto direttamente

Se il problema riguarda la costruzione progressiva di strutture cognitive, è utile avere almeno un testo di Piaget come fonte primaria e non soltanto attraverso il dibattito con Chomsky e Fodor.

Piaget considera la conoscenza come il risultato di processi di costruzione e riorganizzazione.

### Il punto che interessa qui

La domanda piagetiana può essere riletta così:

> Come può una struttura cognitiva inizialmente più povera trasformarsi in una struttura capace di operazioni che prima non possedeva?

Questo rende Piaget una radice teorica importante per tutto il ramo:

$$
\text{costruttivismo}
\rightarrow
\text{Carey}
\rightarrow
\text{Drescher}
$$

### Che cosa lascia aperto

Piaget offre un quadro dello sviluppo cognitivo, non un'architettura artificiale formalmente specificata.

---

# III. Discontinuità concettuale e costruzione di nuove rappresentazioni

## 6. Susan Carey — *The Origin of Concepts*

### Perché è uno dei testi centrali

Carey affronta direttamente la possibilità che durante lo sviluppo cognitivo emergano sistemi rappresentazionali dotati di un potere espressivo che non coincide semplicemente con quello disponibile in precedenza.

Il meccanismo più noto proposto è il **Quinian bootstrapping**.

### La domanda fondamentale

Carey permette di prendere sul serio la possibilità di:

$$
R_0 \longrightarrow R_1
$$

dove $R_1$ non rappresenta semplicemente l'accumulo di nuovi casi, ma una **riorganizzazione concettuale**.

### Perché è importante per il nostro problema

Se questa forma di sviluppo è possibile nella cognizione umana, allora la domanda per l'AI diventa:

> Quali condizioni architetturali permetterebbero a un sistema artificiale di modificare il proprio spazio rappresentazionale?

### Che cosa lascia aperto

Carey propone una teoria dello sviluppo cognitivo umano.

Non fornisce ancora una teoria generale dell'autonomia rappresentazionale di un sistema artificiale.

---

## 7. Gary Drescher — *Made-Up Minds: A Constructivist Approach to Artificial Intelligence*

### Perché è probabilmente una delle aggiunte più importanti

Drescher prova a trasformare il costruttivismo piagetiano in un sistema computazionale.

Il punto interessante è che non si limita a discutere filosoficamente la costruzione dei concetti: cerca di progettare un meccanismo capace di costruire **schemi**, regolarità e strutture interne attraverso l'interazione.

### Perché colma un vuoto

La bibliografia ha molta teoria su:

> perché l'acquisizione di nuovi concetti è problematica?

Drescher sposta la domanda verso:

> **Come potremmo costruire concretamente una macchina che sviluppa progressivamente le proprie strutture?**

È quindi il ponte naturale:

$$
\text{Piaget}
\rightarrow
\text{Carey}
\rightarrow
\text{architettura computazionale}
$$

### Che cosa lascia aperto

Il fatto che il sistema costruisca strutture non implica ancora che possa produrre **nuovi primitivi radicalmente non specificati** o che possieda criteri propri di rilevanza.

---

## 8. Roberto Torretti — *Creative Understanding*

### Perché è importante

Torretti porta il problema della novità concettuale nel contesto della scienza.

Il suo interesse è capire come cambino i concetti scientifici e come possa avvenire una vera **innovazione concettuale**.

### Perché serve

È utile perché mostra che la costruzione di nuove rappresentazioni non è soltanto un problema dello sviluppo infantile.

È anche un problema della conoscenza scientifica:

$$
\text{vecchio quadro concettuale}
\rightarrow
\text{nuovo quadro concettuale}
$$

### Che cosa lascia aperto

Descrive e analizza l'innovazione concettuale umana, ma non fornisce un algoritmo generale che la produca autonomamente.

---

## 9. Douglas Hofstadter e Fluid Analogies Research Group — *Fluid Concepts and Creative Analogies*

### Perché è utile

Questo lavoro affronta un problema vicino ma distinto: la capacità di **ristrutturare dinamicamente uno spazio concettuale**.

Sistemi come Copycat sono interessanti perché non trattano le categorie come completamente rigide: la rappresentazione del problema può cambiare durante il processo di soluzione.

### Il punto importante

Non significa necessariamente creare un nuovo primitivo nel senso più radicale.

Ma mostra una capacità importante:

$$
\text{rappresentazione iniziale}
\rightarrow
\text{ristrutturazione}
\rightarrow
\text{nuova interpretazione}
$$

### Che cosa lascia aperto

La fluidità concettuale non equivale ancora a:

$$
p_{n+1}
$$

come nuovo primitivo realmente indipendente dallo spazio progettato dal sistema.

---

# IV. Significato e symbol grounding

## 10. Stevan Harnad — *The Symbol Grounding Problem*

### Perché è indispensabile

Anche se un sistema riesce a manipolare simboli o rappresentazioni, resta una domanda:

> **Che cosa fa sì che quei simboli significhino qualcosa per il sistema?**

Se ogni simbolo è definito soltanto attraverso altri simboli, otteniamo una rete formalmente coerente ma priva di un collegamento non simbolico con il mondo.

### Perché è centrale per la nostra domanda

La questione non è soltanto:

$$
\text{come nasce una nuova rappresentazione?}
$$

ma:

$$
\text{come quella rappresentazione acquista significato?}
$$

Questo introduce una distinzione fondamentale tra:

- rappresentazione assegnata dall'osservatore;
- rappresentazione che ha una funzione effettiva nell'organizzazione dell'agente.

### Che cosa lascia aperto

Il grounding collega le rappresentazioni all'esperienza e alla discriminazione, ma non risolve da solo il problema della **normatività autonoma**:

> Perché una distinzione dovrebbe contare per il sistema?

---

# V. Interazione, normatività e rappresentazione emergente

## 11. Mark H. Bickhard — modello interattivista della rappresentazione

### Perché è una fonte primaria importante

Bickhard critica l'idea secondo cui una rappresentazione debba essere fondamentalmente una codifica interna che corrisponde a qualcosa di esterno.

Nel modello interattivista, il significato rappresentazionale è legato alle possibilità di interazione del sistema.

### Il cambio di prospettiva

Invece di:

$$
\text{oggetto esterno}
\rightarrow
\text{codifica interna}
$$

la rappresentazione viene collegata a:

$$
\text{organizzazione dell'interazione possibile}
$$

Questo permette di introdurre anche la possibilità dell'**errore**: il sistema può anticipare un'interazione che poi non riesce.

La normatività comincia quindi a essere interna alla dinamica del sistema.

### Perché è centrale

Bickhard crea un ponte naturale tra:

- rappresentazione;
- agency;
- interazione;
- normatività;
- emergenza.

### Che cosa lascia aperto

Resta da mostrare fino a che punto questa impostazione possa produrre una vera espansione open-ended dello spazio rappresentazionale.

---

# VI. Autonomia e auto-organizzazione

## 12. W. Ross Ashby — *Design for a Brain*

### Perché va inserito

Ashby fornisce una delle radici cibernetiche del problema dell'adattamento e dell'auto-organizzazione.

Il punto non è più soltanto rappresentare il mondo, ma mantenere determinate variabili entro regioni compatibili con il funzionamento del sistema.

### Il passaggio importante

Si comincia a intravedere una catena:

$$
\text{regolazione}
\rightarrow
\text{adattamento}
\rightarrow
\text{auto-organizzazione}
\rightarrow
\text{autonomia}
$$

### Perché serve alla nostra ricerca

Introduce una domanda che Goodman e Fodor da soli non possono risolvere:

> Una categoria potrebbe diventare rilevante perché permette al sistema di mantenere la propria organizzazione?

### Che cosa lascia aperto

L'adattamento non equivale automaticamente alla formazione di nuovi concetti.

---

## 13. Francisco J. Varela — *Principles of Biological Autonomy*

### Perché cambia il paradigma

Con Varela la domanda non è più soltanto:

> Come può un sistema manipolare o costruire rappresentazioni?

ma:

> **Che cosa rende un sistema autonomo?**

Un sistema autonomo non è semplicemente controllato dall'esterno: contribuisce a produrre e mantenere la propria organizzazione.

### Perché questo è decisivo

La rilevanza può allora essere legata all'organizzazione stessa dell'agente.

Si apre una possibilità:

$$
\text{autonomia}
\rightarrow
\text{normatività}
\rightarrow
\text{rilevanza}
$$

Una distinzione non sarebbe importante soltanto perché il progettista l'ha scelta, ma perché ha conseguenze per la continuità dell'organizzazione del sistema.

### Che cosa lascia aperto

L'autonomia biologica non dimostra automaticamente come nascano nuovi simboli o nuovi primitivi concettuali.

---

## 14. Francisco Varela, Evan Thompson & Eleanor Rosch — *The Embodied Mind*

### Perché è importante

Questo libro sposta ulteriormente il centro della cognizione.

La cognizione non viene trattata semplicemente come:

$$
\text{input}
\rightarrow
\text{rappresentazione}
\rightarrow
\text{output}
$$

ma come attività incarnata e situata nella relazione tra organismo e ambiente.

### La tesi importante per noi

Il mondo rilevante per un agente non deve essere necessariamente interamente predefinito.

Può emergere attraverso l'interazione:

$$
\text{agente}
\leftrightarrow
\text{ambiente}
$$

### Che cosa lascia aperto

Rimane difficile trasformare l'enattivismo in un meccanismo computazionale preciso capace di spiegare l'origine di nuove categorie formali.

---

## 15. Ezequiel Di Paolo, Thomas Buhrmann & Xabier Barandiaran — *Sensorimotor Life*

### Perché è fondamentale

È una delle sistematizzazioni più complete del rapporto tra:

- autonomia;
- agency;
- normatività;
- corpo;
- interazione sensomotoria;
- produzione di significato.

### Perché serve

La domanda diventa più forte.

Non basta chiedere:

> Come si genera un nuovo concetto?

Bisogna chiedere:

> **Come nasce una nuova distinzione che abbia significato e rilevanza per l'agente?**

Possiamo quindi scrivere:

$$
\text{nuova distinzione}
+
\text{rilevanza}
+
\text{possibilità d'azione}
$$

### Che cosa lascia aperto

Spiega molto bene il problema della significatività per l'agente, ma meno direttamente quello della nascita di un **nuovo primitivo computazionale**.

---

# VII. Emergenza creativa e costruzione di nuovi osservabili

## 16. Peter Cariani — lavori su emergence, adaptive measurement e epistemic autonomy

### Perché deve rimanere trasversale a tutta la bibliografia

Cariani formula forse la distinzione più vicina alla domanda tecnica che ci interessa.

Possiamo distinguere tra:

### Emergenza combinatoria

Il sistema possiede già:

$$
P = \{p_1,\ldots,p_n\}
$$

e genera nuove configurazioni:

$$
f(P)
$$

La complessità può diventare enorme, ma il vocabolario fondamentale rimane quello iniziale.

### Emergenza creativa

Il sistema passa invece a:

$$
P' = \{p_1,\ldots,p_n,p_{n+1}\}
$$

dove appare un nuovo tipo di distinzione o un nuovo osservabile.

### Perché è cruciale

Cariani porta il problema dal piano puramente concettuale a quello **epistemico e operativo**.

La domanda diventa:

> Può un sistema costruire nuovi modi di misurare, distinguere e interagire con il proprio ambiente?

Questa è una formulazione molto più forte della semplice capacità di apprendere nuovi pesi o nuove combinazioni.

### Che cosa lascia aperto

Il problema rimane estremamente difficile:

> Come distinguere una reale espansione dello spazio epistemico da una trasformazione che era già implicitamente prevista dal meta-spazio progettato dall'esterno?

Cariani dovrebbe quindi essere letto **in parallelo a tutti gli altri filoni**, non come semplice voce finale.

---

# VIII. Representation learning e AI moderna

## 17. Yoshua Bengio, Aaron Courville & Pascal Vincent — *Representation Learning: A Review and New Perspectives*

### Perché serve

Questo lavoro rappresenta un ponte verso il machine learning contemporaneo.

Il machine learning moderno non apprende soltanto funzioni su caratteristiche progettate manualmente: apprende anche rappresentazioni interne.

### La domanda fondamentale

Una rete può trasformare:

$$
x
\rightarrow
z_1
\rightarrow
z_2
\rightarrow
\cdots
\rightarrow
z_n
$$

costruendo progressivamente rappresentazioni astratte.

Questo è già un passo importante rispetto ai sistemi simbolici con vocabolario interamente specificato manualmente.

### Ma attenzione

**Representation learning non equivale automaticamente a conceptual innovation.**

Una rete può trovare nuove coordinate latenti senza per questo modificare autonomamente:

- il proprio spazio degli osservabili;
- i propri criteri di rilevanza;
- la propria funzione obiettivo;
- il tipo di interazioni attraverso cui acquisisce informazione.

### Che cosa lascia aperto

È proprio qui che nasce il problema degli LLM e dei Transformer:

> La formazione di rappresentazioni interne sempre più astratte costituisce vera espansione concettuale oppure rimane una riorganizzazione entro uno spazio di apprendimento definito dall'architettura e dall'obiettivo?

---

# IX. Open-endedness

## 18. Letteratura su Open-Ended Evolution / Open-Endedness

### Perché è direttamente collegata al problema

L'Artificial Life studia da tempo una domanda molto simile:

> Come può un sistema continuare a produrre novità senza esaurirsi in un insieme finito o predefinito di possibilità interessanti?

La questione è particolarmente importante perché obbliga a distinguere:

$$
\text{grande spazio combinatorio}
$$

da:

$$
\text{spazio capace di espandersi}
$$

### Collegamento con Cariani

Il problema dell'open-endedness può essere letto come una versione dinamica della distinzione tra emergenza combinatoria ed emergenza creativa.

Non basta generare:

$$
10^{100}
$$

configurazioni differenti se tutte appartengono allo stesso spazio ontologico iniziale.

La domanda forte è:

$$
\Omega_0
\rightarrow
\Omega_1
\rightarrow
\Omega_2
\rightarrow
\cdots
$$

dove anche lo **spazio delle possibilità** può cambiare.

### Che cosa lascia aperto

Molti sistemi open-ended continuano comunque a dipendere da:

- regole di evoluzione progettate;
- criteri esterni;
- ambienti artificialmente costruiti;
- meta-spazi prefissati.

Quindi l'open-endedness non risolve automaticamente il problema dell'autonomia epistemica.

---

# X. AGI e limiti dell'approccio algoritmico tradizionale

## 19. Herbert Roitblat — *Algorithms Are Not Enough*

### Perché conclude bene il percorso

Roitblat riporta queste questioni direttamente alla discussione sull'intelligenza artificiale generale.

Il problema non è soltanto aumentare:

- quantità di dati;
- capacità computazionale;
- dimensione dei modelli;
- complessità delle funzioni.

La questione riguarda anche il modo in cui vengono costruite e modificate le rappresentazioni.

### Perché è utile

Permette di formulare la domanda finale:

> **Un sistema che opera sempre all'interno delle rappresentazioni, degli obiettivi e delle modalità di interazione stabilite dal progettista può essere epistemicamente autonomo?**

### Che cosa lascia aperto

Il libro critica i limiti dei paradigmi esistenti, ma non fornisce ancora una soluzione architetturale definitiva.

---

# La mappa concettuale complessiva

La bibliografia può essere letta come una successione di problemi.

## 1. Carnap

Abbiamo bisogno di distinguere:

$$
\text{estensione} \neq \text{intensione}
$$

↓

## 2. Goodman

I dati non determinano da soli la regola:

$$
D \not\Rightarrow \text{un'unica generalizzazione}
$$

↓

## 3. Fodor

Se per apprendere un concetto devo già poterlo rappresentare:

$$
\text{come nasce un concetto realmente nuovo?}
$$

↓

## 4. Piaget / Carey

Forse è possibile una trasformazione:

$$
R_0 \rightarrow R_1
$$

con:

$$
\operatorname{ExpressivePower}(R_1)
>
\operatorname{ExpressivePower}(R_0)
$$

↓

## 5. Drescher / Hofstadter

Possiamo provare a costruire sistemi che:

- inventano schemi;
- ristrutturano rappresentazioni;
- modificano il modo di interpretare un problema.

Ma rimane:

> è vera innovazione concettuale o riorganizzazione entro un meta-spazio già progettato?

↓

## 6. Harnad

Anche una nuova rappresentazione deve essere **grounded**.

↓

## 7. Bickhard / Varela / Di Paolo

Ma il grounding non basta.

Serve spiegare:

$$
\text{significato}
+
\text{normatività}
+
\text{rilevanza}
+
\text{agency}
$$

↓

## 8. Cariani

Il problema diventa:

> Può il sistema costruire nuovi osservabili e nuovi modi di distinguere il mondo?

↓

## 9. Open-endedness

E può continuare a farlo senza che l'intero spazio delle possibilità sia già stato implicitamente definito?

↓

## 10. AI contemporanea

Infine:

> Le rappresentazioni emergenti nei Transformer e negli LLM costituiscono una forma di vera innovazione concettuale oppure una forma estremamente potente di emergenza combinatoria all'interno di un regime rappresentazionale e normativo definito dall'esterno?

---

# Il vero nucleo della ricerca

La formulazione:

> **“Gli LLM non sanno astrarre.”**

è probabilmente troppo debole.

Gli LLM possono certamente costruire rappresentazioni astratte e generalizzare in numerosi domini.

La domanda teoricamente più interessante è invece:

> **Un sistema può modificare autonomamente il proprio spazio delle rappresentazioni, introducendo nuove distinzioni operative che non erano specificate nel suo vocabolario iniziale, e può autonomamente stabilire che tali distinzioni sono rilevanti?**

Possiamo separarla in quattro condizioni.

## A. Novità rappresentazionale

Il sistema produce una distinzione non riducibile banalmente a una combinazione delle categorie operative iniziali.

## B. Novità operativa

La nuova distinzione modifica ciò che il sistema può misurare, prevedere o fare.

## C. Rilevanza autonoma

La distinzione viene selezionata non soltanto perché migliora una funzione obiettivo fissata dall'esterno, ma perché acquista rilevanza rispetto all'organizzazione e all'attività propria del sistema.

## D. Espansione dello spazio epistemico

Il sistema non seleziona soltanto un punto entro:

$$
\Omega
$$

ma contribuisce a trasformare:

$$
\Omega_0 \rightarrow \Omega_1
$$

Queste quattro condizioni permettono di distinguere molto meglio:

- apprendimento;
- generalizzazione;
- astrazione;
- representation learning;
- composizione;
- ristrutturazione;
- innovazione concettuale;
- autonomia epistemica.

---

# Autori chiave per ciascun problema

| Problema | Autori / testi principali |
|---|---|
| Intensione / estensione | Carnap |
| Induzione e scelta delle categorie | Goodman |
| Impossibilità / difficoltà dell'acquisizione di concetti primitivi | Fodor |
| Costruzione di strutture cognitive | Piaget |
| Discontinuità concettuale | Carey |
| Implementazione computazionale costruttivista | Drescher |
| Ristrutturazione e fluidità concettuale | Hofstadter / FARG |
| Innovazione concettuale scientifica | Torretti |
| Symbol grounding | Harnad |
| Rappresentazione interattiva e normatività | Bickhard |
| Adattamento e auto-organizzazione | Ashby |
| Autonomia | Varela |
| Embodiment / enaction | Varela, Thompson & Rosch |
| Agency e normatività sensomotoria | Di Paolo, Buhrmann & Barandiaran |
| Emergenza creativa / nuovi osservabili | Cariani |
| Representation learning | Bengio, Courville & Vincent |
| Open-ended novelty | Open-Ended Evolution / Artificial Life |
| Limiti dell'AGI algoritmica | Roitblat |

---

# Percorso di lettura consigliato

Non leggerei tutti i testi in ordine cronologico.

Seguirei invece il problema.

## Percorso essenziale — 8 tappe

### 1. Carnap — *Meaning and Necessity*

Per capire bene:

- intensione;
- estensione;
- rappresentazione.

↓

### 2. Goodman — *Fact, Fiction, and Forecast*

Per capire perché:

$$
\text{dati} \neq \text{regola determinata univocamente}
$$

↓

### 3. Piattelli-Palmarini — *Language and Learning*

Per vedere esplodere il conflitto:

$$
\text{costruzione}
\quad\text{vs}\quad
\text{strutture già disponibili}
$$

Leggere Fodor parallelamente.

↓

### 4. Susan Carey — *The Origin of Concepts*

Per incontrare un tentativo serio di spiegare:

$$
\text{vecchio sistema concettuale}
\rightarrow
\text{nuovo sistema concettuale}
$$

↓

### 5. Gary Drescher — *Made-Up Minds*

Per passare dalla teoria a una domanda architetturale:

> Come costruire un sistema che sviluppa strutture?

↓

### 6. Harnad + Bickhard

Per introdurre:

$$
\text{grounding}
+
\text{interazione}
+
\text{normatività}
$$

↓

### 7. Varela — *Principles of Biological Autonomy*

Per chiedere:

> Che cosa cambierebbe se il criterio di rilevanza dipendesse dall'organizzazione propria del sistema?

↓

### 8. Di Paolo et al. — *Sensorimotor Life*

Per arrivare alla combinazione:

$$
\boxed{
\text{autonomia}
+
\text{agency}
+
\text{significato}
+
\text{normatività}
}
$$

Durante tutto il percorso:

> **leggere Cariani in parallelo.**

---

# Percorso tecnico successivo

Dopo aver chiarito il problema teorico, passerei alla parte contemporanea:

1. **Representation learning**
2. **World models**
3. **Object-centric learning**
4. **Continual learning**
5. **Meta-learning**
6. **Causal representation learning**
7. **Neuro-symbolic architectures**
8. **Program synthesis / concept learning**
9. **Open-ended learning**
10. **Intrinsic motivation / empowerment**
11. **Autonomous goal generation**
12. **Developmental robotics**

A quel punto la domanda potrebbe essere trasformata da problema filosofico a programma sperimentale:

> **Quale modifica architetturale permetterebbe a un sistema non soltanto di apprendere rappresentazioni, ma di modificare i propri osservabili, costruire nuove variabili e riorganizzare autonomamente il proprio spazio dei problemi?**

---

# Tre testi che colmano maggiormente i vuoti della bibliografia iniziale

Se si volessero aggiungere soltanto tre fonti alla bibliografia originaria, sceglierei:

## 1. Gary Drescher — *Made-Up Minds*

Perché colma il vuoto tra:

$$
\text{costruttivismo cognitivo}
\leftrightarrow
\text{architettura artificiale}
$$

## 2. Stevan Harnad — *The Symbol Grounding Problem*

Perché impedisce di confondere:

$$
\text{manipolazione formale}
$$

con:

$$
\text{significato}
$$

## 3. Mark Bickhard — lavori sull'Interactivist Model

Perché collega:

$$
\text{rappresentazione}
+
\text{interazione}
+
\text{errore}
+
\text{normatività}
$$

---

# Il quadrato teorico centrale

Se dovessimo ridurre l'intero progetto a quattro autori, probabilmente sarebbero:

## Fodor

**Il problema.**

> Come può comparire un concetto che il sistema non possiede già?

## Carey

**La possibilità di una discontinuità.**

> Un sistema cognitivo può passare a strutture rappresentazionali più potenti.

## Cariani

**La formulazione operativa della novità.**

> Può comparire un nuovo osservabile o una nuova distinzione che non appartiene semplicemente al repertorio combinatorio precedente?

## Varela

**La rilevanza autonoma.**

> Può il criterio di ciò che conta emergere dall'organizzazione propria del sistema?

Il nucleo della ricerca diventa quindi:

$$
\boxed{
\text{Fodor}
+
\text{Carey}
+
\text{Cariani}
+
\text{Varela}
}
$$

ovvero:

$$
\boxed{
\text{nuovi concetti}
+
\text{nuovi osservabili}
+
\text{autonomia}
+
\text{rilevanza}
}
$$

---

# Riferimenti essenziali

- Ashby, W. Ross. *Design for a Brain*.
- Bengio, Yoshua, Aaron Courville, and Pascal Vincent. “Representation Learning: A Review and New Perspectives.”
- Bickhard, Mark H. Lavori sull'**Interactivist Model**, interazione, rappresentazione e normatività.
- Carey, Susan. *The Origin of Concepts*. Oxford University Press.
- Cariani, Peter. Lavori su **emergence**, **adaptive measurement**, **new observables** ed **epistemic autonomy**.
- Carnap, Rudolf. *Meaning and Necessity*.
- Di Paolo, Ezequiel A., Thomas Buhrmann, and Xabier E. Barandiaran. *Sensorimotor Life: An Enactive Proposal*.
- Drescher, Gary L. *Made-Up Minds: A Constructivist Approach to Artificial Intelligence*.
- Fodor, Jerry A. *The Language of Thought*.
- Goodman, Nelson. *Fact, Fiction, and Forecast*.
- Harnad, Stevan. “The Symbol Grounding Problem.”
- Hofstadter, Douglas R., and Fluid Analogies Research Group. *Fluid Concepts and Creative Analogies*.
- Piaget, Jean. *Genetic Epistemology*.
- Piaget, Jean. *Biology and Knowledge*.
- Piattelli-Palmarini, Massimo, ed. *Language and Learning: The Debate between Jean Piaget and Noam Chomsky*.
- Roitblat, Herbert L. *Algorithms Are Not Enough: Creating General Artificial Intelligence*.
- Torretti, Roberto. *Creative Understanding: Philosophical Reflections on Physics*.
- Varela, Francisco J. *Principles of Biological Autonomy*.
- Varela, Francisco J., Evan Thompson, and Eleanor Rosch. *The Embodied Mind*.
- Letteratura su **Open-Ended Evolution / Open-Endedness** nell'Artificial Life.

---

# Tesi di lavoro provvisoria

La questione non sembra essere semplicemente se un sistema artificiale sappia **astrarre**.

Il problema più profondo è distinguere tra:

$$
\text{astrazione entro uno spazio dato}
$$

e:

$$
\text{costruzione autonoma di un nuovo spazio di distinzioni}
$$

Un sistema potrebbe essere estremamente potente nella prima operazione senza possedere la seconda.

La domanda finale può quindi essere formulata così:

> **Quali condizioni sono necessarie affinché un sistema artificiale non si limiti a ottimizzare e ricombinare rappresentazioni entro uno spazio epistemico dato, ma possa costruire autonomamente nuovi osservabili, nuove distinzioni e nuovi criteri di rilevanza, modificando così lo spazio stesso entro cui apprende e agisce?**

Questa domanda collega direttamente:

- filosofia del linguaggio;
- epistemologia;
- scienze cognitive;
- developmental psychology;
- cibernetica;
- enattivismo;
- Artificial Life;
- representation learning;
- AGI.

Ed è probabilmente il punto più forte attorno a cui organizzare tutto il lavoro successivo.
