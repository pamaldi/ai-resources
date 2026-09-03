# La mappa dei libri

**Note di lavoro — 31 luglio 2026.** Seguito della [sintesi su compressione e astrazione](sintesi-compressione-astrazione.md). La parte sui corsi di quelle stesse note è confluita in [formazione/corsi.md](../../formazione/corsi.md).

---

## 1. Premessa: il libro che copre tutto non esiste

La conversazione ha attraversato teoria dell'informazione, sintesi di programmi, neuroscienze del chunking, automi cellulari, filosofia della morfogenesi e strutture dati succinte. Nessuno ha scritto il libro che li tiene insieme.

Il buco preciso: **nessun libro tratta la scoperta autonoma di astrazioni verificate come problema unificato**. Esistono quattro monografie separate su quattro metà dello stesso problema — MDL (offline, senza agente), skill discovery (agentica, senza verifica), program synthesis (verificata, senza embodiment), neuroscienze del chunking (senza parametrizzazione).

---

## 2. I tre che coprono un terzo ciascuno

**MacKay — *Information Theory, Inference, and Learning Algorithms*** (Cambridge, 2003). Entropia, codifica aritmetica (il capitolo migliore che esista), inferenza bayesiana, Occam come conseguenza automatica della marginalizzazione, reti neurali. Esercizi risolti. **Gratis in PDF** — copia locale: [libri](../../libri/MacKay_Information-Theory-Inference-and-Learning-Algorithms.pdf)

**Melanie Mitchell — *Complexity: A Guided Tour*** (Oxford, 2009). Automi cellulari, computational mechanics, emergenza, informazione, evoluzione, Hofstadter sull'analogia. Mitchell **era nella stanza**: coautrice con Crutchfield sull'evoluzione dei CA. Divulgativo ma non annacquato. Copia locale: [libri](../../libri/Mitchell_Complexity-A-Guided-Tour.pdf)

**Hofstadter — *Gödel, Escher, Bach***. Livelli di descrizione, simboli che emergono da substrato, ricorsione, autoriferimento, la vespa Sphex. Nessuna matematica della compressione, ma pone *la domanda* nella forma giusta.

---

## 3. Per i singoli fili

| Filo | Libro |
|---|---|
| MDL a fondo | **Grünwald**, *The Minimum Description Length Principle* (MIT, 2007) |
| Kolmogorov, Solomonoff | **Li & Vitányi**, *An Introduction to Kolmogorov Complexity* (Springer, 4ª ed. 2019) |
| Perché i sistemi complessi sono gerarchici | **Simon**, *The Sciences of the Artificial* — il saggio *The Architecture of Complexity* è la teoria del chunking prima che avesse un nome |
| Numerosità e aritmetica nel cervello | **Dehaene**, *The Number Sense* — copia locale: [libri](../../libri/Dehaene_The-Number-Sense.pdf) |
| Astrazione dalla ripetizione, lato cognitivo | **Hofstadter & Sander**, *Surfaces and Essences* (2013) |
| Competenza senza comprensione | **Dennett**, *From Bacteria to Bach and Back* (2017) |
| RL e cervello | **Sutton & Barto**, capitoli 14–15 |
| Complessità algoritmica applicata | **Zenil, Kiani, Tegnér**, *Algorithmic Information Dynamics* (Cambridge, 2023) |
| Da dove viene l'aritmetica, cognitivamente | **Lakoff & Núñez**, *Where Mathematics Comes From* (2000) — da leggere col pacchetto di stroncature a fianco |

> Per la linea *testo pre-compresso / AI fisica* (Henrich, Bennett, Moravec, Clark) vedi la reading list dedicata: [testo-mondo-pre-compresso.md](testo-mondo-pre-compresso.md).

---

## 4. Lakoff & Narayanan, *The Neural Mind* (2025)

**Dati**: University of Chicago Press, 24 giugno 2025, 384 pagine, quattro capitoli lunghi. Lakoff = linguista cognitivo di Berkeley, noto per il lavoro sulle metafore. Narayanan = neuroscienziato computazionale a Google DeepMind.

**La tesi**: il pensiero non avviene neurone per neurone ma quando i neuroni formano circuiti e i circuiti semplici si combinano in complessi. I pensieri derivano la loro struttura dalla circuiteria usata anche per vista, tatto e udito. Le «metafore per cui viviamo» non sono astrazioni ma costrutti neurali incarnati.

**Perché è nella bibliografia di Gangemi**: il corso [Cognitive Semantics for AI](../../formazione/corsi.md) dichiara approccio 4E; questo libro è il manifesto contemporaneo di quella tradizione.

### Il punto di contatto vero

Il secondo capitolo: *dal controllo motorio al pensiero*, *la grande sorpresa: l'aspetto è controllo motorio*, *image schemas: partendo da Kant*, *pensare con gli schemi*.

Quel «l'aspetto è controllo motorio» è la tesi di dottorato di Narayanan: le **x-schemas** (schemi eseguibili basati su reti di Petri) modellano azioni motorie, e l'aspetto verbale (iniziare, continuare, completare, interrompere) risulta essere la stessa struttura di controllo. Cioè **schemi d'azione parametrici, formalmente specificati, che fungono da primitivi concettuali.**

