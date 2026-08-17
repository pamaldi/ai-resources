# Intensione, estensione e i limiti dell'autonomia

## Bibliografia ragionata — versione unificata

Fusione di due bibliografie costruite indipendentemente. Si sono rivelate **complementari più che sovrapposte**, e la loro divergenza è già un'informazione: descrivono due tradizioni che pongono la stessa domanda e non si citano quasi mai.

| | asse |
|---|---|
| **A** — logico-computazionale | cosa è calcolabile, cosa è esprimibile, da dove vengono i primitivi |
| **B** — enattivo-biologico | cosa rende un sistema un agente, da dove viene la normatività |

> ⚠️ **Le due tradizioni non danno la stessa diagnosi.** Vedere §0.

**Provenienza**: `[V]` verificato in rete · `[M]` citato a memoria, da confermare prima dell'uso formale

---

## 0. Il disaccordo, prima delle liste

Vale la pena metterlo in cima, perché altrimenti la bibliografia sembra un percorso unico e non lo è.

**La diagnosi A**: il limite è formale. Non puoi imparare un concetto che non sai esprimere (Fodor); le proprietà che contano sono indecidibili (Rice); nessun algoritmo è universalmente migliore (Wolpert); la computazione ricombina primitivi ma non li crea (Cariani).

**La diagnosi B**: il limite è che ai sistemi attuali **non importa niente**. Manca la normatività intrinseca — condizioni che siano migliori o peggiori *per il sistema stesso*. Un sistema che si auto-produce ce l'ha per costruzione (Varela, Bickhard, Barandiaran).

Non sono compatibili. Un enattivista risponderebbe che il teorema di Rice è fuori bersaglio perché presuppone ancora che la cognizione sia computazione su rappresentazioni. Un fodoriano risponderebbe che l'autopoiesi spiega perché un sistema *persiste*, non come acquisisce un *concetto*.

**Chi sta in mezzo**: Cariani pubblica nel volume curato da Varela e Bourgine, ma il suo argomento è semiotico-computazionale. È il punto di contatto più vicino esistente, e il fatto che sia una singola persona invece di una letteratura dice quanto il ponte sia sottile.

---

## 0-bis. Le definizioni

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
| Cariani (§5) | — | ottimizzazione **delle** categorie vs **dentro** le categorie |
| Carnap | estensione | intensione + stati possibili |

L'ultima riga di Cariani non è un sinonimo delle altre, ma vi si aggancia: la sua ricerca **semantica** riguarda quali distinzioni esistano — cioè quale estensione sia raggiungibile — mentre la ricerca **sintattica** opera dentro un vocabolario dato.

### Un avvertimento

I termini sono usati in modi non sempre coincidenti nelle diverse tradizioni. In logica modale «intensione» ha un senso tecnico preciso (funzione dai mondi possibili alle estensioni, Carnap); in informatica è più informale e significa «riguardante la forma del programma»; in filosofia della mente si sovrappone parzialmente a *contenuto*.

**Non sono la stessa nozione**, e chi le tratta come tali produce equivoci. La famiglia di somiglianza è reale; l'identità no.

### Riferimenti per questa sezione

**Le definizioni.** Estensione e intensione nella forma qui usata vengono da **Carnap (1947)**, §1; il precedente è **Frege (1892)**. Per una voce enciclopedica aggiornata e gratuita: *Intensional Logic* e *Reference* nella **Stanford Encyclopedia of Philosophy** (`plato.stanford.edu`) — è il punto di ingresso migliore se non si vuole partire dai classici. `[M]`

**Il rapporto tra intensione e possibilità.** Il senso tecnico stretto — l'intensione come funzione dai mondi possibili alle estensioni — è di Carnap ed è ripreso in **Montague (1970), *Universal Grammar*** e nella semantica formale successiva. `[M]`

