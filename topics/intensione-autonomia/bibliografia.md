# Intensione, estensione e i limiti dell'autonomia

## Bibliografia ragionata

Fusione di due bibliografie costruite indipendentemente e poi rimaste separate per mesi. Si sono rivelate **complementari più che sovrapposte**: condividono nove autori su una cinquantina di voci, e la loro divergenza è già un'informazione — descrivono due tradizioni che pongono la stessa domanda e non si citano quasi mai.

| | asse |
|---|---|
| **A** — logico-computazionale | cosa è calcolabile, cosa è esprimibile, da dove vengono i primitivi |
| **B** — enattivo-biologico | cosa rende un sistema un agente, da dove viene la normatività |

> ⚠️ **Le due tradizioni non danno la stessa diagnosi.** Vedere §0 — è la prima cosa da leggere.

### Come leggere le annotazioni

**Provenienza del riferimento** · `[V]` verificato in rete · `[M]` citato a memoria, da confermare prima dell'uso formale

**Disponibilità del testo** (verifica del 17 agosto 2026, dettagli in [Appendice A](#appendice-a--disponibilità-dei-testi)) · 🟢 open access · 🔵 repository pubblico · 🟡 diritti non chiari · 🔒 accesso ristretto · ⚪ nessun full text gratuito

**Lascia aperto:** — presente sui testi centrali. È la riga che concatena la bibliografia: ogni testo risolve qualcosa e consegna al successivo ciò che non risolve.

---

## 0. Il disaccordo, prima delle liste

Vale la pena metterlo in cima, perché altrimenti la bibliografia sembra un percorso unico e non lo è.

**La diagnosi A**: il limite è formale. Non puoi imparare un concetto che non sai esprimere (Fodor); le proprietà che contano sono indecidibili (Rice); nessun algoritmo è universalmente migliore (Wolpert); la computazione ricombina primitivi ma non li crea (Cariani).

**La diagnosi B**: il limite è che ai sistemi attuali **non importa niente**. Manca la normatività intrinseca — condizioni che siano migliori o peggiori *per il sistema stesso*. Un sistema che si auto-produce ce l'ha per costruzione (Varela, Bickhard, Barandiaran).

Non sono compatibili. Un enattivista risponderebbe che il teorema di Rice è fuori bersaglio perché presuppone ancora che la cognizione sia computazione su rappresentazioni. Un fodoriano risponderebbe che l'autopoiesi spiega perché un sistema *persiste*, non come acquisisce un *concetto*.

**Chi sta in mezzo**: Cariani pubblica nel volume curato da Varela e Bourgine, ma il suo argomento è semiotico-computazionale. È il punto di contatto più vicino esistente, e il fatto che sia una singola persona invece di una letteratura dice quanto il ponte sia sottile.

---

## 0-bis. La domanda, in forma

> **Un sistema può modificare autonomamente il proprio spazio delle rappresentazioni, introducendo nuove distinzioni operative che non erano specificate nel suo vocabolario iniziale, e può autonomamente stabilire che quelle distinzioni sono rilevanti?**

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

dove $p_{n+1}$ non sia semplicemente una combinazione conveniente di elementi già disponibili, ma una **nuova distinzione operativa**, capace di modificare il modo in cui il sistema organizza il proprio dominio.

Da qui emergono sette problemi distinti, che sono anche l'indice di questa bibliografia:

| # | problema | §  |
|---|---|---|
| 1 | **Intensione ed estensione** — che cos'è una rappresentazione e che rapporto ha con ciò a cui si applica? | §1 |
| 2 | **Induzione** — perché proprio una generalizzazione e non un'altra? | §2 |
| 3 | **Limiti formali** — cosa è in linea di principio decidibile su una descrizione? | §3 |
| 4 | **Acquisizione dei concetti** — come può comparire un concetto che il sistema non possiede già? | §4 |
| 5 | **Costruzione di nuove rappresentazioni** — può un sistema passare a uno spazio più potente? | §5 |
| 6 | **Grounding e significato** — come acquistano significato le rappresentazioni *per il sistema*? | §6 |
| 7 | **Autonomia, agency, normatività** — da dove viene il criterio di rilevanza? | §7–8 |
| 8 | **Emergenza creativa e open-endedness** — può comparire novità non prefissata? | §9–10 |

---

## 0-ter. Le definizioni

Prima delle letture, i termini. Le tre coppie ricorrono in tutta la bibliografia con nomi diversi ma sono strettamente imparentate.

### Estensione e intensione

**Estensione** di un termine: l'**insieme delle cose** a cui si applica.
**Intensione**: la **regola, condizione o modo di presentazione** che determina quell'insieme.

```
"animale con il cuore"   ─┐
                          ├─ stessa ESTENSIONE (di fatto, gli stessi animali)
"animale con i reni"     ─┘   intensioni DIVERSE (due condizioni distinte)
```

Il punto è che l'identità di estensione **non implica** identità di intensione. Scoprire che due condizioni diverse selezionano gli stessi oggetti è una scoperta empirica, non logica — è l'esempio di Frege: «stella del mattino» e «stella della sera» indicano Venere, ma stabilirlo è stata astronomia.

Da cui una conseguenza che ritorna ovunque: **due descrizioni possono essere equivalenti in ciò che denotano e diversissime in ciò che consentono di fare.**

Ne segue anche la formulazione forte del problema (§0-bis): un sistema può avere accesso a moltissimi casi **estensionali** senza per questo possedere il principio **intensionale** che li organizza. È il fondamento per distinguere memorizzazione dei casi, generalizzazione e possesso di un concetto.

### Applicata alle funzioni e ai programmi

Due programmi sono:

| | quando |
|---|---|
| **estensionalmente uguali** | per ogni input producono lo stesso output |
| **intensionalmente uguali** | sono lo stesso programma |

Bubble sort e quicksort sono estensionalmente identici — calcolano la stessa funzione — e nessuno userebbe il primo. La differenza è tutta intensionale: numero di passi, struttura, lunghezza della descrizione.

Stesso schema, sull'aritmetica:

```
mult(a,b)              e      a + a + … + a   (b volte)
```

calcolano la stessa funzione sui naturali. **Estensionalmente indistinguibili.** Ma nella prima il numero di ripetizioni è un argomento manipolabile; nella seconda è una proprietà della forma dell'espressione. L'addizione ripetuta *contiene* quell'informazione ma non la *rappresenta*.

> Una funzione obiettivo che guardi solo *cosa produce* un'ipotesi non può preferire l'una all'altra. La distinzione va messa esplicitamente nel criterio — come lunghezza di descrizione, o come costo di esecuzione.

### Perché il criterio guarda sempre la forma

E qui la logica dà una risposta secca, che è il **teorema di Rice** (§3): ogni proprietà **estensionale** non banale di un programma è indecidibile, mentre le proprietà **intensionali** — lunghezza, sintassi, numero di passi — sono immediate.

Quindi nessun criterio automatico può interrogare direttamente *cosa* un programma calcola. Può interrogare solo *com'è fatto*. Non è pigrizia del progettista: è l'unica cosa guardabile.

### Le coppie imparentate

Termini diversi, stessa faglia. Utile tenerli allineati:

| | lato «cosa» | lato «come» |
|---|---|---|
| semantica classica | estensione | intensione |
| programmi | funzione calcolata | algoritmo |
| Frege | riferimento (*Bedeutung*) | senso (*Sinn*) |
| teoria dei tipi | uguaglianza proposizionale | uguaglianza definizionale |
| Cariani (§9) | — | ottimizzazione **delle** categorie vs **dentro** le categorie |
| Carnap | estensione | intensione + stati possibili |

L'ultima riga di Cariani non è un sinonimo delle altre, ma vi si aggancia: la sua ricerca **semantica** riguarda quali distinzioni esistano — cioè quale estensione sia raggiungibile — mentre la ricerca **sintattica** opera dentro un vocabolario dato.

### Un avvertimento

I termini sono usati in modi non sempre coincidenti nelle diverse tradizioni. In logica modale «intensione» ha un senso tecnico preciso (funzione dai mondi possibili alle estensioni, Carnap); in informatica è più informale e significa «riguardante la forma del programma»; in filosofia della mente si sovrappone parzialmente a *contenuto*.

**Non sono la stessa nozione**, e chi le tratta come tali produce equivoci. La famiglia di somiglianza è reale; l'identità no.

### Riferimenti per questa sezione

**Le definizioni.** Estensione e intensione nella forma qui usata vengono da **Carnap (1947)**, §1; il precedente è **Frege (1892)**. Per una voce enciclopedica aggiornata e gratuita: *Intensional Logic* e *Reference* nella **Stanford Encyclopedia of Philosophy** (`plato.stanford.edu`) — è il punto di ingresso migliore se non si vuole partire dai classici. `[M]`

**Il rapporto tra intensione e possibilità.** Il senso tecnico stretto — l'intensione come funzione dai mondi possibili alle estensioni — è di Carnap ed è ripreso in **Montague (1970), *Universal Grammar*** e nella semantica formale successiva. `[M]`

**L'uguaglianza estensionale tra programmi.** La distinzione è standard in teoria dei linguaggi di programmazione; l'esposizione canonica sta in **Pierce, *Types and Programming Languages*** (MIT Press, 2002), sui capitoli dedicati all'equivalenza contestuale. Per il lato teoria dei tipi, **Martin-Löf (1984)**, già in §1. `[M]`

**Il teorema di Rice.** **Rice (1953)**, in §3. Per l'enunciato con dimostrazione: **Sipser, *Introduction to the Theory of Computation***, oppure **Rogers, *Theory of Recursive Functions and Effective Computability*** (1967) per la trattazione completa. `[M]`

**Il costo intensionale dentro un criterio induttivo.** **Levin (1973)** e lo **speed prior** di **Schmidhuber (2002)**, entrambi in §3 — sono i due posti in cui il numero di passi entra formalmente nella selezione dell'ipotesi invece di restarne fuori.

> ⚠️ **Nota di provenienza.** Le definizioni e i teoremi citati sopra sono standard. Non lo sono due cose in questa sezione, che vanno lette come rielaborazione e non come dottrina:
>
> — **l'esempio `mult` contro addizione ripetuta** è una formulazione di lavoro, non un esempio canonico della letteratura;
> — **la tabella delle coppie imparentate** è un allineamento costruito qui. Le corrispondenze sono difendibili una per una, ma nessun autore le mette in fila così, e la riga su Cariani vi si aggancia solo per analogia.

---

# Parte I — Le letture

## 1. La distinzione

**Frege, G. (1892).** *Über Sinn und Bedeutung*. Zeitschrift für Philosophie und philosophische Kritik 100: 25–50. `[M]`

> L'origine. Riferimento contro senso: stessa cosa indicata, modo di presentarla diverso. Scoprire che stella del mattino e stella della sera coincidono è stata astronomia, non logica.

**★ Carnap, R. (1947).** *Meaning and Necessity: A Study in Semantics and Modal Logic*. University of Chicago Press. `[M]` 🟡

> Il testo classico più diretto, e il punto di partenza logico-semantico dell'intera bibliografia. Estensione = l'insieme che soddisfa il predicato; intensione = la regola che decide l'appartenenza. **Due regole diverse possono selezionare lo stesso insieme.**
>
> Permette di separare l'*insieme dei casi osservati* dalla *regola che li rende casi dello stesso tipo* — cioè di distinguere memorizzazione, generalizzazione e possesso di un concetto.
>
> **Lascia aperto:** descrive la struttura semantica, non come *nasca* una nuova intensione. Da dove viene il criterio che permette di vedere casi differenti come istanze della stessa categoria?

**Kripke, S. (1980).** *Naming and Necessity*. Harvard University Press. `[M]`

> Possedere una descrizione di qualcosa e riuscire a riferirsi a quella cosa non sono la stessa operazione.

**Putnam, H. (1975).** *The Meaning of "Meaning"*. In *Mind, Language and Reality*, Cambridge University Press, 215–271. `[M]`

> Twin Earth: il significato non è determinato dagli stati interni. È il primo punto in cui l'ambiente entra dentro il contenuto semantico — e da lì si arriva al grounding (§6).

**Quine, W.V.O. (1951).** *Two Dogmas of Empiricism*. Philosophical Review 60(1): 20–43. `[M]`

> Il contraltare estensionalista: se il significato non si riduce all'estensione, non è chiaro che sia qualcosa. La distinzione non è pacifica.

**Martin-Löf, P. (1984).** *Intuitionistic Type Theory*. Bibliopolis. `[M]`

> La versione viva e operativa: uguaglianza *definizionale* (stessa forma normale) contro *proposizionale* (esiste una dimostrazione). Spina dorsale di Coq, Agda, Lean.

---

## 2. Dai casi alla regola — il problema dell'induzione

**★ Goodman, N. (1955).** *Fact, Fiction, and Forecast*. Harvard University Press. `[M]` 🔒

> **Il nuovo enigma dell'induzione.** Il problema di *grue*: dato un insieme finito di osservazioni, sono compatibili molte generalizzazioni differenti. Da $D = \{x_1,\ldots,x_n\}$ non segue una sola $f(D)$, ma un ventaglio $f_1(D),\ldots,f_k(D)$.
>
> La domanda diventa quindi perché alcune categorie ci sembrano naturali e altre arbitrarie — cioè **perché il sistema privilegia certe regolarità**. È il ponte obbligato tra §1 e §3.
>
> **Lascia aperto:** rende evidente il problema della rilevanza e della scelta delle categorie, ma non dice da dove provengano categorie *nuove*.

**Mitchell, T.M. (1980).** *The Need for Biases in Learning Generalizations*. CBM-TR-117, Rutgers University. `[M]`
`https://www.cs.cmu.edu/~tom/pubs/NeedForBias_1980.pdf`

> Il collegamento tra il problema filosofico e il machine learning: per generalizzare oltre gli esempi osservati **serve necessariamente un bias induttivo**. Non esiste deduzione della regola dai dati. Breve, gratuito, e più chiaro di molta letteratura successiva.

**Wolpert, D. & Macready, W. (1997).** *No Free Lunch Theorems for Optimization*. IEEE Transactions on Evolutionary Computation 1(1): 67–82. `[M]`
**Wolpert, D. (1996).** *The lack of a priori distinctions between learning algorithms*. Neural Computation 8(7): 1341–1390. `[M]`

> La versione matematica di Mitchell. Le prestazioni vengono per intero dal combaciare del bias col mondo. **Non esiste un apprendista universale**, e quindi qualcosa deve essere dato prima.

---

## 3. I limiti formali

*Assenti dalla tradizione B, e in larga parte ignorati anche dalla letteratura ML.*

**Rice, H.G. (1953).** *Classes of recursively enumerable sets and their decision problems*. Transactions of the American Mathematical Society 74(2): 358–366. `[M]`

> **Il fondo della questione.** Ogni proprietà *estensionale* non banale di un programma è indecidibile; le proprietà *intensionali* — lunghezza, sintassi, numero di passi — sono immediate.
>
> Ne segue che ogni criterio automatico guarda la forma non per pigrizia del progettista, ma perché **è l'unica cosa guardabile**.

**Blum, M. (1967).** *A machine-independent theory of the complexity of recursive functions*. Journal of the ACM 14(2): 322–336. `[M]`

> Il teorema di speedup: esistono funzioni per cui, dato un qualunque programma che le calcola, ne esiste sempre uno molto più veloce. Non esiste un programma ottimo.

**Levin, L. (1973).** *Universal sequential search problems*. Problems of Information Transmission 9(3): 265–266. `[M]`

> Lunghezza del programma **più** logaritmo del tempo. Uno dei pochi criteri induttivi in cui il costo intensionale entra dentro invece di restare fuori.

---

## 4. Il problema radicale dell'acquisizione dei concetti

**★ Fodor, J. (1975).** *The Language of Thought*. Harvard University Press. `[M]` 🔒

> Rende il problema estremamente duro. Imparare è formulare e testare ipotesi; un'ipotesi va formulata in un linguaggio; quindi **non puoi imparare un concetto che non eri già in grado di esprimere.** La circolarità: per apprendere $C$ devo formulare un'ipotesi che contiene $C$, dunque devo già possedere $C$.
>
> Per l'AI la domanda diventa: se l'intero spazio delle ipotesi è definito dal linguaggio rappresentazionale iniziale, il sistema crea davvero nuovi concetti o seleziona combinazioni già esprimibili?
>
> **Lascia aperto:** la conclusione è il nativismo radicale dei concetti — che Fodor accettava e quasi nessun altro. È precisamente la conclusione che questa ricerca vuole mettere alla prova.

**★ Piattelli-Palmarini, M. (a cura di) (1980).** *Language and Learning: The Debate between Jean Piaget and Noam Chomsky*. Harvard University Press. `[M]` 🔵

> **Il libro più vicino alla domanda.** Atti di Royaumont, 1975. *Un sistema può generare strutture più potenti di quelle che possiede?* Piaget dice sì, Fodor risponde con l'argomento sopra, e trecento pagine di disaccordo. Esiste in italiano.
>
> In forma: è possibile $R_0 \rightarrow R_1$ con $\operatorname{ExpressivePower}(R_1) > \operatorname{ExpressivePower}(R_0)$?
>
> **Lascia aperto:** formula magnificamente il problema, non produce un meccanismo computazionale.

**Piaget, J.** *Genetic Epistemology*; *Biology and Knowledge*. `[M]` 🔒

> Utile come fonte primaria, non solo attraverso il dibattito con Chomsky e Fodor. La conoscenza come risultato di costruzione e riorganizzazione: come può una struttura cognitiva inizialmente più povera trasformarsi in una capace di operazioni che prima non possedeva? Radice del ramo *costruttivismo → Carey → Drescher*.
>
> **Lascia aperto:** un quadro dello sviluppo cognitivo, non un'architettura formalmente specificata.

---

## 5. Discontinuità concettuale e costruzione di nuove rappresentazioni

**★ Carey, S. (2009).** *The Origin of Concepts*. Oxford University Press. `[M]` ⚪

> Affronta direttamente la possibilità che durante lo sviluppo emergano sistemi rappresentazionali con potere espressivo non riducibile al precedente. Il meccanismo proposto è il **Quinian bootstrapping**. Il passaggio $R_0 \rightarrow R_1$ non è accumulo di casi ma **riorganizzazione concettuale**.
>
> Se questa forma di sviluppo è possibile nella cognizione umana, la domanda per l'AI diventa: quali condizioni architetturali permetterebbero a un sistema artificiale di modificare il proprio spazio rappresentazionale?
>
> **Lascia aperto:** è una teoria dello sviluppo umano, non dell'autonomia rappresentazionale di un sistema artificiale.

**★ Drescher, G. (1991).** *Made-Up Minds: A Constructivist Approach to Artificial Intelligence*. MIT Press. `[M]` 🟢/🔵

> Prova a trasformare il costruttivismo piagetiano in un sistema computazionale: non discute filosoficamente la costruzione dei concetti, progetta un meccanismo che costruisce **schemi** attraverso l'interazione.
>
> Colma il vuoto tra «perché l'acquisizione di concetti è problematica» e «come costruire una macchina che sviluppa le proprie strutture». È il ponte *Piaget → Carey → architettura computazionale*, e probabilmente l'aggiunta più importante dell'intera bibliografia.
>
> **Lascia aperto:** costruire strutture non implica produrre **nuovi primitivi radicalmente non specificati**, né possedere criteri propri di rilevanza.

**Torretti, R.** *Creative Understanding: Philosophical Reflections on Physics*. University of Chicago Press. `[M]` ⚪

> Porta il problema della novità concettuale nel contesto della scienza: come cambiano i concetti scientifici, e come può avvenire vera innovazione concettuale. Mostra che la costruzione di nuove rappresentazioni non è solo un problema dello sviluppo infantile.
>
> **Lascia aperto:** descrive l'innovazione concettuale umana, non fornisce un algoritmo che la produca.

**Hofstadter, D. & Fluid Analogies Research Group.** *Fluid Concepts and Creative Analogies*. `[M]` ⚪/🔒

> Problema vicino ma distinto: la capacità di **ristrutturare dinamicamente uno spazio concettuale**. Copycat è interessante perché le categorie non sono rigide — la rappresentazione del problema cambia durante la soluzione: *rappresentazione iniziale → ristrutturazione → nuova interpretazione*.
>
> **Lascia aperto:** la fluidità concettuale non equivale ancora a $p_{n+1}$ come nuovo primitivo indipendente dallo spazio progettato.

---

## 6. Grounding — quando una rappresentazione significa qualcosa

**★ Harnad, S. (1990).** *The Symbol Grounding Problem*. Physica D 42: 335–346. `[M]` 🟢

> Come può il significato di un simbolo essere intrinseco al sistema invece di dipendere da un interprete esterno? Se ogni simbolo è definito solo attraverso altri simboli si ottiene una rete formalmente coerente ma priva di collegamento non simbolico col mondo: collegare simboli ad altri simboli non basta.
>
> Introduce la distinzione decisiva tra **rappresentazione assegnata dall'osservatore** e **rappresentazione con funzione effettiva nell'organizzazione dell'agente**. La domanda non è solo come nasca una nuova rappresentazione, ma come acquisti significato.
>
> **Lascia aperto:** il grounding collega rappresentazioni ed esperienza, ma non risolve la **normatività autonoma**. Perché una distinzione dovrebbe *contare* per il sistema?

**★ Bickhard, M.H. (1993).** *Representational Content in Humans and Machines*. Journal of Experimental and Theoretical Artificial Intelligence 5: 285–333. `[M]` 🟢

> Contro la teoria della corrispondenza: una correlazione tra stato interno e oggetto esterno non basta a fare una rappresentazione **per il sistema** — la correlazione è visibile solo a noi. Nel modello interattivista il contenuto è legato alle *possibilità di interazione*: non «oggetto esterno → codifica interna» ma «organizzazione dell'interazione possibile».
>
> Questo introduce la possibilità dell'**errore** — il sistema anticipa un'interazione che poi fallisce — e con essa una normatività interna alla dinamica del sistema. È il ponte naturale tra rappresentazione, agency, interazione, normatività ed emergenza.
>
> **Lascia aperto:** resta da mostrare fin dove questa impostazione produca vera espansione open-ended dello spazio rappresentazionale.

**Pattee, H. (2001).** *The physics of symbols: bridging the epistemic cut*. BioSystems 60: 5–21. `[M]`

> La stessa domanda dal lato fisico: come una configurazione di materia diventa un simbolo per il sistema di cui fa parte.

**Rosen, R. (1991).** *Life Itself*. Columbia University Press. `[M]`

> Il più ambizioso e il più difficile. Chiusura alla causalità efficiente come criterio del vivente.

---

## 7. Normatività, agency, autonomia

*L'asse che la tradizione A non ha.*

**Ashby, W.R.** *Design for a Brain*. `[M]` 🔵/🟡

> Una delle radici cibernetiche del problema. Il punto non è più rappresentare il mondo, ma mantenere certe variabili entro regioni compatibili col funzionamento del sistema: *regolazione → adattamento → auto-organizzazione → autonomia*.
>
> Introduce una domanda che Goodman e Fodor da soli non possono porre: **una categoria potrebbe diventare rilevante perché permette al sistema di mantenere la propria organizzazione?**
>
> **Lascia aperto:** l'adattamento non equivale alla formazione di nuovi concetti.

**Maturana, H. & Varela, F. (1980).** *Autopoiesis and Cognition: The Realization of the Living*. D. Reidel. `[M]`

> Un vivente non persegue un obiettivo assegnato dall'esterno: è una rete di processi che produce e rigenera la propria organizzazione.

**★ Varela, F. (1979).** *Principles of Biological Autonomy*. North Holland. Nuova edizione annotata MIT Press, 2025. `[M]` 🟢

> Il testo interamente dedicato all'autonomia in senso costitutivo, non operativo. Con Varela la domanda non è più «come può un sistema costruire rappresentazioni?» ma **«che cosa rende un sistema autonomo?»** — e la rilevanza viene legata all'organizzazione stessa dell'agente: *autonomia → normatività → rilevanza*.
>
> Una distinzione conterebbe non perché scelta dal progettista, ma perché ha conseguenze per la continuità dell'organizzazione del sistema.
>
> **Lascia aperto:** l'autonomia biologica non mostra come nascano nuovi simboli o nuovi primitivi concettuali.

**Bickhard, M.H. (2000).** *Autonomy, Function, and Representation*. Communication and Cognition – AI 17(3–4): 111–131. `[M]` 🟢

> Il passaggio dalla rappresentazione all'autonomia. Come possano emergere funzione e normatività: **ciò che è buono o cattivo per il sistema non deve essere definito da un osservatore esterno.**

**Barandiaran, X., Di Paolo, E. & Rohde, M. (2009).** *Defining Agency: Individuality, Normativity, Asymmetry, and Spatio-temporality in Action*. Adaptive Behavior 17(5): 367–386. `[M]`

> Il tentativo più rigoroso di definire cosa serva per essere un agente: individualità, interazione asimmetrica, normatività.

---

## 8. Enattivismo e corpo

**Varela, F., Thompson, E. & Rosch, E. (1991).** *The Embodied Mind*. MIT Press. Ed. riveduta 2017. `[M]` ⚪

> Il libro fondativo. La cognizione non è mondo → input → rappresentazione → output, ma emerge dalla relazione continua tra organismo, corpo, ambiente e azione. La tesi che conta qui: **il mondo rilevante per un agente non deve essere interamente predefinito**, può emergere dall'interazione.
>
> **Lascia aperto:** difficile trasformare l'enattivismo in un meccanismo computazionale preciso che spieghi l'origine di nuove categorie formali.

**Pfeifer, R. & Bongard, J. (2006).** *How the Body Shapes the Way We Think*. MIT Press. `[M]`

> La versione robotica: morfologia e interazione come parti costitutive dell'intelligenza, non come contorno.

**Froese, T. & Ziemke, T. (2009).** *Enactive artificial intelligence: Investigating the systemic organization of life and mind*. Artificial Intelligence 173(3): 466–500. `[V]`

> **Il ponte.** L'enattivismo portato dentro la rivista *Artificial Intelligence*, non in una rivista di scienze cognitive. Il posto giusto da cui entrare se si viene dal lato tecnico.

**★ Di Paolo, E., Buhrmann, T. & Barandiaran, X. (2017).** *Sensorimotor Life: An Enactive Proposal*. Oxford University Press. `[M]` 🟢

> La sintesi contemporanea più completa del rapporto tra autonomia, agency, normatività, corpo, interazione sensomotoria e produzione di significato. Rende la domanda più forte: non «come si genera un nuovo concetto?» ma **«come nasce una nuova distinzione che abbia significato e rilevanza per l'agente?»** — cioè *nuova distinzione + rilevanza + possibilità d'azione*.
>
> **Lascia aperto:** spiega la significatività per l'agente, meno direttamente la nascita di un **nuovo primitivo computazionale**.

---

## 9. Nuovi primitivi — un sistema può estendere il proprio alfabeto?

*Il cuore della domanda, e la parte con meno letteratura. Cariani va letto **in parallelo a tutte le altre sezioni**, non come voce finale.*

Tutto scaricabile da `petercariani.com`. 🟢

**★ Cariani, P. (1989).** *On the Design of Devices with Emergent Semantic Functions*. Tesi di dottorato, SUNY Binghamton. `[V]`

> La tassonomia dei dispositivi adattivi, e la frase che riassume tutto: **i sistemi di IA possono essere solo tanto buoni quanto i criteri di rilevanza dei loro progettisti.** Per il nucleo della domanda è probabilmente il testo gratuito più importante da scaricare subito.

**★ Cariani, P. (1991).** *Emergence and artificial life*. In Langton, C.G. et al. (a cura di), *Artificial Life II*, Addison-Wesley, 775–798. `[V]`

> La distinzione centrale, e la formulazione più vicina alla domanda tecnica di questa bibliografia:
>
> **Emergenza combinatoria** — il sistema possiede $P = \{p_1,\ldots,p_n\}$ e genera nuove configurazioni $f(P)$. La complessità può diventare enorme, il vocabolario resta quello iniziale.
>
> **Emergenza creativa** — il sistema passa a $P' = \{p_1,\ldots,p_n,p_{n+1}\}$, dove compare un nuovo tipo di distinzione o un nuovo osservabile.
>
> La tesi: la computazione pura fa la prima, non la seconda. Il problema si sposta dal piano concettuale a quello **epistemico e operativo** — può un sistema costruire nuovi modi di misurare, distinguere e interagire?
>
> **Lascia aperto:** come distinguere una reale espansione dello spazio epistemico da una trasformazione già implicitamente prevista dal meta-spazio progettato dall'esterno.

**Cariani, P. (1991).** *Some epistemological implications of devices which construct their own sensors and effectors*. In Varela, F. & Bourgine, P. (a cura di), *Towards a Practice of Autonomous Systems*, MIT Press, 484–493. `[V]`

> Il punto di contatto con la tradizione B: pubblicato nel volume di Varela. → [sintesi ragionata](cariani-1991-sintesi.md)

**Cariani, P. (1993).** *To evolve an ear: epistemological implications of Gordon Pask's electrochemical devices*. Systems Research 10(3): 19–33. `[V]`

> Il caso empirico. Il dispositivo di Pask si fa crescere le connessioni fino a distinguere due frequenze, senza che nessuno gli abbia dato «frequenza» come categoria. Che sia analogico e non computazionale **è** il punto.

**Cariani, P. (1998).** *Epistemic autonomy through adaptive sensing*. IEEE ISIC. `[V]`

> La versione compatta, venti pagine, se ne leggi una sola.

> ⚠️ La clausola «in assenza di stati nascosti all'osservatore» fa un lavoro pesante, quasi definitorio. E la via d'uscita — accoppiarsi alla materia analogica — sposta il problema fuori dal sistema più che risolverlo: se i primitivi vengono dal mondo, non è il sistema a crearli.

---

## 10. Open-endedness — la versione tecnica moderna

*Il campo che pone la domanda in forma costruttiva: perché non riusciamo a costruire un sistema che continui a produrre novità?*

La questione obbliga a distinguere un **grande spazio combinatorio** da uno **spazio capace di espandersi**. Non basta generare $10^{100}$ configurazioni se appartengono tutte allo stesso spazio ontologico iniziale; la domanda forte è $\Omega_0 \rightarrow \Omega_1 \rightarrow \Omega_2 \rightarrow \cdots$, dove cambia lo **spazio delle possibilità**. È la versione dinamica della distinzione di Cariani.

**Banzhaf, W. et al. (2016).** *Defining and simulating open-ended novelty: requirements, guidelines, and challenges*. Theory in Biosciences 135(3): 131–161. `[V]`

> **La tassonomia**: tre tipi di novità — *variazione, innovazione, emergenza* — più un meta-modello a livelli di struttura. È la distinzione di Cariani raffinata, in forma pubblicabile.

**Taylor, T. et al. (2016).** *Open-ended evolution: Perspectives from the OEE workshop in York*. Artificial Life 22(3): 408–423. `[V]`

**Packard, N. et al. (2019).** *An overview of open-ended evolution*. Artificial Life 25(1–2). `[V]` 🟢

> L'editoriale del numero speciale di *Artificial Life*, PDF libero su MIT Press. Il punto d'ingresso migliore al campo.

**Stanley, K.O. (2019).** *Why open-endedness matters*. Artificial Life 25(3): 232–235. `[V]`

> Il campo produce workshop e numeri speciali, non trattati. Non si scrive il libro definitivo su un fallimento in corso.

**Lehman, J. & Stanley, K.O. (2011).** *Abandoning objectives: Evolution through the search for novelty alone*. Evolutionary Computation 19(2): 189–223. `[V]`

> **Le funzioni obiettivo possono attivamente sviare la ricerca verso vicoli ciechi.** Cercare la sola novità comportamentale, ignorando l'obiettivo, spesso arriva più lontano. Risultato sperimentale con conseguenze per qualunque criterio di promozione.

**Stanley, K.O. & Lehman, J. (2015).** *Why Greatness Cannot Be Planned: The Myth of the Objective*. Springer. `[M]`

**Corominas-Murtra, B., Seoane, L. & Solé, R.** *Zipf's law, unbounded complexity and open-ended evolution*. arXiv:1612.01605. `[V]` 🟢

**Hughes, E. et al. (2024).** *Open-Endedness is Essential for Artificial Superhuman Intelligence*. ICML 2024, arXiv:2406.04268. `[V]`

> Definizione formale: un sistema è open-ended se, **dal punto di vista di un osservatore**, la sequenza di artefatti prodotti è insieme nuova e apprendibile. L'osservatore-dipendenza viene da Cariani, non citato.
>
> Segnala anche uno spostamento del campo da diagnosi a promessa. Leggerlo sapendolo.

> **Lascia aperto:** molti sistemi open-ended dipendono comunque da regole di evoluzione progettate, criteri esterni, ambienti artificialmente costruiti, meta-spazi prefissati. L'open-endedness non risolve automaticamente il problema dell'autonomia epistemica.

---

## 11. I libri sui limiti

**Dreyfus, H. (1972; ed. riveduta 1992, *What Computers Still Can't Do*).** MIT Press. `[V]`

> Il canonico. Contro l'IA simbolica da posizioni fenomenologiche: il sapere pratico non è rappresentabile in regole, il contesto non si formalizza. Deriso all'epoca, poi in larga parte confermato.

**Fodor, J. (2000).** *The Mind Doesn't Work That Way*. MIT Press. `[M]`

> L'abduzione richiede di valutare la rilevanza globale, e la rilevanza non è una proprietà locale del simbolo. Il problema della cornice come limite di principio.

**Roitblat, H.** *Algorithms Are Not Enough: Creating General Artificial Intelligence*. MIT Press. `[M]` ⚪

> Riporta la questione alla discussione sull'AGI. Il problema non è solo aumentare dati, calcolo, dimensione dei modelli: riguarda **come vengono costruite e modificate le rappresentazioni**. Permette la formulazione finale: *un sistema che opera sempre all'interno delle rappresentazioni, degli obiettivi e delle modalità di interazione stabilite dal progettista può essere epistemicamente autonomo?*
>
> **Lascia aperto:** critica i paradigmi esistenti, non fornisce un'alternativa architetturale.

**Landgrebe, J. & Smith, B. (2022).** *Why Machines Will Never Rule the World*. Routledge. `[V]`

> Il recente. Tesi forte, titolo che non aiuta a farla prendere sul serio. Smith è un ontologo di prima grandezza.

---

## 12. Dove la questione ricompare nel ML attuale

*Nessuno di questi cita le sezioni 6–9. È il punto.*

**★ Bengio, Y., Courville, A. & Vincent, P. (2013).** *Representation Learning: A Review and New Perspectives*. arXiv:1206.5538. `[V]` 🟢

> Il ponte verso il ML contemporaneo: il modello non apprende solo funzioni su feature progettate a mano, apprende rappresentazioni interne, costruendo $x \rightarrow z_1 \rightarrow \cdots \rightarrow z_n$. Già un passo oltre i sistemi simbolici a vocabolario interamente specificato.
>
> **Ma representation learning non equivale a conceptual innovation.** Una rete può trovare nuove coordinate latenti senza modificare il proprio spazio degli osservabili, i propri criteri di rilevanza, la propria funzione obiettivo, o il tipo di interazioni con cui acquisisce informazione.
>
> **Lascia aperto:** è qui che nasce la domanda sugli LLM. Rappresentazioni interne sempre più astratte sono vera espansione concettuale, o riorganizzazione entro uno spazio definito da architettura e obiettivo?

**★ Rafiee, B. & Sutton, R.S. (2026).** *Toward Enactive Artificial Intelligence*. arXiv:2605.24238. `[V]`

> **La novità che cambia il quadro.** Sutton — l'autore di Sutton & Barto — argomenta che l'IA mainstream, dai sistemi a regole agli LLM, ha trascurato l'interazione incarnata e la **normatività intrinseca**. Sostiene che l'RL mostri una risonanza strutturale con i principi enattivi, **avvertendo che non va scambiata per equivalenza teorica**.
>
> È il momento in cui la tradizione B entra nel discorso tecnico dalla porta principale.

**Ellis, K. et al. (2021).** *DreamCoder*. PLDI. `[M]`

> La libreria cresce davvero, ma vive **fuori** dal modello e si cerca per enumerazione. Crescita senza gradienti.

**Altabaa, A. et al. (2023).** *Abstractors and relational cross-attention*. arXiv:2304.00195. `[M]`

> Simboli **dentro** l'architettura, con cardinalità fissata a priori in un `nn.Parameter`. Il complemento esatto di DreamCoder.

**Macfarlane, M. et al. (2026).** *Gradient-Based Program Synthesis with Neurally Interpreted Languages*. arXiv:2604.18907, ICLR 2026. `[V]`

> Scopre autonomamente un vocabolario di primitive subsimboliche con esecutore differenziabile. Scopre **quali**; **quante** resta un iperparametro.

**Fu, Y. et al. (2026).** *DiscoLoop*. arXiv:2607.00341. `[V]`

> L'entità-ponte è quasi perfettamente decodificabile ma lo stato è **mal allineato** con l'embedding corrispondente. L'informazione c'è e non è utilizzabile come operando: la versione empirica esatta della distinzione della §1.

**Yu, A. et al. (2026).** *LatentSkill*. arXiv:2606.06087 · **ParametricSkills**, arXiv:2606.30015. `[V]`

> Due gruppi, stessa idea, venticinque giorni di distanza, senza citarsi. Utili come caso di studio su **cosa non è un simbolo**: il prodotto ha un dosaggio continuo, va tarato per task, e sovradosato porta il modello sotto il proprio baseline.

**Geiger, A. et al. (2023).** *Causal Abstraction: A Theoretical Foundation for Mechanistic Interpretability*. arXiv:2301.04709. `[M]`

> Il formalismo per chiedere se una rappresentazione faccia davvero lavoro causale. Le interchange intervention sono il test operativo che manca a tutti i lavori sopra.

---

# Parte II — La sintesi

## 13. La catena

La bibliografia si legge come una successione di problemi, ciascuno consegnato dal precedente.

| | autore | il problema che apre |
|---|---|---|
| 1 | **Carnap** | $\text{estensione} \neq \text{intensione}$ |
| 2 | **Goodman** | $D \not\Rightarrow$ un'unica generalizzazione |
| 3 | **Rice / Wolpert** | il criterio può guardare solo la forma, e nessun bias è universale |
| 4 | **Fodor** | se per apprendere un concetto devo già poterlo rappresentare, come nasce un concetto nuovo? |
| 5 | **Piaget / Carey** | forse $R_0 \rightarrow R_1$ con $\operatorname{ExpressivePower}(R_1) > \operatorname{ExpressivePower}(R_0)$ |
| 6 | **Drescher / Hofstadter** | si possono costruire sistemi che inventano schemi e ristrutturano — ma è innovazione o riorganizzazione entro un meta-spazio progettato? |
| 7 | **Harnad** | anche una nuova rappresentazione deve essere *grounded* |
| 8 | **Bickhard / Varela / Di Paolo** | il grounding non basta: servono significato, normatività, rilevanza, agency |
| 9 | **Cariani** | può il sistema costruire nuovi osservabili e nuovi modi di distinguere? |
| 10 | **Open-endedness** | e può continuare a farlo, senza che lo spazio sia già implicitamente definito? |
| 11 | **AI contemporanea** | le rappresentazioni emergenti nei Transformer sono innovazione concettuale, o emergenza combinatoria estremamente potente entro un regime definito dall'esterno? |

---

## 14. Le quattro condizioni

La formulazione «gli LLM non sanno astrarre» è troppo debole: gli LLM costruiscono rappresentazioni astratte e generalizzano in molti domini. La domanda teoricamente interessante si separa invece in quattro condizioni, che permettono di distinguere apprendimento, generalizzazione, astrazione, representation learning, composizione, ristrutturazione, innovazione concettuale e autonomia epistemica.

**A. Novità rappresentazionale** — il sistema produce una distinzione non riducibile banalmente a una combinazione delle categorie operative iniziali.

**B. Novità operativa** — la nuova distinzione modifica ciò che il sistema può misurare, prevedere o fare.

**C. Rilevanza autonoma** — la distinzione è selezionata non solo perché migliora una funzione obiettivo fissata dall'esterno, ma perché acquista rilevanza rispetto all'organizzazione e all'attività proprie del sistema.

**D. Espansione dello spazio epistemico** — il sistema non seleziona soltanto un punto entro $\Omega$, ma contribuisce a trasformare $\Omega_0 \rightarrow \Omega_1$.

---

## 15. Il quadrato teorico centrale

Ridotto a quattro autori:

$$
\boxed{
\text{Fodor} + \text{Carey} + \text{Cariani} + \text{Varela}
}
\qquad\text{ovvero}\qquad
\boxed{
\text{nuovi concetti} + \text{nuovi osservabili} + \text{autonomia} + \text{rilevanza}
}
$$

| autore | ruolo | domanda |
|---|---|---|
| **Fodor** | il problema | come può comparire un concetto che il sistema non possiede già? |
| **Carey** | la possibilità di una discontinuità | un sistema cognitivo può passare a strutture rappresentazionali più potenti? |
| **Cariani** | la formulazione operativa della novità | può comparire un nuovo osservabile che non appartiene al repertorio combinatorio precedente? |
| **Varela** | la rilevanza autonoma | può il criterio di ciò che conta emergere dall'organizzazione propria del sistema? |

---

## 16. Percorsi di lettura

### Se leggi tre cose

1. **Piattelli-Palmarini (1980)** — la domanda posta bene, discussa da persone in disaccordo
2. **Mitchell (1980)** — venti pagine gratuite, il ponte tra il problema filosofico e il ML
3. **Cariani (1998)** — la versione costruttiva, con tassonomia e dispositivo funzionante

Per il retrogusto amaro: **Rice (1953)**, due pagine sul perché le proprietà che contano non sono calcolabili.

### Percorso essenziale — 8 tappe

Non in ordine cronologico: seguendo il problema.

```
1. Carnap            intensione, estensione, rappresentazione
2. Goodman           dati ≠ regola determinata univocamente
3. Piattelli-Palm.   il conflitto costruzione vs strutture già disponibili (Fodor in parallelo)
4. Carey             vecchio sistema concettuale → nuovo sistema concettuale
5. Drescher          dalla teoria alla domanda architetturale
6. Harnad + Bickhard grounding + interazione + normatività
7. Varela            e se il criterio di rilevanza dipendesse dall'organizzazione del sistema?
8. Di Paolo et al.   autonomia + agency + significato + normatività
```

**Durante tutto il percorso: leggere Cariani in parallelo.**

### Percorso A — logico-computazionale

```
Carnap  →  Goodman  →  Mitchell  →  Rice  →  Fodor / Piattelli-Palmarini
        →  Cariani  →  Banzhaf et al.
```
*Da cosa significa un termine, a perché serve un bias, a cosa è calcolabile, a se i primitivi possano nascere.*

### Percorso B — enattivo-biologico

```
Putnam  →  Harnad  →  Bickhard (1993, 2000)  →  Barandiaran et al.
        →  Varela  →  Froese & Ziemke  →  Rafiee & Sutton
```
*Da dove sta il significato, a cosa lo ancora, a cosa rende un sistema un agente, a come rientra nell'IA.*

### Il punto di incontro

Chi ha tempo per uno solo dei due percorsi ma vuole vedere il confine: **Cariani (1991, in Varela & Bourgine)** e **Froese & Ziemke (2009)**. Sono i due testi che stanno fisicamente sulla giuntura.

### Percorso tecnico successivo

Chiarito il problema teorico, le aree contemporanee da attraversare:

representation learning · world models · object-centric learning · continual learning · meta-learning · causal representation learning · neuro-symbolic architectures · program synthesis / concept learning · open-ended learning · intrinsic motivation / empowerment · autonomous goal generation · developmental robotics

A quel punto la domanda diventa un programma sperimentale:

> **Quale modifica architetturale permetterebbe a un sistema non soltanto di apprendere rappresentazioni, ma di modificare i propri osservabili, costruire nuove variabili e riorganizzare autonomamente il proprio spazio dei problemi?**

---

## 17. La domanda, e cosa non è dimostrato

> **Quali condizioni sono necessarie affinché un sistema artificiale non si limiti a ottimizzare e ricombinare rappresentazioni entro uno spazio epistemico dato, ma possa costruire autonomamente nuovi osservabili, nuove distinzioni e nuovi criteri di rilevanza, modificando così lo spazio stesso entro cui apprende e agisce?**

Il problema profondo non è se un sistema sappia **astrarre**, ma distinguere l'*astrazione entro uno spazio dato* dalla *costruzione autonoma di un nuovo spazio di distinzioni*. Un sistema può essere estremamente potente nella prima operazione senza possedere la seconda.

**Nessuno dei testi elencati dimostra che i sistemi autonomi siano impossibili.** Quello che esiste è:

- un argomento logico che nega la possibilità di acquisire concetti nuovi (Fodor), la cui conclusione quasi nessuno accetta — il che di solito significa che una premessa è sbagliata, e nessuno ha mai indicato con sicurezza quale
- un argomento cibernetico che la circoscrive alla computazione pura (Cariani), con una clausola che fa molto lavoro
- un teorema che nega l'universalità ma non la possibilità (Wolpert)
- una tradizione che sposta il problema dalla rappresentazione alla normatività (Varela, Bickhard), e che ha una proposta ma non una dimostrazione
- un campo che ci prova da trent'anni e non ci riesce (open-endedness)

Ed è aperta anche la questione se le due tradizioni stiano parlando dello stesso problema. Il fatto che Sutton nel 2026 abbia scritto un paper enattivo — dopo quarant'anni passati dall'altra parte — è il segnale più forte che il confine si stia muovendo.

---

# Appendice A — Disponibilità dei testi

**Verifica web: 17 agosto 2026.** Questa sezione distingue **la disponibilità del testo** dalla sua importanza teorica.

### Legenda

- 🟢 **Open Access / autore** — testo completo reso disponibile ufficialmente dall'editore, dall'autore o da un repository istituzionale con accesso pubblico.
- 🔵 **Repository / archivio pubblico** — copia consultabile o scaricabile da un archivio universitario o bibliotecario; quando la licenza non è esplicita viene segnalato.
- 🟡 **Diritti non chiari** — scansione disponibile in un archivio pubblico, ma senza una licenza Open Access chiaramente indicata.
- 🔒 **Prestito digitale / accesso ristretto** — il volume è presente online, ma non come PDF liberamente scaricabile.
- ⚪ **Nessun full text gratuito verificato** — è disponibile l'edizione commerciale, un'anteprima o materiale sostitutivo.
- ⚠️ **Copie non ufficiali** — durante la ricerca risultano copie complete su mirror o siti di upload non ufficiali. La loro autorizzazione non è verificabile; per questo non vengono linkate direttamente.

> **Nota:** la situazione può cambiare nel tempo. Un link indicato come gratuito descrive ciò che era verificabile il 17 agosto 2026. La presenza di una scansione su Internet Archive o su un repository non implica automaticamente che l'opera sia Open Access.

### Riepilogo

| Testo | Stato | Migliore accesso gratuito verificato |
|---|---|---|
| Carnap — *Meaning and Necessity* | 🟡 | Internet Archive, scansione completa; record con `rights: Not Available` |
| Goodman — *Fact, Fiction, and Forecast* | 🔒 | Internet Archive / prestito digitale |
| Fodor — *The Language of Thought* | 🔒 | Internet Archive / accesso ristretto |
| Piattelli-Palmarini — *Language and Learning* | 🔵 | PDF completo in repository LMU München; licenza non evidente nel record |
| Piaget — *Genetic Epistemology* | 🔒 | Internet Archive / accesso ristretto |
| Carey — *The Origin of Concepts* | ⚪ | précis e articoli dell'autrice gratuiti; non il libro completo |
| Drescher — *Made-Up Minds* | 🟢/🔵 | tesi MIT del 1989 nel repository istituzionale; il libro MIT Press resta commerciale |
| Torretti — *Creative Understanding* | ⚪ | nessun OA completo verificato; copie non ufficiali esistono ma non sono linkate |
| Hofstadter/FARG — *Fluid Concepts and Creative Analogies* | ⚪/🔒 | cataloghi/archivi e materiali FARG; nessun OA completo ufficiale verificato |
| Harnad — *The Symbol Grounding Problem* | 🟢 | arXiv, PDF completo |
| Bickhard — *The Interactivist Model* | 🟢 | PDF sul sito universitario dell'autore |
| Ashby — *Design for a Brain* | 🔵/🟡 | Internet Archive, scansione completa scaricabile |
| Varela — *Principles of Biological Autonomy* | 🟢 | MIT Press Open Access, licenza CC BY-NC-ND |
| Varela, Thompson & Rosch — *The Embodied Mind* | ⚪ | MIT Press online/preview; non risulta OA completo |
| Di Paolo et al. — *Sensorimotor Life* | 🟢 | PDF completo messo a disposizione da Xabier Barandiaran |
| Cariani — lavori principali | 🟢 | PDF sul sito personale dell'autore, inclusa la tesi |
| Bengio et al. — *Representation Learning* | 🟢 | arXiv, PDF completo |
| Open-Ended Evolution / Open-Endedness | 🟢 | MIT Press / *Artificial Life*, PDF dell'editoriale 2019 |
| Roitblat — *Algorithms Are Not Enough* | ⚪ | MIT Press; nessun full text OA completo verificato |

### Dettaglio per testo

**Carnap — *Meaning and Necessity*** · 🟡 scansione completa, status dei diritti non chiaro
- <https://archive.org/details/in.ernet.dli.2015.46380> — Digital Library of India / Central Library, Delhi University. Il record indica `dc.rights: Not Available`.
- <https://archive.org/details/meaningandnecess033225mbp> — altra scansione bibliotecaria.
- ⚠️ Risultano copie su mirror non ufficiali; non vengono linkate.

**Goodman — *Fact, Fiction, and Forecast*** · 🔒 nessun PDF OA completo verificato
- <https://archive.org/details/factfictionforec0000good> — collezione di libri digitalizzati / print-disabled; l'accesso dipende dalle modalità di consultazione o prestito.
- ⚠️ Scansioni complete su siti di upload non ufficiali; non linkate.

**Fodor — *The Language of Thought*** · 🔒 accesso ristretto
- <https://archive.org/details/languageofthough0000fodo_z1l0> — record marcato `Access-restricted-item: true`.
- ⚠️ Copie non ufficiali esistono; non linkate.

**Piattelli-Palmarini — *Language and Learning*** · 🔵 PDF completo in repository universitario
- <https://epub.ub.uni-muenchen.de/2872/1/2872.pdf> — Ludwig-Maximilians-Universität München. Fonte istituzionale affidabile, ma nel record non è evidente una licenza CC/OA specifica.
- Per lo studio è una delle copie gratuite più utili dell'intera bibliografia.

**Piaget — *Genetic Epistemology* / *Biology and Knowledge*** · 🔒 accesso ristretto
- <https://archive.org/details/geneticepistemol00piag> — `Access-restricted-item: true`.
- <https://archive.org/details/principlesofgene0000piag> — *The Principles of Genetic Epistemology*.
- Non è stata verificata un'edizione inglese completa e ufficialmente OA di *Biology and Knowledge*.

**Carey — *The Origin of Concepts*** · ⚪ libro non OA, ottimi sostituti gratuiti della stessa autrice
- *The Origin of Concepts: A Precis* — <https://pmc.ncbi.nlm.nih.gov/articles/PMC3489495/>
- *Concept Innateness, Concept Continuity, and Bootstrapping* — <https://pmc.ncbi.nlm.nih.gov/articles/PMC3528179/>
- Coprono core cognition, conceptual discontinuity e Quinian bootstrapping direttamente dall'autrice.

**Drescher — *Made-Up Minds*** · 🟢/🔵 la tesi MIT del 1989 è la scelta gratuita migliore
- Tesi MIT, stesso titolo, handle permanente: <http://hdl.handle.net/1721.1/77702> — contiene già il cuore dello schema mechanism e del progetto costruttivista.
- Anteprima MIT Press del libro (1991): <https://direct.mit.edu/books/monograph/2490/bookpreview-pdf/2395200>

**Torretti — *Creative Understanding*** · ⚪ nessun OA ufficiale
- <https://press.uchicago.edu/ucp/books/book/chicago/C/bo3636120.html> — PDF commerciale.
- ⚠️ Copie complete su mirror non ufficiali; non linkate.

**Hofstadter & FARG — *Fluid Concepts and Creative Analogies*** · ⚪/🔒 nessuna edizione OA ufficiale
- <https://openlibrary.org/books/OL1432732M/Fluid_concepts_creative_analogies> — catalogo, può indicare modalità di prestito.
- <https://github.com/eraoul/Fluid-Concepts-and-Creative-Analogies> — repository non ufficiale, utile per **codice e materiali FARG**, non come fonte del PDF.

**Harnad — *The Symbol Grounding Problem*** · 🟢 gratuito
- arXiv: <https://arxiv.org/abs/cs/9906002> · PDF: <https://arxiv.org/pdf/cs/9906002>
- Anche sul sito dell'autore: <https://www.southampton.ac.uk/~harnad/Papers/Harnad/harnad90.sgproblem.html>

**Bickhard — modello interattivista** · 🟢 disponibile dal sito dell'autore
- *The Interactivist Model*: <https://www.lehigh.edu/~mhb0/SyntheseInteractModel3Aug07.pdf>
- *Autonomy, Function, and Representation* (HTML): <https://www.lehigh.edu/~mhb0/autfuncrep.html>
- Pagina pubblicazioni: <https://www.lehigh.edu/~mhb0/pubspage.html>

**Ashby — *Design for a Brain*** · 🔵/🟡 scansione completa scaricabile
- <https://archive.org/details/designforbrain00ashb> — PDF e altri formati.
- Edizione commerciale con DOI: <https://link.springer.com/book/10.1007/978-94-015-1320-3>

**Varela — *Principles of Biological Autonomy*** · 🟢 Open Access ufficiale, **licenza CC BY-NC-ND**
- <https://direct.mit.edu/books/oa-monograph/5965/Principles-of-Biological-Autonomy>
- <https://mitpress.mit.edu/9780262551403/principles-of-biological-autonomy/>
- Il caso migliore dell'intera bibliografia: libro completo, editore ufficiale, licenza dichiarata.

**Varela, Thompson & Rosch — *The Embodied Mind*** · ⚪ non risulta OA completo
- Ed. originale: <https://direct.mit.edu/books/monograph/3956/The-Embodied-MindCognitive-Science-and-Human>
- Ed. rivista: <https://direct.mit.edu/books/monograph/4061/The-Embodied-MindCognitive-Science-and-Human>
- MIT Press espone anteprime e in alcuni casi capitoli consultabili, ma non è marcato OA come *Principles of Biological Autonomy*.

**Di Paolo, Buhrmann & Barandiaran — *Sensorimotor Life*** · 🟢 PDF completo da uno degli autori
- <https://xabier.barandiaran.net/2020/06/24/sensorimotor-life-an-enactive-proposal-the-book/> — la pagina dichiara esplicitamente il download disponibile.
- Edizione Oxford Academic: <https://academic.oup.com/book/5967>

**Cariani — lavori principali** · 🟢 l'autore rende disponibili molti dei propri lavori
- Pubblicazioni: <https://petercariani.com/Publications.html> · Cybernetics/emergence: <https://petercariani.com/Cybernetics.html>
- Tesi 1989 (il testo gratuito più importante da scaricare subito): <https://petercariani.com/CarianiNewWebsite/Publications_files/CarianiPhDIntegrated1989.pdf>
- *Towards an Evolutionary Semiotics*: <https://petercariani.com/CarianiNewWebsite/Publications_files/EvolutionarySemiotics97.pdf>
- Copie locali in questo repo: [Cariani 1991](../../library/papers/Cariani_1991_ArtificialLife-II.pdf) · [Cariani 1998](../../library/papers/Cariani_1998.pdf)

**Bengio, Courville & Vincent — *Representation Learning*** · 🟢 preprint completo
- <https://arxiv.org/abs/1206.5538> · PDF: <https://arxiv.org/pdf/1206.5538>

**Open-Ended Evolution / Open-Endedness** · 🟢 molta letteratura fondamentale gratuita
- Packard et al., editoriale del numero speciale *Artificial Life* 25(1), 2019: <https://direct.mit.edu/artl/article/25/1/1/2910/Open-Ended-Evolution-and-Open-Endedness-Editorial> · PDF: <https://direct.mit.edu/artl/article-pdf/25/1/1/1667104/artl_e_00282.pdf>
- Corominas-Murtra, Seoane & Solé, *Zipf's law, unbounded complexity and open-ended evolution*: <https://arxiv.org/abs/1612.01605>
- È una delle aree in cui si può costruire una raccolta ampia usando quasi solo preprint gratuiti.

**Roitblat — *Algorithms Are Not Enough*** · ⚪ nessun full text OA verificato
- <https://direct.mit.edu/books/monograph/4957/Algorithms-Are-Not-EnoughCreating-General> — metadati e anteprime.

---

# Appendice B — Riferimenti, in ordine alfabetico

- Altabaa, A. et al. *Abstractors and relational cross-attention*. arXiv:2304.00195.
- Ashby, W. Ross. *Design for a Brain*.
- Banzhaf, W. et al. *Defining and simulating open-ended novelty*. Theory in Biosciences 135(3), 2016.
- Barandiaran, X., Di Paolo, E. & Rohde, M. *Defining Agency*. Adaptive Behavior 17(5), 2009.
- Bengio, Y., Courville, A. & Vincent, P. *Representation Learning: A Review and New Perspectives*. arXiv:1206.5538.
- Bickhard, M.H. *Representational Content in Humans and Machines*. JETAI 5, 1993.
- Bickhard, M.H. *Autonomy, Function, and Representation*. Communication and Cognition – AI 17(3–4), 2000.
- Blum, M. *A machine-independent theory of the complexity of recursive functions*. JACM 14(2), 1967.
- Carey, S. *The Origin of Concepts*. Oxford University Press.
- Cariani, P. *On the Design of Devices with Emergent Semantic Functions*. Tesi, SUNY Binghamton, 1989.
- Cariani, P. *Emergence and artificial life*. In *Artificial Life II*, 1991.
- Cariani, P. *Some epistemological implications of devices which construct their own sensors and effectors*. In Varela & Bourgine, 1991.
- Cariani, P. *To evolve an ear*. Systems Research 10(3), 1993.
- Cariani, P. *Epistemic autonomy through adaptive sensing*. IEEE ISIC, 1998.
- Carnap, R. *Meaning and Necessity*. University of Chicago Press, 1947.
- Corominas-Murtra, B., Seoane, L. & Solé, R. *Zipf's law, unbounded complexity and open-ended evolution*. arXiv:1612.01605.
- Di Paolo, E., Buhrmann, T. & Barandiaran, X. *Sensorimotor Life: An Enactive Proposal*. Oxford UP, 2017.
- Drescher, G. *Made-Up Minds: A Constructivist Approach to Artificial Intelligence*. MIT Press, 1991.
- Dreyfus, H. *What Computers Still Can't Do*. MIT Press, 1992 (orig. 1972).
- Ellis, K. et al. *DreamCoder*. PLDI 2021.
- Fodor, J. *The Language of Thought*. Harvard University Press, 1975.
- Fodor, J. *The Mind Doesn't Work That Way*. MIT Press, 2000.
- Frege, G. *Über Sinn und Bedeutung*. 1892.
- Froese, T. & Ziemke, T. *Enactive artificial intelligence*. Artificial Intelligence 173(3), 2009.
- Fu, Y. et al. *DiscoLoop*. arXiv:2607.00341.
- Geiger, A. et al. *Causal Abstraction*. arXiv:2301.04709.
- Goodman, N. *Fact, Fiction, and Forecast*. Harvard University Press, 1955.
- Harnad, S. *The Symbol Grounding Problem*. Physica D 42, 1990.
- Hofstadter, D. & FARG. *Fluid Concepts and Creative Analogies*.
- Hughes, E. et al. *Open-Endedness is Essential for Artificial Superhuman Intelligence*. ICML 2024.
- Kripke, S. *Naming and Necessity*. Harvard University Press, 1980.
- Landgrebe, J. & Smith, B. *Why Machines Will Never Rule the World*. Routledge, 2022.
- Lehman, J. & Stanley, K.O. *Abandoning objectives*. Evolutionary Computation 19(2), 2011.
- Levin, L. *Universal sequential search problems*. 1973.
- Macfarlane, M. et al. *Gradient-Based Program Synthesis with Neurally Interpreted Languages*. ICLR 2026.
- Martin-Löf, P. *Intuitionistic Type Theory*. Bibliopolis, 1984.
- Maturana, H. & Varela, F. *Autopoiesis and Cognition*. D. Reidel, 1980.
- Mitchell, T.M. *The Need for Biases in Learning Generalizations*. Rutgers, 1980.
- Packard, N. et al. *An overview of open-ended evolution*. Artificial Life 25, 2019.
- Pattee, H. *The physics of symbols*. BioSystems 60, 2001.
- Pfeifer, R. & Bongard, J. *How the Body Shapes the Way We Think*. MIT Press, 2006.
- Piaget, J. *Genetic Epistemology*; *Biology and Knowledge*.
- Piattelli-Palmarini, M. (ed.) *Language and Learning*. Harvard University Press, 1980.
- Putnam, H. *The Meaning of "Meaning"*. 1975.
- Quine, W.V.O. *Two Dogmas of Empiricism*. Philosophical Review 60(1), 1951.
- Rafiee, B. & Sutton, R.S. *Toward Enactive Artificial Intelligence*. arXiv:2605.24238.
- Rice, H.G. *Classes of recursively enumerable sets and their decision problems*. 1953.
- Roitblat, H. *Algorithms Are Not Enough*. MIT Press.
- Rosen, R. *Life Itself*. Columbia University Press, 1991.
- Stanley, K.O. *Why open-endedness matters*. Artificial Life 25(3), 2019.
- Stanley, K.O. & Lehman, J. *Why Greatness Cannot Be Planned*. Springer, 2015.
- Taylor, T. et al. *Open-ended evolution: Perspectives from the OEE workshop in York*. Artificial Life 22(3), 2016.
- Torretti, R. *Creative Understanding*. University of Chicago Press.
- Varela, F. *Principles of Biological Autonomy*. North Holland, 1979 · MIT Press, 2025.
- Varela, F., Thompson, E. & Rosch, E. *The Embodied Mind*. MIT Press, 1991.
- Wolpert, D. *The lack of a priori distinctions between learning algorithms*. Neural Computation 8(7), 1996.
- Wolpert, D. & Macready, W. *No Free Lunch Theorems for Optimization*. IEEE TEC 1(1), 1997.
- Yu, A. et al. *LatentSkill*, arXiv:2606.06087 · *ParametricSkills*, arXiv:2606.30015.
