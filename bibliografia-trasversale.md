# Bibliografia trasversale

*Sintesi delle nove bibliografie dell'archivio. Nessuna di esse è stata modificata: questo documento è una lettura sopra di loro, non un rimpiazzo.*

**Compilato:** 31 agosto 2026. **Ultima revisione:** 3 settembre 2026 (§1: ingresso della nona lista, correzione delle date SemEval).

---

## 0. Cosa è questo documento, e con quale criterio è filtrato

L'archivio contiene nove liste bibliografiche costruite in momenti diversi, per progetti diversi, con criteri di inclusione diversi (e in tre casi non dichiarati). Sommate fanno alcune centinaia di voci. Nessuno le ha mai lette una accanto all'altra.

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
| [intensione-autonomia](argomenti/intensione-autonomia/bibliografia.md) | da dove vengono i primitivi; autonomia, normatività | ~60 in 17 §§ | sì — due tradizioni, con §0 sul loro disaccordo | disponibilità testi verificata 17 ago 2026 |
| [reasoning](argomenti/reasoning/bibliografia-ragionata.md) | reasoning come omonimo; 11 nuclei A–K | ~120 (45 nell'itinerario) | sì, ed è il più esplicito dell'archivio | citazioni al mag 2026 |
| [composizionalità transformer](argomenti/composizionalita-transformer/bibliografia.md) | aritmetica e circuiti nei Transformer | ~21, di cui 12 ★ | sì — rilevanza per il design sperimentale | — |
| [content drift](argomenti/interpretability/bibliografia-drift-mechint.md) | CoT drift + mech interp su EDOS/HateXplain | ~55 in 10 §§ | no, ma ha uno schema di verifica (✔/⚠) | — |
| [scoperta di astrazioni](argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) | library learning, skill discovery, compressione | ~50 | implicito (prior art di un progetto chiuso) | **ago 2026, invecchia in fretta** |
| [interpretability](argomenti/interpretability/bibliografia.md) | XAI e mech interp, livelli 0–9 | ~35 | **no** | — |
| [mappa dei libri](argomenti/compressione-astrazione/mappa-dei-libri.md) | monografie | ~15 | sì — cosa copre quale terzo del problema | lug 2026 |
| [SemEval 2027](lavori/2026-09_semeval-2027/reading-list.md) | valutazione di task candidate (due nella lista, sette nella [valutazione del 3 set](lavori/2026-09_semeval-2027/valutazione-task.md)) | ~10 | sì — formale/strutturato vs vago | training data 8 set 2026 |
| [AAS — paper della lezione *Intelligent Agents*](formazione/autonomous-adaptive-systems/pdf/README.md) | i riferimenti di un corso di RL e agenti | 9 + 1 non scaricabile | sì — cosa è citato nelle slide, non cosa è rilevante | ricostruita dalle slide, 3 set 2026 |

La nona lista entra con **intersezione zero**: nessuno dei nove paper del corso compare in nessuna delle altre otto bibliografie, e nessuna delle altre otto cita Turing, AlphaGo, DeepStack o RLHF. Non è una svista dell'una o delle altre — è il segno che l'archivio ha costruito i propri fili *attorno* al canone RL/agenti invece che dentro, e che quel canone entra qui per la prima volta. Per questo la lista non tocca né la §2 né la §3: non ha ancora niente con cui incrociarsi.

Tre schemi di priorità incompatibili convivono: **★** (composizionalità, intensione), **portante vs stato dell'arte** (reasoning), **prioritarie / tecniche / da consultare** (scoperta di astrazioni), più i **livelli 0–9** di interpretability, che sono profondità e non priorità. E due schemi di verifica: `[V]`/`[M]` in intensione-autonomia, `✔`/`⚠` in content-drift. Il resto non ne ha.

---

## 2. Il nucleo condiviso

Le voci presenti in **due o più** bibliografie. È l'ossatura reale dell'archivio, e non era scritta da nessuna parte.

| Voce | Dossier | Perché ricorre |
|---|---|---|
| **Elhage, N., Nanda, N., Olsson, C., Henighan, T., Joseph, N., Mann, B., et al. (2021).** *A Mathematical Framework for Transformer Circuits*. Transformer Circuits Thread, Anthropic | composizionalità · content-drift · reasoning · interpretability | **La voce più condivisa dell'archivio.** Non è un risultato, è il vocabolario: residual stream, circuiti QK/OV, composizione fra teste. Quattro dossier su cinque che toccano i Transformer partono da qui |
| **Wang, K. R., Variengien, A., Conmy, A., Shlegeris, B. & Steinhardt, J. (2023).** *Interpretability in the Wild: A Circuit for Indirect Object Identification in GPT-2 Small*. ICLR | composizionalità · content-drift · reasoning | Il template metodologico per un circuito ricostruito end-to-end |
| **Conmy, A., Mavor-Parker, A. N., Lynch, A., Heimersheim, S. & Garriga-Alonso, A. (2023).** *Towards Automated Circuit Discovery for Mechanistic Interpretability*. NeurIPS | composizionalità · content-drift · reasoning | L'automazione (ACDC), citata da tutti come piano B quando l'analisi manuale esplode |
| **Nanda, N., Chan, L., Lieberum, T., Smith, J. & Steinhardt, J. (2023).** *Progress Measures for Grokking via Mechanistic Interpretability*. ICLR | composizionalità · content-drift(¹) · reasoning · scoperta di astrazioni | L'unico algoritmo aritmetico interamente reverse-engineered. In *scoperta di astrazioni* compare per un'altra ragione: come caso di **simbolo emergente** |
| **Quirke, P., Neo, C. & Barez, F. (2024).** *Arithmetic in Transformers Explained*. arXiv:2402.02619 — vedi §5(²) | composizionalità (★) · reasoning (I.3) · interpretability | I circuiti dell'addizione multi-cifra in Transformer piccoli |
| **Bai, X., Pres, I., Deng, Y., Tan, C., Shieber, S. M., Viégas, F. B., Wattenberg, M. & Lee, A. (2025).** *Why Can't Transformers Learn Multiplication? Reverse-Engineering Reveals Long-Range Dependency Pitfalls*. arXiv:2510.00184 | composizionalità (★) · reasoning (I.3) | Il DAG di cache e retrieval dei prodotti parziali costruito dall'attenzione |
| **Lindsey, J., Gurnee, W., Ameisen, E., Chen, B., Pearce, A., Turner, N. L., et al. (2025).** *On the Biology of a Large Language Model*. Transformer Circuits Thread, Anthropic | composizionalità (★) · reasoning (I.3) | Circuiti aritmetici ibridi in un modello di frontiera: la cautela obbligata sul transfer dalla piccola scala |
| **Dziri, N., Lu, X., Sclar, M., Li, X. L., Jiang, L., Lin, B. Y., et al. (2023).** *Faith and Fate: Limits of Transformers on Compositionality*. NeurIPS | composizionalità (★) · reasoning | La composizionalità come proprietà graduabile, non binaria |
| **Lake, B. M. & Baroni, M. (2018).** *Generalization Without Systematicity: On the Compositional Skills of Sequence-to-Sequence Recurrent Networks*. ICML | composizionalità (★) · reasoning | SCAN: il benchmark che ha reso misurabile la sfida di Fodor & Pylyshyn |
| **Hupkes, D., Dankers, V., Mul, M. & Bruni, E. (2020).** *Compositionality Decomposed: How Do Neural Networks Generalise?*. JAIR 67 | composizionalità · reasoning | Le cinque nozioni separabili: impedisce di usare "composizionalità" come blocco unico |
| **Zeng, P., Griffiths, T. L. & Lake, B. M. (2026).** *Nothing from Something: Can a Language Model Discover 0?*. CCN 2026, arXiv:2606.17289 | composizionalità (★) · intensione-autonomia (★) | **L'unica giuntura già dichiarata**: i due dossier si linkano a vicenda su questa voce. Vedi §3.E |
| **Turpin, M., Michael, J., Perez, E. & Bowman, S. R. (2023).** *Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting*. NeurIPS | content-drift · reasoning (nucleo H) | Il paper fondativo sull'infedeltà della traccia: bias mai menzionati determinano la risposta |
| **Lanham, T., Chen, A., Radhakrishnan, A., Steiner, B., Denison, C., et al. (2023).** *Measuring Faithfulness in Chain-of-Thought Reasoning*. Anthropic, arXiv:2307.13702 | content-drift · reasoning (nucleo H) | Le metriche di perturbazione: early answering, adding mistakes, filler token, parafrasi |
| **Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q. & Zhou, D. (2022).** *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*. NeurIPS 35 | content-drift · reasoning (G.1) | Punto d'ingresso obbligato, e in entrambi i dossier immediatamente relativizzato |
| **Bricken, T., Templeton, A., Batson, J., et al. (2023).** *Towards Monosemanticity: Decomposing Language Models With Dictionary Learning*. Transformer Circuits Thread · **Templeton, A., Conerly, T., Marcus, J., et al. (2024).** *Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet*. Transformer Circuits Thread · **Cunningham, H., Ewart, A., Riggs, L., Huben, R. & Sharkey, L. (2023).** *Sparse Autoencoders Find Highly Interpretable Features in Language Models*. arXiv:2309.08600 | content-drift · interpretability | In interpretability sono un livello del percorso di lettura; in content-drift sono **«il ramo più probabile a farti perdere due mesi senza risultato»**. Stesso oggetto, giudizio opposto |
| **Meng, K., Bau, D., Andonian, A. & Belinkov, Y. (2022).** *Locating and Editing Factual Associations in GPT*. NeurIPS 35, arXiv:2202.05262 | composizionalità · content-drift | Il *causal tracing* nella sua formulazione originale |
| **Marks, S. & Tegmark, M. (2023).** *The Geometry of Truth: Emergent Linear Structure in Large Language Model Representations of True/False Datasets*. arXiv:2310.06824 | composizionalità · content-drift | Direzioni lineari non solo decodificabili ma causalmente coinvolte; difference-in-means come metodo |
| **Geiger, A., Lu, H., Icard, T. & Potts, C. (2021).** *Causal Abstractions of Neural Networks*. NeurIPS — e **Geiger, A., et al. (2023).** *Causal Abstraction: A Theoretical Foundation for Mechanistic Interpretability*. arXiv:2301.04709 | intensione-autonomia (§12) · reasoning (I.2) | In entrambi è **il collo di bottiglia**: le condizioni sotto cui «la rete implementa l'algoritmo X» smette di essere una metafora |
| **Goodman, N. (1955).** *Fact, Fiction, and Forecast*. Harvard University Press | intensione-autonomia (★) · reasoning (fase 1) | *Grue*: la generalizzazione OOD trent'anni prima |
| **Todd, E., et al. (2024).** *Function Vectors in Large Language Models*. ICLR | reasoning (I.4) · scoperta di astrazioni (§5) | Riuso di funzioni apprese; e in *scoperta di astrazioni* come esempio di **quasi-simbolo** |
| **Zhou, H., et al. (2023/2024).** *What Algorithms Can Transformers Learn? A Study in Length Generalization*. ICLR, arXiv:2310.16028 | reasoning (nucleo E) · scoperta di astrazioni | L'ipotesi RASP-L: il ponte fra espressività e apprendibilità |
| **Ellis, K., Wong, C., Nye, M., Sablé-Meyer, M., et al. (2021).** *DreamCoder: Bootstrapping Inductive Program Synthesis with Wake-Sleep Library Learning*. PLDI | intensione-autonomia (§12) · scoperta di astrazioni | In *intensione* è un limite («la libreria vive **fuori** dal modello, e si cerca per enumerazione»); in *scoperta* è la fondazione del filone |
| **Grünwald, P. (2007).** *The Minimum Description Length Principle*. MIT Press | mappa dei libri · scoperta di astrazioni | In entrambi: «da consultare», mai da leggere per intero |

(¹) In content-drift compare come voce di contorno del §5, non con l'enfasi degli altri.
(²) Lo stesso `arXiv:2402.02619` è registrato con **tre titoli diversi** in tre file dell'archivio. Vedi §5.

**Cosa dice la tabella.** Il baricentro condiviso dell'archivio è l'**apparato mech-interp** (Elhage, Wang, Conmy, Nanda, Geiger): è ciò che quattro dossier su otto usano davvero, ed è l'unico strumentario su cui esiste consenso interno. Tutto il resto è specialistico per filo.

---

## 3. Le convergenze non dichiarate

Qui sta il valore vero di leggere gli otto documenti insieme: **quattro domande su cui più dossier convergono da letterature che non si citano**.

### A. «Decodificabile ≠ usato causalmente» — quattro dossier, quattro tradizioni

| Dossier | Come arriva alla distinzione |
|---|---|
| composizionalità | **Hewitt, J. & Liang, P. (2019).** *Designing and Interpreting Probes with Control Tasks*. EMNLP-IJCNLP — un probe accurato non prova nulla |
| content-drift | **Belinkov, Y. (2022).** *Probing Classifiers: Promises, Shortcomings, and Advances*. Computational Linguistics 48(1) — un probe può imparare il task da sé |
| reasoning (J.4) | **Rigotti, M., Barak, O., Warden, M. R., Wang, X.-J., Daw, N. D., Miller, E. K. & Fusi, S. (2013).** *The Importance of Mixed Selectivity in Complex Cognitive Tasks*. Nature 497 — e **Bernardi, S., Benna, M. K., Rigotti, M., Munuera, J., Fusi, S. & Salzman, C. D. (2020).** *The Geometry of Abstraction in the Hippocampus and Prefrontal Cortex*. Cell 183(4): la **CCGP**, dalla neuroscienza dei primati |
| intensione-autonomia (§12) | **Geiger, A., et al. (2023).** *Causal Abstraction: A Theoretical Foundation for Mechanistic Interpretability* — le interchange intervention come «test operativo che manca a tutti i lavori sopra» |

Quattro letterature — probing in NLP, interpretabilità, neuroscienza dei sistemi, causal abstraction — arrivano indipendentemente alla stessa distinzione. La versione neuroscientifica è la più vecchia e la più operativa: la CCGP è nata perché la decodificabilità semplice si era già rivelata quasi priva di contenuto (è il risultato di Rigotti: con dimensionalità sufficiente qualunque partizione è separabile). Il dossier reasoning lo dice esplicitamente in J.4 — «l'interpretabilità dei Transformer non ha ancora assorbito del tutto questa lezione» — ma nessun altro documento dell'archivio lo raccoglie.

> **La mossa disponibile**, già indicata in reasoning J.4 e mai ripresa altrove: importare la CCGP in contesto aritmetico — un probe sui prodotti parziali addestrato su alcune coppie di cifre e testato su altre.

### B. «Il neurale propone, il simbolico verifica» — e il teorema che lo giustifica

Quattro dossier ospitano la stessa architettura senza che nessuno la nomini allo stesso modo:

- **scoperta di astrazioni** (§5): «il neurale propone, il simbolo vive fuori, la verifica lo promuove» — è dove sono atterrati tutti. I tre sistemi citati: **Wang, G., Xie, Y., Jiang, Y., Mandlekar, A., Xiao, C., Zhu, Y., Fan, L. & Anandkumar, A. (2023).** *Voyager: An Open-Ended Embodied Agent with Large Language Models*; **Grand, G., Wong, L., Bowers, M., et al. (2024).** *LILO: Learning Interpretable Libraries by Compressing and Documenting Code*. ICLR; **Stengel-Eskin, E., et al. (2024).** *ReGAL: Refactoring Programs to Discover Generalizable Abstractions*. ICML;
- **reasoning F.2**: *trovare* una dimostrazione e *verificarla* hanno difficoltà radicalmente diversa;
- **reasoning K**: la distinzione fra integrazione **a livello di loss** — **Manhaeve, R., Dumančić, S., Kimmig, A., Demeester, T. & De Raedt, L. (2018).** *DeepProbLog: Neural Probabilistic Logic Programming*. NeurIPS — e integrazione **a livello di pipeline** — **Pan, L., Albalak, A., Wang, X. & Wang, W. Y. (2023).** *Logic-LM: Empowering Large Language Models with Symbolic Solvers for Faithful Logical Reasoning*; **Olausson, T. X., et al. (2023).** *LINC: A Neurosymbolic Approach for Logical Reasoning by Combining Language Models with First-Order Logic Provers*. «La seconda è quella che funziona oggi, la prima è quella teoricamente interessante»;
- **SemEval 2027**: la pipeline NS-EDL, validatore simbolico sopra un layer NLI.

**Il pezzo che manca e che l'archivio possiede già senza saperlo:** reasoning F.2 fornisce la *giustificazione complessologica* dell'architettura che gli altri tre adottano per ragioni ingegneristiche. L'asimmetria generare/verificare non è una comodità implementativa, è un fatto di teoria della complessità.

### C. Da dove vengono i primitivi — tre risposte incompatibili nello stesso archivio

| Dossier | Risposta | Stato |
|---|---|---|
| intensione-autonomia | **Non dalla computazione pura.** **Cariani, P. (1991).** *Emergence and Artificial Life*, in Langton, C. G. et al. (a cura di), *Artificial Life II*: emergenza combinatoria vs creativa. E **Fodor, J. (1975).** *The Language of Thought*: non si può imparare un concetto che non si è già in grado di esprimere | argomento, con una clausola che fa molto lavoro |
| scoperta di astrazioni | **Dalla compressione MDL su programmi.** **Ellis, K., et al. (2021).** *DreamCoder* e **Bowers, M., Olausson, T. X., Wong, L., Grand, G., Tenenbaum, J. B., Ellis, K. & Solar-Lezama, A. (2023).** *Top-Down Synthesis for Library Learning* (Stitch), POPL. E funziona | funziona, ma **offline** e fuori dal modello |
| mappa dei libri (§4) | **Dal corpo.** **Lakoff, G. & Narayanan, S. (2025).** *The Neural Mind*. University of Chicago Press: gli *image schemas* derivati dall'esperienza sensomotoria | «nessuna funzione obiettivo, nessun criterio di selezione fra schemi, nessuna verifica» |

I collegamenti a coppie esistono già (mappa dei libri → intensione; scoperta di astrazioni → intensione). Il **triangolo** no. Ed è interessante perché le tre risposte non sono varianti: sono un argomento di impossibilità, una dimostrazione di esistenza in un regime ristretto, e una tesi difficilmente falsificabile. La seconda è l'unica con codice funzionante, ed è precisamente quella che l'argomento della prima non copre — DreamCoder cresce la libreria per enumerazione, senza gradienti, il che è *emergenza combinatoria* alla Cariani con l'insieme di partenza scelto bene.

### D. Il primato del formato — lo stesso fenomeno a quattro livelli

- **reasoning F.1** — **Cook, S. A. & Reckhow, R. A. (1979).** *The Relative Efficiency of Propositional Proof Systems*. JSL 44(1): cambiare formato = cambiare sistema di prova, e questo può cambiare la lunghezza minima della dimostrazione di un **fattore esponenziale**. È la giustificazione teorica più solida dell'esistenza di scaffold efficaci;
- **reasoning E** — **Merrill, W. & Sabharwal, A. (2024).** *The Expressive Power of Transformers with Chain of Thought*. ICLR: la CoT come computazione seriale che estende la classe di complessità;
- **composizionalità** — **Lee, N., Sreenivasan, K., Lee, J. D., Lee, K. & Papailiopoulos, D. (2024).** *Teaching Arithmetic to Small Transformers*. ICLR: il formato dei dati determina cosa un piccolo Transformer riesce ad apprendere in aritmetica;
- **content-drift** — **Sprague, Z., Yin, F., Rodriguez, J. D., Jiang, D., Wadhwa, M., Singhal, P., Zhao, X., Ye, X., Mahowald, K. & Durrett, G. (2024).** *To CoT or Not to CoT? Chain-of-Thought Helps Mainly on Math and Symbolic Reasoning*. ICLR 2025, arXiv:2409.12183: empiricamente la CoT aiuta **solo** su matematica e ragionamento simbolico.

Teoria della complessità, espressività architetturale, formato del training, efficacia misurata: quattro strati dello stesso fatto, distribuiti su tre dossier che non si citano.

### E. Il modello di come dovrebbe funzionare un link

**Zeng, P., Griffiths, T. L. & Lake, B. M. (2026).** *Nothing from Something: Can a Language Model Discover 0?* è l'unico caso in cui due dossier si linkano reciprocamente sulla stessa voce, ciascuno spiegando **cosa l'altro ci trova**: intensione-autonomia la usa come messa alla prova empirica del problema di Fodor, composizionalità come oggetto sperimentale e gancio mech-interp. È il formato che le altre ventidue voci condivise della §2 non hanno.

---

## 4. Le tensioni

**1. Due politiche di inclusione opposte.** Reasoning dichiara: «Le rassegne non entrano mai, salvo come punto di ingresso a un'area nuova, e in quel caso vengono sostituite dai primari appena letti». [interpretability/papers.md](argomenti/interpretability/bibliografia.md) è per metà rassegne (livelli 7–8, otto voci) e non ha criterio di inclusione. Non è un errore in sé — sono documenti con funzioni diverse, uno è una bibliografia di ricerca e l'altro una mappa didattica del campo — ma la differenza non è scritta da nessuna parte, e chi apre il secondo dopo il primo non ha modo di saperlo.

**2. Le sparse autoencoder.** Livello 6 di un percorso di lettura in un dossier; «il ramo più affascinante e il più probabile candidato a farti perdere due mesi senza risultato» nell'altro. Il secondo giudizio è operativo e più recente: dovrebbe vincere, e non è visibile a chi legge solo il primo.

**3. Il transfer dalla neuroscienza.** Reasoning J è esplicito: «da questo nucleo vanno presi i metodi e le distinzioni, **non i risultati**», e la §15 esclude il NeuroAI in senso lato. Intensione-autonomia costruisce invece un intero asse (tradizione B: **Varela, F. (1979).** *Principles of Biological Autonomy*; **Bickhard, M. H. (1993).** *Representational Content in Humans and Machines*; **Barandiaran, X., Di Paolo, E. & Rohde, M. (2009).** *Defining Agency: Individuality, Normativity, Asymmetry, and Spatio-temporality in Action*; **Di Paolo, E., Buhrmann, T. & Barandiaran, X. (2017).** *Sensorimotor Life: An Enactive Proposal*) su un argomento biologico. Non è una contraddizione — l'uno esclude il transfer di *risultati* sperimentali, l'altro importa una *tesi concettuale* — ma i due criteri non sono mai stati messi accanto, e la distinzione fra i due tipi di prestito è esattamente ciò che rende la seconda mossa difendibile.

**4. Sovrapposizione quasi totale su un'area.** Composizionalità §§1–2 e reasoning I.3 coprono lo stesso materiale (Quirke, Bai, Lindsey, Nanda, e **Zhong, Z., Liu, Z., Tegmark, M. & Andreas, J. (2023).** *The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks*, NeurIPS) con annotazioni diverse. Reasoning aggiunge il vincolo che il primo non enuncia: Zhong e Lindsey insieme rendono **illegittimo** il passaggio *circuito trovato in un modello piccolo → meccanismo generale*. È il punto da cui un revisore attacca, e sta solo in uno dei due documenti.

---

## 5. Igiene

Cose concrete emerse dalla lettura incrociata.

- **I due dossier più grandi sono i meno visibili.** `argomenti/reasoning/bibliografia-ragionata.md` e `argomenti/interpretability/bibliografia-drift-mechint.md` sono ~1050 righe e la bibliografia più curata dell'archivio, ma nessuna delle due ha una riga propria nel README di radice.
- **Lo stesso paper è registrato con tre titoli diversi.** `arXiv:2402.02619` compare come *Arithmetic in Transformers Explained* (composizionalità), *Understanding Addition and Subtraction in Transformers* (interpretability/aritmetica-mech-int), *Understanding Addition in Transformers* (reasoning I.3) — e con due liste autori diverse (Quirke, Neo & Barez vs Quirke & Barez). Da risolvere una volta sola, prima che finisca in un paper.
- **[interpretability/bibliografia.md](argomenti/interpretability/bibliografia.md) porta residui di conversazione.** La riga 124 comincia con «Ottima osservazione — nella lista mancava il "perché" fondamentale», e il livello 0 è appiccicato in coda invece che in testa; l'indice finale annuncia «ex 28–30» ma le voci sono 28–29. È l'unico documento dell'archivio che non è stato riscritto dopo essere stato generato.
- **[reasoning/neurosimbolico-nlp.md](argomenti/reasoning/neurosimbolico-nlp.md)** è appunti grezzi (abstract in inglese incollati) e copre la stessa area del nucleo K di reasoning, che è più curato. Candidato a fusione.
- **Nessuna convenzione di verifica condivisa.** `[V]`/`[M]`, `✔`/`⚠`, oppure niente. Vale la pena sceglierne una: è l'unica annotazione che serve davvero sei mesi dopo, quando una citazione va in un paper.
- **Le date di validità sono dichiarate solo dove il campo si muove in fretta** (scoperta di astrazioni, ago 2026) — ed è la scelta giusta. Andrebbe estesa alla bibliografia drift/mech-int, che è tutta su letteratura 2023–2026.

---

## 6. Se leggi dieci cose in tutto l'archivio

Non un percorso per un filo: le dieci voci che pagano di più **attraverso** i fili, con il dossier che le ospita.

| | Voce | Cosa dà |
|---|---|---|
| 1 | **Marr, D. (1982).** *Vision: A Computational Investigation into the Human Representation and Processing of Visual Information*. W. H. Freeman — cap. 1 · *reasoning* J.1 | I tre livelli di analisi. Sette degli undici sensi di "reasoning" si dispongono su di essi, e quasi tutti i disaccordi pubblici sono confusioni di livello |
| 2 | **Elhage, N., et al. (2021).** *A Mathematical Framework for Transformer Circuits*. Anthropic — quattro dossier | Il vocabolario condiviso. Senza, tre quarti dell'archivio è illeggibile |
| 3 | **Goodman, N. (1955).** *Fact, Fiction, and Forecast*. Harvard University Press — cap. 3 · *intensione* + *reasoning* | *Grue*. Dai dati non segue una generalizzazione: il problema della rilevanza, prima che avesse un nome tecnico |
| 4 | **Rice, H. G. (1953).** *Classes of Recursively Enumerable Sets and Their Decision Problems*. Transactions of the AMS 74(2) — *intensione* §3 | Due pagine. Ogni criterio automatico può guardare solo la forma, e non per pigrizia del progettista |
| 5 | **Cook, S. A. & Reckhow, R. A. (1979).** *The Relative Efficiency of Propositional Proof Systems*. JSL 44(1) + **Haken, A. (1985).** *The Intractability of Resolution*. TCS 39 — *reasoning* F.1 | La difficoltà del problema ≠ il limite dell'agente. La distinzione più assente dalla letteratura ML sul reasoning |
| 6 | **Bernardi, S., Benna, M. K., Rigotti, M., Munuera, J., Fusi, S. & Salzman, C. D. (2020).** *The Geometry of Abstraction in the Hippocampus and Prefrontal Cortex*. Cell 183(4) — *reasoning* J.4 | La CCGP: decodificabile ≠ astratto, con una metrica già costruita. Vedi §3.A |
| 7 | **Hewitt, J. & Liang, P. (2019).** *Designing and Interpreting Probes with Control Tasks*. EMNLP-IJCNLP — *composizionalità* ★ | Il correttivo metodologico che rende non pubblicabile metà di quello che si vorrebbe scrivere |
| 8 | **Dziri, N., et al. (2023).** *Faith and Fate: Limits of Transformers on Compositionality*. NeurIPS — *composizionalità* + *reasoning* | La composizionalità come grandezza graduabile, sul caso aritmetico |
| 9 | **Zeng, P., Griffiths, T. L. & Lake, B. M. (2026).** *Nothing from Something: Can a Language Model Discover 0?*. CCN — *composizionalità* + *intensione* | La domanda filosofica trasformata in esperimento controllato. La giuntura dell'archivio |
| 10 | **Cariani, P. (1998).** *Epistemic Autonomy through Adaptive Sensing*. IEEE ISIC — *intensione* §9 | Venti pagine. Emergenza combinatoria vs creativa: la formulazione operativa della domanda che tiene insieme tre fili su sei |

**Se invece un solo libro:** **MacKay, D. J. C. (2003).** *Information Theory, Inference, and Learning Algorithms*. Cambridge University Press — fatto con gli esercizi, non sfogliato. È il verdetto della [mappa dei libri](argomenti/compressione-astrazione/mappa-dei-libri.md), ed è l'unico titolo dell'archivio di cui si dica che *cambia gli strumenti* invece di aggiungere riferimenti.

---

## 7. Manutenzione di questo file

Non è una bibliografia e non va fatto crescere come tale. Va rifatto quando cambia una delle tre cose che lo giustifica:

- entra o esce una bibliografia dall'archivio;
- una voce passa da un dossier a due (cioè: entra nel nucleo condiviso della §2);
- una delle quattro convergenze della §3 viene raccolta esplicitamente in uno dei dossier — nel qual caso la riga va tolta da qui, perché ha smesso di essere invisibile.

Se cresce senza che nessuna di queste tre cose sia successa, sta diventando una copia.