**L'uguaglianza estensionale tra programmi.** La distinzione è standard in teoria dei linguaggi di programmazione; l'esposizione canonica sta in **Pierce, *Types and Programming Languages*** (MIT Press, 2002), sui capitoli dedicati all'equivalenza contestuale. Per il lato teoria dei tipi, **Martin-Löf (1984)**, già in §1. `[M]`

**Il teorema di Rice.** **Rice (1953)**, già citato in §3. Per l'enunciato con dimostrazione: **Sipser, *Introduction to the Theory of Computation***, oppure **Rogers, *Theory of Recursive Functions and Effective Computability*** (1967) per la trattazione completa. `[M]`

**Il costo intensionale dentro un criterio induttivo.** **Levin (1973)** e lo **speed prior** di **Schmidhuber (2002)**, entrambi in §3 — sono i due posti in cui il numero di passi entra formalmente nella selezione dell'ipotesi invece di restarne fuori.

> ⚠️ **Nota di provenienza.** Le definizioni e i teoremi citati sopra sono standard. Non lo sono due cose in questa sezione, che vanno lette come rielaborazione e non come dottrina:
>
> — **l'esempio `mult` contro addizione ripetuta** è una formulazione di lavoro, non un esempio canonico della letteratura;
> — **la tabella delle coppie imparentate** è un allineamento costruito qui. Le corrispondenze sono difendibili una per una, ma nessun autore le mette in fila così, e la riga su Cariani vi si aggancia solo per analogia.

## 1. La distinzione

**Frege, G. (1892).** *Über Sinn und Bedeutung*. Zeitschrift für Philosophie und philosophische Kritik 100: 25–50. `[M]`

> L'origine. Riferimento contro senso: stessa cosa indicata, modo di presentarla diverso. Scoprire che stella del mattino e stella della sera coincidono è stata astronomia, non logica.

**Carnap, R. (1947).** *Meaning and Necessity: A Study in Semantics and Modal Logic*. University of Chicago Press. `[M]`

> Il testo classico più diretto. Estensione = l'insieme che soddisfa il predicato; intensione = la regola che decide l'appartenenza. **Due regole diverse possono selezionare lo stesso insieme.**

**Kripke, S. (1980).** *Naming and Necessity*. Harvard University Press. `[M]`

> Possedere una descrizione di qualcosa e riuscire a riferirsi a quella cosa non sono la stessa operazione.

**Putnam, H. (1975).** *The Meaning of "Meaning"*. In *Mind, Language and Reality*, Cambridge University Press, 215–271. `[M]`

> Twin Earth: il significato non è determinato dagli stati interni. È il primo punto in cui l'ambiente entra dentro il contenuto semantico — e da lì si arriva al grounding.

**Quine, W.V.O. (1951).** *Two Dogmas of Empiricism*. Philosophical Review 60(1): 20–43. `[M]`

> Il contraltare estensionalista: se il significato non si riduce all'estensione, non è chiaro che sia qualcosa. La distinzione non è pacifica.

**Martin-Löf, P. (1984).** *Intuitionistic Type Theory*. Bibliopolis. `[M]`

> La versione viva e operativa: uguaglianza *definizionale* (stessa forma normale) contro *proposizionale* (esiste una dimostrazione). Spina dorsale di Coq, Agda, Lean.

---

## 2. Dai casi alla regola — il problema dell'induzione

**Goodman, N. (1955).** *Fact, Fiction, and Forecast*. Harvard University Press. `[M]`

> **Il nuovo enigma dell'induzione.** Gli stessi dati sono compatibili con generalizzazioni molto diverse; la domanda diventa perché alcune categorie ci sembrano naturali e altre arbitrarie. È il ponte obbligato tra la §1 e la §3.

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

## 4. Grounding — quando una rappresentazione significa qualcosa

**Harnad, S. (1990).** *The Symbol Grounding Problem*. Physica D 42: 335–346. `[M]`
`https://www.southampton.ac.uk/~harnad/Papers/Harnad/harnad90.sgproblem.html`

