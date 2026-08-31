# Bibliografia trasversale

*Sintesi delle otto bibliografie dell'archivio. Nessuna di esse è stata modificata: questo documento è una lettura sopra di loro, non un rimpiazzo.*

**Compilato:** 31 agosto 2026.

---

## 0. Cosa è questo documento, e con quale criterio è filtrato

L'archivio contiene otto liste bibliografiche costruite in momenti diversi, per progetti diversi, con criteri di inclusione diversi (e in tre casi non dichiarati). Sommate fanno alcune centinaia di voci. Nessuno le ha mai lette una accanto all'altra.

Farlo produce tre cose che non esistono altrove, e che sono le uniche ragioni per cui questo file merita di stare nel repo:

1. **quali voci ricorrono in più bibliografie** — l'unica misura di centralità che l'archivio possiede e che nessun singolo documento può vedere;
2. **su quali domande i dossier convergono senza dirselo** — dove due letterature diverse stanno rispondendo alla stessa cosa e non si citano;
3. **dove i criteri di inclusione si contraddicono** — perché due documenti dello stesso archivio applicano politiche opposte.

**Criterio di inclusione qui.** Una voce entra se soddisfa almeno una condizione:

- **(a)** compare in **due o più** bibliografie distinte;
- **(b)** è marcata come portante nella propria bibliografia (★, "nucleo minimo", "prioritarie", fase 1–4 dell'itinerario) **e** regge un filo del [README](README.md).

Non entra una voce solo perché è buona. Le bibliografie originali restano il posto dove sta il dettaglio: qui c'è solo ciò che è visibile **fra** i documenti.

---

## 1. Censimento

| Documento | Copre | Voci ca. | Criterio dichiarato | Validità |
|---|---|---|---|---|
| [intensione-autonomia](topics/intensione-autonomia/bibliografia.md) | da dove vengono i primitivi; autonomia, normatività | ~60 in 17 §§ | sì — due tradizioni, con §0 sul loro disaccordo | disponibilità testi verificata 17 ago 2026 |
| [reasoning](topics/reasoning/reasoning-bibliografia-ragionata.md) | reasoning come omonimo; 11 nuclei A–K | ~120 (45 nell'itinerario) | sì, ed è il più esplicito dell'archivio | citazioni al mag 2026 |
| [composizionalità transformer](topics/composizionalita_transformer/BIBLIOGRAFIA_composizionalita_transformer.md) | aritmetica e circuiti nei Transformer | ~21, di cui 12 ★ | sì — rilevanza per il design sperimentale | — |
| [content drift](topics/content-drift/bibliografia_drift_mechint.md) | CoT drift + mech interp su EDOS/HateXplain | ~55 in 10 §§ | no, ma ha uno schema di verifica (✔/⚠) | — |
| [scoperta di astrazioni](topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) | library learning, skill discovery, compressione | ~50 | implicito (prior art di un progetto chiuso) | **ago 2026, invecchia in fretta** |
| [interpretability](topics/interpretability/papers.md) | XAI e mech interp, livelli 0–9 | ~35 | **no** | — |
| [mappa dei libri](topics/compressione-astrazione/mappa-dei-libri.md) | monografie | ~15 | sì — cosa copre quale terzo del problema | lug 2026 |
| [SemEval 2027](projects/semeval-2027/reading-list.md) | valutazione di due task candidate | ~10 | sì — formale/strutturato vs vago | sample data dal 1 set 2026 |

Tre schemi di priorità incompatibili convivono: **★** (composizionalità, intensione), **portante vs stato dell'arte** (reasoning), **prioritarie / tecniche / da consultare** (scoperta di astrazioni), più i **livelli 0–9** di interpretability, che sono profondità e non priorità. E due schemi di verifica: `[V]`/`[M]` in intensione-autonomia, `✔`/`⚠` in content-drift. Il resto non ne ha.

---

## 2. Il nucleo condiviso

Le voci presenti in **due o più** bibliografie. È l'ossatura reale dell'archivio, e non era scritta da nessuna parte.

| Voce | Dossier | Perché ricorre |
|---|---|---|
| **Elhage et al. (2021)** — *A Mathematical Framework for Transformer Circuits* | composizionalità · content-drift · reasoning · interpretability | **La voce più condivisa dell'archivio.** Non è un risultato, è il vocabolario: residual stream, QK/OV, composizione fra teste. Quattro dossier su cinque che toccano i Transformer partono da qui |
| **Wang et al. (2023)** — *Interpretability in the Wild* (IOI) | composizionalità · content-drift · reasoning | Il template metodologico per un circuito ricostruito end-to-end |
| **Conmy et al. (2023)** — ACDC | composizionalità · content-drift · reasoning | L'automazione, citata da tutti come piano B quando l'analisi manuale esplode |
| **Nanda et al. (2023)** — *Progress Measures for Grokking* | composizionalità · content-drift(¹) · reasoning · scoperta di astrazioni | L'unico algoritmo aritmetico interamente reverse-engineered. In *scoperta di astrazioni* compare per un'altra ragione: come caso di **simbolo emergente** |
| **Quirke & Barez (2024)** · **Bai et al. (2025)** · **Lindsey et al. (2025)** | composizionalità (★) · reasoning (I.3) | Il trittico dell'aritmetica: addizione, moltiplicazione, modello di frontiera |
| **Dziri et al. (2023)** — *Faith and Fate* | composizionalità (★) · reasoning | La composizionalità come proprietà graduabile, non binaria |
| **Lake & Baroni (2018)** — SCAN | composizionalità (★) · reasoning | Il benchmark che ha reso misurabile la sfida di Fodor & Pylyshyn |
| **Hupkes et al. (2020)** — *Compositionality Decomposed* | composizionalità · reasoning | Le cinque nozioni separabili: impedisce di usare "composizionalità" come blocco unico |
| **Zeng, Griffiths & Lake (2026)** — *Can a Language Model Discover 0?* | composizionalità (★) · intensione-autonomia (★) | **L'unica giuntura già dichiarata**: i due dossier si linkano a vicenda su questa voce. Vedi §3 |
| **Turpin et al. (2023)** · **Lanham et al. (2023)** | content-drift · reasoning (nucleo H) | Il problema della fedeltà della traccia, e le metriche di perturbazione |
| **Wei et al. (2022)** — Chain-of-Thought | content-drift · reasoning | Punto d'ingresso obbligato, e in entrambi i dossier immediatamente relativizzato |
| **Bricken (2023)** · **Templeton (2024)** · **Cunningham (2023)** — SAE | content-drift · interpretability | In interpretability sono un livello del percorso; in content-drift sono **"il ramo più probabile a farti perdere due mesi"**. Stesso oggetto, giudizio opposto |
| **Meng et al. (2022)** — causal tracing · **Marks & Tegmark (2023)** | composizionalità · content-drift | Localizzazione causale e direzioni lineari |
| **Geiger et al. (2021/2023)** — causal abstraction | intensione-autonomia (§12) · reasoning (I.2) | In entrambi è **il collo di bottiglia**: le condizioni sotto cui "la rete implementa l'algoritmo X" smette di essere una metafora |
| **Goodman (1955)** — *Fact, Fiction, and Forecast* | intensione-autonomia (★) · reasoning (fase 1) | *Grue*: la generalizzazione OOD trent'anni prima |
| **Todd et al. (2024)** — function vectors | reasoning (I.4) · scoperta di astrazioni (§5) | Riuso; e in *scoperta di astrazioni* come esempio di **quasi-simbolo** |
| **Zhou et al. (2023/24)** — RASP-L | reasoning (nucleo E) · scoperta di astrazioni | Il ponte fra espressività e apprendibilità |
| **DreamCoder** (Ellis et al. 2021) | intensione-autonomia (§12) · scoperta di astrazioni | In *intensione* è un limite ("la libreria vive **fuori** dal modello"); in *scoperta* è la fondazione del filone |
| **Grünwald** — *MDL* | mappa dei libri · scoperta di astrazioni | In entrambi: "da consultare", mai da leggere |

(¹) In content-drift compare come voce di contorno del §5, non con l'enfasi degli altri.

**Cosa dice la tabella.** Il baricentro condiviso dell'archivio è l'**apparato mech-interp** (Elhage, Wang, Conmy, Nanda, Geiger): è ciò che quattro dossier su otto usano davvero, ed è l'unico strumentario su cui esiste consenso interno. Tutto il resto è specialistico per filo.

---

## 3. Le convergenze non dichiarate

Qui sta il valore vero di leggere gli otto documenti insieme: **quattro domande su cui più dossier convergono da letterature che non si citano**.

### A. «Decodificabile ≠ usato causalmente» — quattro dossier, quattro tradizioni

| Dossier | Come arriva alla distinzione |
|---|---|
| composizionalità | **Hewitt & Liang (2019)**, control task: un probe accurato non prova nulla |
| content-drift | **Belinkov (2022)**: un probe può imparare il task da sé |
| reasoning (J.4) | **Rigotti (2013) + Bernardi (2020)**: la **CCGP**, dalla neuroscienza dei primati |
| intensione-autonomia (§12) | **Geiger**: le interchange intervention come «test operativo che manca a tutti i lavori sopra» |

Quattro letterature — NLP probing, interpretabilità, neuroscienza dei sistemi, causal abstraction — arrivano indipendentemente alla stessa distinzione. La versione neuroscientifica è la più vecchia e la più operativa: la CCGP è nata perché la decodificabilità semplice si era già rivelata quasi priva di contenuto. Il dossier reasoning lo dice esplicitamente (J.4: «l'interpretabilità dei Transformer non ha ancora assorbito del tutto questa lezione») ma nessun altro documento dell'archivio lo raccoglie.

> **La mossa disponibile**, già indicata in reasoning J.4 e mai ripresa altrove: importare la CCGP in contesto aritmetico — probe sui prodotti parziali addestrato su alcune coppie di cifre, testato su altre.

### B. «Il neurale propone, il simbolico verifica» — e il teorema che lo giustifica

Quattro dossier ospitano la stessa architettura senza che nessuno la nomini allo stesso modo:

- **scoperta di astrazioni** (§5): «il neurale propone, il simbolo vive fuori, la verifica lo promuove» — è dove sono atterrati tutti (Voyager, LILO, ReGAL);
- **reasoning F.2**: *trovare* una dimostrazione e *verificarla* hanno difficoltà radicalmente diversa;
- **reasoning K**: la distinzione fra integrazione **a livello di loss** (DeepProbLog) e **a livello di pipeline** (Logic-LM, LINC) — «la seconda è quella che funziona oggi, la prima è quella teoricamente interessante»;
- **SemEval 2027**: la pipeline NS-EDL, validatore simbolico sopra un layer NLI.

**Il pezzo che manca e che l'archivio possiede già senza saperlo:** reasoning F.2 fornisce la *giustificazione complessologica* dell'architettura che gli altri tre adottano per ragioni ingegneristiche. L'asimmetria generare/verificare non è una comodità implementativa, è un fatto di teoria della complessità.

### C. Da dove vengono i primitivi — tre risposte incompatibili nello stesso archivio

| Dossier | Risposta | Stato |
|---|---|---|
| intensione-autonomia | **Non dalla computazione pura** — emergenza combinatoria vs creativa (Cariani); e non si può imparare un concetto non esprimibile (Fodor) | argomento, con una clausola che fa molto lavoro |
| scoperta di astrazioni | **Dalla compressione MDL su programmi** — DreamCoder, Stitch. E funziona | funziona, ma **offline** e fuori dal modello |
| mappa dei libri (§4) | **Dal corpo** — image schemas derivati dall'esperienza sensomotoria (Lakoff & Narayanan) | «nessuna funzione obiettivo, nessun criterio di selezione, nessuna verifica» |

I collegamenti a coppie esistono già (mappa dei libri → intensione; scoperta di astrazioni → intensione). Il **triangolo** no. Ed è interessante perché le tre risposte non sono varianti: sono un argomento di impossibilità, una dimostrazione di esistenza in un regime ristretto, e una tesi non falsificabile. La seconda è l'unica con codice funzionante, ed è precisamente quella che l'argomento della prima non copre — DreamCoder cresce la libreria per enumerazione, senza gradienti, il che è *emergenza combinatoria* alla Cariani con l'insieme di partenza scelto bene.

### D. Il primato del formato — lo stesso fenomeno a quattro livelli

- **reasoning F.1**: cambiare formato = cambiare sistema di prova, e questo può cambiare la lunghezza minima della dimostrazione di un **fattore esponenziale**. È la giustificazione teorica più solida dell'esistenza di scaffold efficaci;
- **reasoning E** (Merrill & Sabharwal 2024): la CoT come computazione seriale che estende la classe di complessità;
- **composizionalità** (Lee et al. 2024): il formato dei dati determina cosa un piccolo Transformer riesce ad apprendere in aritmetica;
- **content-drift** (Sprague et al. 2024): empiricamente la CoT aiuta **solo** su matematica e ragionamento simbolico.

Teoria della complessità, espressività architetturale, formato del training, efficacia misurata: quattro strati dello stesso fatto, distribuiti su tre dossier che non si citano.

### E. Il modello di come dovrebbe funzionare un link

**Zeng, Griffiths & Lake (2026)** è l'unico caso in cui due dossier si linkano reciprocamente sulla stessa voce, ciascuno spiegando **cosa l'altro ci trova**: intensione-autonomia la usa come messa alla prova empirica del problema di Fodor, composizionalità come oggetto sperimentale e gancio mech-interp. È il formato che le altre diciotto voci condivise della §2 non hanno.

---

## 4. Le tensioni

**1. Due politiche di inclusione opposte.** Reasoning dichiara: «Le rassegne non entrano mai, salvo come punto di ingresso a un'area nuova, e in quel caso vengono sostituite dai primari appena letti». [interpretability/papers.md](topics/interpretability/papers.md) è per metà rassegne (livelli 7–8, otto voci) e non ha criterio di inclusione. Non è un errore in sé — sono documenti con funzioni diverse, uno è una bibliografia di ricerca e l'altro una mappa didattica del campo — ma la differenza non è scritta da nessuna parte, e chi apre il secondo dopo il primo non ha modo di saperlo.

**2. Le SAE.** Livello 6 di un percorso di lettura in un dossier; «il ramo più affascinante e il più probabile candidato a farti perdere due mesi senza risultato» nell'altro. Il secondo giudizio è operativo e più recente: dovrebbe vincere, e non è visibile a chi legge solo il primo.

**3. Il transfer dalla neuroscienza.** Reasoning J è esplicito: «da questo nucleo vanno presi i metodi e le distinzioni, **non i risultati**», e la §15 esclude il NeuroAI in senso lato. Intensione-autonomia costruisce invece un intero asse (tradizione B: Varela, Bickhard, Barandiaran, Di Paolo) su un argomento biologico. Non è una contraddizione — l'uno esclude il transfer di *risultati* sperimentali, l'altro importa una *tesi concettuale* — ma i due criteri non sono mai stati messi accanto, e la distinzione fra i due tipi di prestito è esattamente ciò che rende la seconda mossa difendibile.

**4. Sovrapposizione quasi totale su un'area.** Composizionalità §§1–2 e reasoning I.3 coprono lo stesso materiale (Quirke, Bai, Lindsey, Nanda, Zhong) con annotazioni diverse. Reasoning aggiunge il vincolo che il primo non enuncia: Zhong e Lindsey insieme rendono **illegittimo** il passaggio *circuito trovato in un modello piccolo → meccanismo generale*. È il punto da cui un revisore attacca, e sta solo in uno dei due documenti.

---

## 5. Igiene

Cose concrete emerse dalla lettura incrociata.

- **I due dossier più grandi non sono nel repo né nel README.** `topics/reasoning/` e `topics/content-drift/` risultano **untracked** in git, e il [README](README.md) non li menziona: i suoi cinque fili si fermano a prima che esistessero. Sono ~1050 righe e la bibliografia più curata dell'archivio. Prima azione ovvia: commit e aggiornamento della mappa dei fili.
- **[interpretability/papers.md](topics/interpretability/papers.md) porta residui di conversazione.** La riga 124 comincia con «Ottima osservazione — nella lista mancava il "perché" fondamentale», e il livello 0 è appiccicato in coda invece che in testa; l'indice finale annuncia «ex 28–30» ma le voci sono 28–29. È l'unico documento dell'archivio che non è stato riscritto dopo essere stato generato.
- **`topics/reasoning-neurosimbolico/neurosimbolico-nlp.md`** è appunti grezzi (abstract in inglese incollati) e copre la stessa area del nucleo K di reasoning, che è più curato. Candidato a fusione.
- **Nessuna convenzione di verifica condivisa.** `[V]`/`[M]`, `✔`/`⚠`, oppure niente. Vale la pena sceglierne una: è l'unica annotazione che serve davvero sei mesi dopo, quando una citazione va in un paper.
- **Le date di validità sono dichiarate solo dove il campo si muove in fretta** (scoperta di astrazioni, ago 2026) — ed è la scelta giusta. Andrebbe estesa a content-drift, che è tutto su letteratura 2023–2026.

---

## 6. Se leggi dieci cose in tutto l'archivio

Non un percorso per un filo: le dieci voci che pagano di più **attraverso** i fili, con il dossier che le ospita.

| | Voce | Cosa dà |
|---|---|---|
| 1 | **Marr (1982)**, cap. 1 — *reasoning* J.1 | I tre livelli. Sette degli undici sensi di "reasoning" si dispongono su di essi, e quasi tutti i disaccordi pubblici sono confusioni di livello |
| 2 | **Elhage et al. (2021)** — quattro dossier | Il vocabolario condiviso. Senza, tre quarti dell'archivio è illeggibile |
| 3 | **Goodman (1955)**, cap. 3 — *intensione* + *reasoning* | *Grue*. Dai dati non segue una generalizzazione: il problema della rilevanza, prima che avesse un nome tecnico |
| 4 | **Rice (1953)** — *intensione* §3 | Due pagine. Ogni criterio automatico può guardare solo la forma, e non per pigrizia del progettista |
| 5 | **Cook & Reckhow (1979)** + **Haken (1985)** — *reasoning* F.1 | La difficoltà del problema ≠ il limite dell'agente. La distinzione più assente dalla letteratura ML sul reasoning |
| 6 | **Bernardi et al. (2020)**, CCGP — *reasoning* J.4 | Decodificabile ≠ astratto, con una metrica già costruita. Vedi §3.A |
| 7 | **Hewitt & Liang (2019)** — *composizionalità* ★ | Il correttivo metodologico che rende non pubblicabile metà di quello che si vorrebbe scrivere |
| 8 | **Dziri et al. (2023)** — *composizionalità* + *reasoning* | La composizionalità come grandezza graduabile, sul caso aritmetico |
| 9 | **Zeng, Griffiths & Lake (2026)** — *composizionalità* + *intensione* | La domanda filosofica trasformata in esperimento controllato. La giuntura dell'archivio |
| 10 | **Cariani (1998)** — *intensione* §9 | Venti pagine. Emergenza combinatoria vs creativa: la formulazione operativa della domanda che tiene insieme tre fili su cinque |

**Se invece un solo libro:** MacKay, *Information Theory, Inference, and Learning Algorithms* — fatto con gli esercizi, non sfogliato. È il verdetto della [mappa dei libri](topics/compressione-astrazione/mappa-dei-libri.md), ed è l'unico titolo dell'archivio di cui si dica che *cambia gli strumenti* invece di aggiungere riferimenti.

---

## 7. Manutenzione di questo file

Non è una bibliografia e non va fatto crescere come tale. Va rifatto quando cambia una delle tre cose che giustifica:

- entra o esce una bibliografia dall'archivio;
- una voce passa da un dossier a due (cioè: entra nel nucleo condiviso della §2);
- una delle quattro convergenze della §3 viene raccolta esplicitamente in uno dei dossier — nel qual caso la riga va tolta da qui, perché ha smesso di essere invisibile.

Se cresce senza che nessuna di queste tre cose sia successa, sta diventando una copia.
