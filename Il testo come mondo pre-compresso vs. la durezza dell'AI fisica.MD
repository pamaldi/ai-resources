# Il testo come mondo pre-compresso vs. la durezza dell'AI fisica
### Reading list ragionata — libri e paper

**La tesi da possedere:** il testo non è dati grezzi ma il mondo già compresso da miliardi di cervelli umani (un token porta semantica gratis); l'AI fisica è difficile non perché "non si può tokenizzare il mondo", ma perché non esiste un corpus sensomotorio pre-digerito, i dati di interazione costano ordini di grandezza più del testo, e il closed loop cambia la natura del problema. È il paradosso di Moravec in versione moderna.

---

## Libri

### Fondamento: perché il linguaggio comprime

- **Joseph Henrich — *The Secret of Our Success* (2015)**
  Il libro singolo più importante per il "perché il testo è pre-digerito". Tesi: l'intelligenza individuale umana è sopravvalutata; la potenza viene dall'evoluzione culturale cumulativa — ogni generazione eredita conoscenza già distillata, e il linguaggio è il canale. È letteralmente la ragione per cui un token porta semantica gratis: qualcuno l'ha già pagata.

- **Michael Tomasello — *The Cultural Origins of Human Cognition* (1999)**
  La versione da psicologia dello sviluppo dello stesso argomento: il "ratchet effect" della trasmissione culturale. Complementare a Henrich, più focalizzato sui meccanismi cognitivi individuali (attenzione condivisa, intenzionalità).

- **Daniel Dennett — *From Bacteria to Bach and Back* (2017)**
  Il vocabolario filosofico: "competenza senza comprensione", memi come software culturale. Utile per dire con precisione che il web è un deposito di competenza compressa — e per discutere se il modello che lo assorbe "comprenda" o meno.

- **Terrence Deacon — *The Symbolic Species* (1997)**
  La versione più profonda (co-evoluzione linguaggio-cervello) su come i simboli comprimono. Più impegnativo; da terzo passaggio.

### Fondamento: perché il sensomotorio è lo strato duro

- **Hans Moravec — *Mind Children* (1988)**
  La fonte primaria del paradosso, con la spiegazione evolutiva ancora insuperata: percezione e motricità ottimizzate da centinaia di milioni di anni di evoluzione, ragionamento astratto da poche decine di migliaia — quindi il secondo è computazionalmente superficiale, il primo profondissimo. Datato nei dettagli, inquietantemente fresco nel capitolo centrale.

- **Max Bennett — *A Brief History of Intelligence* (2023)**
  Il libro singolo più vicino all'intera tesi. Cinque "breakthrough" evolutivi del cervello, con il linguaggio come *ultimo* strato sopra fondamenta sensomotorie antichissime. Struttura perfetta dell'argomento: gli LLM hanno scalato lo strato in cima saltando quelli sotto.

- **Fei-Fei Li — *The Worlds I See* (2023)**
  In forma di memoir, la tesi della "spatial intelligence" come prossima frontiera: il visivo/fisico non ha mai avuto il suo ImageNet-del-web sensomotorio. Leggero, ma dà il contesto storico di ImageNet dalla persona che l'ha costruito.

- **Andy Clark — *Surfing Uncertainty* (2015)**
  Predictive processing: il cervello come macchina predittiva che impara *agendo*. Il fondamento cognitivo del problema del closed loop — la distribuzione degli input dipende dalle tue azioni. Ponte naturale verso la linea JEPA/world models.

- **Melanie Mitchell — *Artificial Intelligence: A Guide for Thinking Humans* (2019)**
  Trattazione moderna e accessibile del paradosso di Moravec e della "barriera del senso comune". Buon punto d'ingresso se si vuole un unico libro divulgativo.

### Il pezzo mancante nei libri

- **Li & Vitányi — *An Introduction to Kolmogorov Complexity and Its Applications***
  L'unico libro su "intelligenza come compressione", ma è un tomo tecnico di teoria. Per questa parte il formato giusto sono i paper (sezione sotto).

**Se il budget è di due soli libri:** Henrich (perché il testo è compresso) + Bennett (perché il sensomotorio è duro). Moravec come terzo per la fonte storica.

---

## Paper (e materiale non peer-reviewed di pari peso)

### 1. Predizione = compressione — il fondamento teorico

- **Delétang et al. — *Language Modeling Is Compression* (DeepMind, 2023)**
  Dimostra formalmente ed empiricamente che un LLM è un compressore lossless allo stato dell'arte (batte gzip e PNG anche su immagini e audio). Il ponte tra Kolmogorov e GPT.