> Come può il significato di un simbolo essere intrinseco al sistema invece di dipendere da un interprete esterno? Collegare simboli ad altri simboli non basta: serve un ancoraggio non simbolico.

**Bickhard, M.H. (1993).** *Representational Content in Humans and Machines*. Journal of Experimental and Theoretical Artificial Intelligence 5: 285–333. `[M]`

> Contro la teoria della corrispondenza: una correlazione tra stato interno e oggetto esterno non basta a fare una rappresentazione **per il sistema**. La correlazione è visibile solo a noi.

**Pattee, H. (2001).** *The physics of symbols: bridging the epistemic cut*. BioSystems 60: 5–21. `[M]`

> La stessa domanda dal lato fisico: come una configurazione di materia diventa un simbolo per il sistema di cui fa parte.

**Rosen, R. (1991).** *Life Itself*. Columbia University Press. `[M]`

> Il più ambizioso e il più difficile. Chiusura alla causalità efficiente come criterio del vivente.

---

## 5. Nuovi primitivi — un sistema può estendere il proprio alfabeto?

*Il cuore della domanda, e la parte con meno letteratura.*

### Il lato filosofico

**Fodor, J. (1975).** *The Language of Thought*. Harvard University Press. `[M]`

> Imparare è formulare e testare ipotesi; un'ipotesi va formulata in un linguaggio; quindi **non puoi imparare un concetto che non eri già in grado di esprimere.** Conclusione: nativismo radicale dei concetti — che Fodor accettava e quasi nessun altro.

**Piattelli-Palmarini, M. (a cura di) (1980).** *Language and Learning: The Debate between Jean Piaget and Noam Chomsky*. Harvard University Press. `[M]`

> **Il libro più vicino alla domanda.** Atti di Royaumont, 1975. *Un sistema può generare strutture più potenti di quelle che possiede?* Piaget dice sì, Fodor risponde con l'argomento sopra, e trecento pagine di disaccordo. Esiste in italiano.

### Il lato cibernetico — Cariani

Tutto scaricabile da `petercariani.com`.

**Cariani, P. (1989).** *On the Design of Devices with Emergent Semantic Functions*. Tesi di dottorato, SUNY Binghamton. `[V]`

> La tassonomia dei dispositivi adattivi, e la frase che riassume tutto: **i sistemi di IA possono essere solo tanto buoni quanto i criteri di rilevanza dei loro progettisti.**

**Cariani, P. (1991).** *Emergence and artificial life*. In Langton, C.G. et al. (a cura di), *Artificial Life II*, Addison-Wesley, 775–798. `[V]`

> La distinzione centrale: **emergenza combinatoria** (nuove combinazioni di elementi esistenti) contro **emergenza creativa** (nuovi generi di elementi). E la tesi: la computazione pura fa la prima, non la seconda.

**Cariani, P. (1991).** *Some epistemological implications of devices which construct their own sensors and effectors*. In Varela, F. & Bourgine, P. (a cura di), *Towards a Practice of Autonomous Systems*, MIT Press, 484–493. `[V]`

> Il punto di contatto con la tradizione B: pubblicato nel volume di Varela.

**Cariani, P. (1993).** *To evolve an ear: epistemological implications of Gordon Pask's electrochemical devices*. Systems Research 10(3): 19–33. `[V]`

> Il caso empirico. Il dispositivo di Pask si fa crescere le connessioni fino a distinguere due frequenze, senza che nessuno gli abbia dato «frequenza» come categoria. Che sia analogico e non computazionale **è** il punto.

**Cariani, P. (1998).** *Epistemic autonomy through adaptive sensing*. IEEE ISIC. `[V]`

> La versione compatta, venti pagine, se ne leggi una sola.