Gli *image schemas* (CONTENITORE, PERCORSO, ORIGINE-PERCORSO-META, FORZA) sono candidati primitivi che pretendono di non essere scelti a mano ma **derivati dall'esperienza sensomotoria**. È una risposta alla domanda di Thom — da dove viene l'alfabeto? Lakoff: **viene dal corpo**. La stessa domanda, posta in forma logico-computazionale, è quella della [bibliografia intensione/autonomia](../intensione-autonomia/bibliografia.md).

### Le riserve

1. **Non c'è compressione, non c'è MDL, non c'è apprendimento formale.** Meccanismo = hebbiano + mappatura metaforica. Nessuna funzione obiettivo, nessun criterio di selezione tra schemi, nessuna verifica. Sta interamente dal lato «da dove vengono i primitivi», per niente dal lato «come si scopre un'astrazione nuova».
2. **Il programma di Lakoff è contestato**: la teoria della metafora concettuale è accusata da decenni di essere post-hoc e difficilmente falsificabile. Stessa critica che ha affondato Thom.
3. **Le blurb sono tutte in famiglia** (Núñez, Mark Johnson, Aziz-Zadeh). Nessuna voce esterna critica.

### Verdetto

Se si fa il corso di Gangemi: leggerlo, è il contesto. Se interessa la domanda sui primitivi: sfogliare il capitolo 2 (image schemas + parte di Narayanan sul motorio). Per il progetto: periferico.

---

## 5. Citare come strumento vs citare come legittimità

**Mettere Lakoff in bibliografia ≠ sposare Lakoff.** In un corso intitolato *Cognitive Semantics for AI* con approccio 4E dichiarato, è lettura canonica della tradizione esaminata — come Sutton & Barto in un corso di RL. Le altre voci della bibliografia sono lavori tecnici con implementazioni.

**Gangemi fa un mestiere diverso.** Lakoff fa teoria cognitiva difficilmente falsificabile; Gangemi fa knowledge engineering — ontologie, pattern, sistemi che girano, valutazione su competency question. Prendere dalla semantica cognitiva l'*ispirazione* su quali strutture rappresentare non lo rende responsabile della validità psicologica di quelle strutture. Un frame è utile se fa annotare e ragionare meglio, indipendentemente dal fatto che sia implementato in un circuito corticale.

**Anzi**: gli image schemas hanno un problema di falsificabilità *come teoria del cervello*, ma trasformati in pattern ontologici — strutture riusabili con vincoli espliciti — diventano valutabili. Gangemi ha dato all'intuizione di Lakoff un criterio di successo che Lakoff non aveva.

**Dove la critica morde**: quanta di questa ispirazione cognitiva fa lavoro *reale* nei sistemi? Se si togliesse l'apparato lakoffiano e si chiamassero le stesse strutture «schemi relazionali» senza pretese neurali, funzionerebbero uguale? Probabilmente sì — nel qual caso la cornice cognitiva è motivazione, non meccanismo.

### La lezione trasferibile

> Ci sono due modi di citare una tradizione: come **fonte di strumenti** (li usi, si vede) o come **fonte di legittimità** (li nomini, e basta). Il secondo è sempre attaccabile.

Se Graybiel, Schmidhuber o Crutchfield compaiono in un paper solo per dare profondità, un revisore lo nota. Se compaiono perché se ne è preso un criterio operativo, no.

**Domanda buona da fare a Gangemi, se capita**: non «cosa pensi di Lakoff», ma *come si valuta se un pattern cognitivamente ispirato stia davvero facendo lavoro nel sistema*.

---

## 6. Raccomandazioni

- **Non** leggere *The Neural Mind* per intero. Leggere invece **Lakoff & Núñez, *Where Mathematics Comes From*** — è sulla domanda giusta (da dove nasce la moltiplicazione, cognitivamente) — affiancato da **Dehaene** per la versione con i dati. Due libri che litigano sullo stesso tema sono il modo migliore di impararlo.
- **Se uno solo: MacKay, letto sul serio.** Non sfogliato: fatto, con gli esercizi, tre mesi. È l'unico che *cambia gli strumenti* invece di aggiungere riferimenti. Dopo, tutto il resto si legge più in fretta e con più giudizio — si riconosce al volo chi fa teoria dell'informazione seria e chi la evoca. Ed è gratis.

---

## 7. La cosa più importante

La conversazione è passata da Sphex a Elias-Fano a Thom a HashLife a Graybiel. C'è già **molta più ampiezza di quanta se ne possa usare**. Ogni nuovo agganciamento è gratificante e non costa niente — è la trappola specifica di chi è bravo a collegare: il collegamento dà la stessa soddisfazione della costruzione, a un decimo della fatica.

> **La cosa che darebbe di più adesso: scrivere le duecento righe di Python che scoprono `double` e falliscono a scoprire `mult`.** Non per il paper — per vedere dove *esattamente* si rompe. Si romperà in un punto che nessuna di queste letture ha fatto prevedere, e quel punto varrà più di altri dieci riferimenti bibliografici.

Poi si torna a Thom, che nel frattempo non scappa.

> Scritto a fine luglio 2026, quando il progetto che avrebbe dovuto contenere quelle duecento righe esisteva ancora. Il progetto è stato chiuso senza che venissero scritte — il che rende l'osservazione più vera, non meno.