- **Rich Sutton — *The Bitter Lesson* (2019, essay, 2 pagine)**
  Non parla di compressione, ma è il contrappunto obbligato a ogni discorso su cosa scala e cosa no: i metodi generali che sfruttano il calcolo battono sempre la conoscenza di dominio cablata a mano.

### 2. Perché il testo è speciale — la densità semantica

- **Ilya Sutskever — *An Observation on Generalization* (talk, Berkeley 2023)**
  La formulazione della predizione come compressione del processo generatore: predire bene il prossimo token richiede modellare ciò che l'ha prodotto. Non peer-reviewed, ma è la fonte primaria della posizione.

- **Andrej Karpathy — talk e scritti vari (2023–)**
  La formulazione "il testo è la proiezione del mondo attraverso menti umane" compare quasi verbatim. Da prendere come divulgazione d'autore della stessa tesi.

- **Bender & Koller — *Climbing towards NLU* (ACL 2020)**
  Il paper dell'"octopus test" — la versione *scettica* dello stesso punto: se il testo è solo una proiezione, cosa manca a chi vede solo quella? Da leggere insieme ai due precedenti per avere la tensione completa del dibattito, non solo un lato.

### 3. Il paradosso di Moravec aggiornato — il collo di bottiglia dei dati

- **Yann LeCun — *A Path Towards Autonomous Machine Intelligence* (position paper, 2022)**
  La critica sistematica all'autoregressione su token per il mondo fisico e la proposta JEPA: predire in spazio di rappresentazione, non pixel-per-pixel. Tesi contestata, non fatto acquisito — ed è questo che la rende utile.

- **V-JEPA / V-JEPA 2-AC (Meta, 2024–2025)**
  Il seguito operativo della linea JEPA: world model appresi da video, con la variante action-conditioned per il controllo robotico.

- **Silver & Sutton — *The Era of Experience* (2025)**
  La formulazione più esplicita di "i dati umani sono finiti e stanno finendo; la prossima fase è l'esperienza raccolta dall'agente". Il paragrafo sulla densità semantica visto dal lato delle conseguenze.

- **Open X-Embodiment (2023)**
  Lo sforzo di 21 istituzioni per assemblare ~1M di traiettorie robotiche. Il confronto con i trilioni di token del web è l'intero argomento in una riga: il rapporto tra i due numeri *è* il collo di bottiglia.

- **EgoScale (2026)**
  Le performance delle policy robotiche scalano in modo prevedibile con la dimensione del pretraining — prima evidenza forte che i foundation model robotici seguono le stesse curve data-driven degli LLM. Rende il collo di bottiglia dei dati più centrale, non meno: se le scaling law valgono, la domanda diventa dove trovare gli ordini di grandezza mancanti.

### 4. La confutazione empirica dello slogan — tokenizzare si può

- **RT-2 (Google DeepMind, 2023)**
  Azioni robotiche come token di testo dentro un VLM: il comando motorio trattato letteralmente come linguaggio. La confutazione empirica diretta di "non si può tokenizzare il mondo fisico".

- **OpenVLA (2024)**
  La versione open della stessa idea (7B, fine-tunabile su GPU consumer). Dimostra che il paradigma è replicabile fuori da Google.

- **π0 (Physical Intelligence, 2024)**
  E quando i token discreti non bastano (manipolazione fine, controllo ad alta frequenza): flow matching per generare azioni continue. La risposta ingegneristica — non metafisica — al problema del continuo.

- **Genie / Genie 2 (DeepMind, 2024)**
  Mondi interattivi generati da token latenti di video: perfino gli ambienti si tokenizzano.

---

## Ordine di lettura consigliato

1. **Sezione 1–2** → il *perché* gli LLM funzionano: compressione di un corpus già compresso dall'umanità.
2. **Sezione 3** → il *perché* il fisico è duro: nessun corpus equivalente, costo dell'esperienza, closed loop.
3. **Sezione 4** → il *perché* lo slogan sulla tokenizzazione è la diagnosi sbagliata del problema vero.
4. **Libri** in parallelo per lo strato profondo (Henrich su tutti: nessun paper dà quella prospettiva).

Test finale di possesso dell'argomento: saperlo sostenere in entrambe le direzioni — sia "il testo è un trucco irripetibile" sia "le scaling law robotiche chiuderanno il gap".