> ⚠️ La clausola «in assenza di stati nascosti all'osservatore» fa un lavoro pesante, quasi definitorio. E la via d'uscita — accoppiarsi alla materia analogica — sposta il problema fuori dal sistema più che risolverlo: se i primitivi vengono dal mondo, non è il sistema a crearli.

---

## 6. Normatività, agency, autonomia

*L'asse che la tradizione A non ha.*

**Maturana, H. & Varela, F. (1980).** *Autopoiesis and Cognition: The Realization of the Living*. D. Reidel. `[M]`

> Un vivente non persegue un obiettivo assegnato dall'esterno: è una rete di processi che produce e rigenera la propria organizzazione.

**Varela, F. (1979).** *Principles of Biological Autonomy*. North Holland. Nuova edizione annotata MIT Press, 2025. `[M]`

> Il testo interamente dedicato all'autonomia, in senso costitutivo e non semplicemente operativo.

**Bickhard, M.H. (2000).** *Autonomy, Function, and Representation*. Communication and Cognition – AI 17(3–4): 111–131. `[M]`

> Il passaggio dalla rappresentazione all'autonomia. Come possano emergere funzione e normatività: **ciò che è buono o cattivo per il sistema non deve essere definito da un osservatore esterno.**

**Barandiaran, X., Di Paolo, E. & Rohde, M. (2009).** *Defining Agency: Individuality, Normativity, Asymmetry, and Spatio-temporality in Action*. Adaptive Behavior 17(5): 367–386. `[M]`

> Il tentativo più rigoroso di definire cosa serva per essere un agente: individualità, interazione asimmetrica, normatività.

---

## 7. Enattivismo e corpo

**Varela, F., Thompson, E. & Rosch, E. (1991).** *The Embodied Mind*. MIT Press. Ed. riveduta 2017. `[M]`

> Il libro fondativo. La cognizione non è mondo → input → rappresentazione → output, ma emerge dalla relazione continua tra organismo, corpo, ambiente e azione.

**Pfeifer, R. & Bongard, J. (2006).** *How the Body Shapes the Way We Think*. MIT Press. `[M]`

> La versione robotica: morfologia e interazione come parti costitutive dell'intelligenza, non come contorno.

**Froese, T. & Ziemke, T. (2009).** *Enactive artificial intelligence: Investigating the systemic organization of life and mind*. Artificial Intelligence 173(3): 466–500. `[V]`

> **Il ponte.** L'enattivismo portato dentro la rivista *Artificial Intelligence*, non in una rivista di scienze cognitive. Il posto giusto da cui entrare se si viene dal lato tecnico.

**Di Paolo, E., Buhrmann, T. & Barandiaran, X. (2017).** *Sensorimotor Life: An Enactive Proposal*. Oxford University Press. `[M]`

> La sintesi contemporanea che lega significato, agency, autonomia e interazione sensomotoria.

---

## 8. Open-endedness — la versione tecnica moderna

*Il campo che pone la domanda in forma costruttiva: perché non riusciamo a costruire un sistema che continui a produrre novità?*

**Banzhaf, W. et al. (2016).** *Defining and simulating open-ended novelty: requirements, guidelines, and challenges*. Theory in Biosciences 135(3): 131–161. `[V]`

> **La tassonomia**: tre tipi di novità — *variazione, innovazione, emergenza* — più un meta-modello a livelli di struttura. È la distinzione di Cariani raffinata, in forma pubblicabile.

**Taylor, T. et al. (2016).** *Open-ended evolution: Perspectives from the OEE workshop in York*. Artificial Life 22(3): 408–423. `[V]`

**Packard, N. et al. (2019).** *An overview of open-ended evolution*. Artificial Life 25(2): 93–103. `[V]`

**Stanley, K.O. (2019).** *Why open-endedness matters*. Artificial Life 25(3): 232–235. `[V]`

> Il campo produce workshop e numeri speciali, non trattati. Non si scrive il libro definitivo su un fallimento in corso.

**Lehman, J. & Stanley, K.O. (2011).** *Abandoning objectives: Evolution through the search for novelty alone*. Evolutionary Computation 19(2): 189–223. `[V]`

> **Le funzioni obiettivo possono attivamente sviare la ricerca verso vicoli ciechi.** Cercare la sola novità comportamentale, ignorando l'obiettivo, spesso arriva più lontano. Risultato sperimentale con conseguenze per qualunque criterio di promozione.

**Stanley, K.O. & Lehman, J. (2015).** *Why Greatness Cannot Be Planned: The Myth of the Objective*. Springer. `[M]`

**Hughes, E. et al. (2024).** *Open-Endedness is Essential for Artificial Superhuman Intelligence*. ICML 2024, arXiv:2406.04268. `[V]`

> Definizione formale: un sistema è open-ended se, **dal punto di vista di un osservatore**, la sequenza di artefatti prodotti è insieme nuova e apprendibile. L'osservatore-dipendenza viene da Cariani, non citato.
>
> Segnala anche uno spostamento del campo da diagnosi a promessa. Leggerlo sapendolo.

---

## 9. I libri sui limiti

**Dreyfus, H. (1972; ed. riveduta 1992, *What Computers Still Can't Do*).** MIT Press. `[V]`

> Il canonico. Contro l'IA simbolica da posizioni fenomenologiche: il sapere pratico non è rappresentabile in regole, il contesto non si formalizza. Deriso all'epoca, poi in larga parte confermato.

**Fodor, J. (2000).** *The Mind Doesn't Work That Way*. MIT Press. `[M]`

> L'abduzione richiede di valutare la rilevanza globale, e la rilevanza non è una proprietà locale del simbolo. Il problema della cornice come limite di principio.

**Landgrebe, J. & Smith, B. (2022).** *Why Machines Will Never Rule the World*. Routledge. `[V]`

> Il recente. Tesi forte, titolo che non aiuta a farla prendere sul serio. Smith è un ontologo di prima grandezza.

---

## 10. Dove la questione ricompare nel ML attuale

*Nessuno di questi cita le sezioni 4–7. È il punto.*

**Rafiee, B. & Sutton, R.S. (2026).** *Toward Enactive Artificial Intelligence*. arXiv:2605.24238. `[V]`

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

## 11. Percorsi di lettura

### Se leggi tre cose

1. **Piattelli-Palmarini (1980)** — la domanda posta bene, discussa da persone in disaccordo
2. **Mitchell (1980)** — venti pagine gratuite, il ponte tra il problema filosofico e il ML
3. **Cariani (1998)** — la versione costruttiva, con tassonomia e dispositivo funzionante

Per il retrogusto amaro: **Rice (1953)**, due pagine sul perché le proprietà che contano non sono calcolabili.

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

---

## 12. La domanda, e cosa non è dimostrato

> **Come può un sistema determinare autonomamente cosa distingue, cosa significa, cosa è rilevante e cosa ha valore?**

Nessuno dei testi elencati dimostra che i sistemi autonomi siano impossibili. Quello che esiste è:

- un argomento logico che nega la possibilità di acquisire concetti nuovi (Fodor), la cui conclusione quasi nessuno accetta — il che di solito significa che una premessa è sbagliata, e nessuno ha mai indicato con sicurezza quale
- un argomento cibernetico che la circoscrive alla computazione pura (Cariani), con una clausola che fa molto lavoro
- un teorema che nega l'universalità ma non la possibilità (Wolpert)
- una tradizione che sposta il problema dalla rappresentazione alla normatività (Varela, Bickhard), e che ha una proposta ma non una dimostrazione
- un campo che ci prova da trent'anni e non ci riesce (open-endedness)

Ed è aperta anche la questione se le due tradizioni stiano parlando dello stesso problema. Il fatto che Sutton nel 2026 abbia scritto un paper enattivo — dopo quarant'anni passati dall'altra parte — è il segnale più forte che il confine si stia muovendo.