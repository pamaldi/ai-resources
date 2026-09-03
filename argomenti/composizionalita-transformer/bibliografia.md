# Bibliografia
## Composizionalità, aritmetica e mechanistic interpretability nei Transformer

Questa bibliografia è organizzata per rilevanza rispetto al progetto sperimentale descritto nel README.  
I riferimenti contrassegnati con **★** sono quelli più direttamente importanti per il design dell'esperimento.

---

## 1. Riferimenti fondamentali per il progetto

### ★ Quirke, Neo & Barez — circuiti aritmetici in piccoli Transformer

Quirke, P., Neo, C., & Barez, F. (2024). **Arithmetic in Transformers Explained**. *arXiv preprint arXiv:2402.02619*.

https://arxiv.org/abs/2402.02619

**Rilevanza:** analizza meccanicisticamente piccoli Transformer autoregressivi addestrati su addizione, sottrazione e training mixed. È il riferimento principale per i circuiti aritmetici di base, il riuso di feature tra operazioni e il tipo di modello sperimentale da adottare.

---

### ★ Bai et al. — moltiplicazione, partial products e cache DAG

Bai, X., Pres, I., Deng, Y., Tan, C., Shieber, S. M., Viégas, F. B., Wattenberg, M., & Lee, A. (2025). **Why Can't Transformers Learn Multiplication? Reverse-Engineering Reveals Long-Range Dependency Pitfalls**. *arXiv preprint arXiv:2510.00184*.

https://arxiv.org/abs/2510.00184

**Rilevanza:** riferimento più diretto per il progetto. Mostra che un Transformer capace di apprendere la moltiplicazione multi-cifra può costruire tramite attenzione un **directed acyclic graph (DAG)** per cachare e recuperare i pairwise partial products. Introduce inoltre una auxiliary loss sul *running sum* che fornisce un inductive bias utile per apprendere la moltiplicazione.

---

### ★ Lee et al. — formato dei dati, next-token prediction e length generalization

Lee, N., Sreenivasan, K., Lee, J. D., Lee, K., & Papailiopoulos, D. (2024). **Teaching Arithmetic to Small Transformers**. *International Conference on Learning Representations (ICLR 2024)*.

https://openreview.net/forum?id=dsUB4bst9S

**Rilevanza:** dimostra che formato dei dati, sampling e rappresentazione degli step intermedi influenzano fortemente l'apprendimento aritmetico nei piccoli Transformer. È particolarmente importante per giustificare il controllo sul formato `NUM OP NUM = NUM` e per distinguere composizionalità da length generalization.

---

### ★ Dziri et al. — limiti della composizionalità nei Transformer

Dziri, N., Lu, X., Sclar, M., Li, X. L., Jiang, L., Lin, B. Y., Welleck, S., West, P., Bhagavatula, C., Le Bras, R., Hwang, J. D., Sanyal, S., Ren, X., Ettinger, A., Harchaoui, Z., & Choi, Y. (2023). **Faith and Fate: Limits of Transformers on Compositionality**. *Advances in Neural Information Processing Systems (NeurIPS 2023)*.

https://openreview.net/forum?id=Fkckkr3ya8

**Rilevanza:** studia task composizionali, inclusa la moltiplicazione multi-cifra, attraverso grafi computazionali e complessità dei sottoproblemi. Fornisce un importante precedente per trattare la composizionalità come problema strutturale graduabile anziché come proprietà binaria.

---

### ★ Lindsey et al. — circuit tracing in Claude 3.5 Haiku

Lindsey, J., Gurnee, W., Ameisen, E., Chen, B., Pearce, A., Turner, N. L., Citro, C., Abrahams, D., Carter, S., Hosmer, B., Marcus, J., Sklar, M., Templeton, A., Bricken, T., McDougall, C., Cunningham, H., Henighan, T., Jermyn, A., Jones, A., Persic, A., Qi, Z., Thompson, T. B., Zimmerman, S., Rivoire, K., Conerly, T., Olah, C., & Batson, J. (2025). **On the Biology of a Large Language Model**. *Transformer Circuits Thread*.

https://transformer-circuits.pub/2025/attribution-graphs/biology.html

**Rilevanza:** mostra che un frontier model può usare strategie aritmetiche e circuiti più ibridi e distribuiti rispetto ai piccoli Transformer specializzati. È il riferimento principale per motivare la cautela nel trasferire risultati meccanicistici dalla piccola alla grande scala.

---

## 2. Aritmetica e generalizzazione algoritmica

### McLeish et al. — positional representation e extrapolation

McLeish, S., Bansal, A., Stein, A., Jain, N., Kirchenbauer, J., Bartoldson, B. R., Kailkhura, B., Bhatele, A., Geiping, J., Schwarzschild, A., & Goldstein, T. (2024). **Transformers Can Do Arithmetic with the Right Embeddings**. *Advances in Neural Information Processing Systems 37 (NeurIPS 2024)*.

https://arxiv.org/abs/2405.17399

**Rilevanza:** mostra che una parte importante dei fallimenti di generalizzazione aritmetica deriva dalla rappresentazione della posizione delle cifre. Con *Abacus Embeddings* ottiene forte extrapolation a lunghezze superiori a quelle viste nel training. È un controllo importante contro l'interpretazione eccessiva dei fallimenti come "non composizionali".

---

### Kantamneni & Tegmark — rappresentazioni numeriche nei language model

Kantamneni, S., & Tegmark, M. (2025). **Language Models Use Trigonometry to Do Addition**. *arXiv preprint arXiv:2502.00873*.

https://arxiv.org/abs/2502.00873

**Rilevanza:** propone una spiegazione a livello rappresentazionale dell'addizione in language model di scala intermedia, identificando una struttura numerica a elica e verificandone il ruolo con interventi causali. Utile per confrontare algoritmi appresi a scale differenti.

---

### Nanda et al. — grokking e algoritmi interni

Nanda, N., Chan, L., Lieberum, T., Smith, J., & Steinhardt, J. (2023). **Progress Measures for Grokking via Mechanistic Interpretability**. *International Conference on Learning Representations (ICLR 2023)*.

https://arxiv.org/abs/2301.05217

**Rilevanza:** reverse-engineering di piccoli Transformer su addizione modulare. Mostra come un comportamento apparentemente emergente possa essere decomposto in formazione progressiva di circuiti e validato tramite ablazioni.

---

## 3. Composizionalità e systematic generalization

### ★ Lake & Baroni — SCAN e systematicity

Lake, B. M., & Baroni, M. (2018). **Generalization without Systematicity: On the Compositional Skills of Sequence-to-Sequence Recurrent Networks**. *Proceedings of the 35th International Conference on Machine Learning (ICML 2018), PMLR 80*.

https://proceedings.mlr.press/v80/lake18a.html

**Rilevanza:** lavoro classico sulla distinzione tra semplice generalizzazione e generalizzazione composizionale sistematica. Il principio sperimentale — conoscere una primitiva ma testarla in una combinazione nuova — è direttamente collegato alla Condizione B del progetto.

---

### ★ Zeng, Griffiths & Lake — un modello può *scoprire* lo zero?

Zeng, P., Griffiths, T. L., & Lake, B. M. (2026). **Nothing from Something: Can a Language Model Discover 0?**. *Proceedings of the 9th Conference on Cognitive Computational Neuroscience (CCN 2026)*.

https://arxiv.org/abs/2606.17289 · [PDF locale](pdf/Zeng-Griffiths-Lake_Discover-Zero-CCN26.pdf)

**Rilevanza:** paper-ponte tra questo dossier e [intensione/autonomia](../intensione-autonomia/bibliografia.md#4-il-problema-radicale-dellacquisizione-dei-concetti). Usa lo stesso oggetto sperimentale dell'intera bibliografia — GPT-2 (124M) e un piccolo Transformer addestrati su addizione/sottrazione a una cifra, tokenizzazione per-cifra, analisi delle rappresentazioni delle cifre (similarità coseno degli embedding) e ruolo del *carry* — ma per una domanda più radicale della systematic recombination: **un modello addestrato in un mondo senza lo zero può postularlo quando gli serve?** Cioè può introdurre un primitivo nuovo ($p_{n+1}$), non solo ricombinare quelli dati.

**Risultati**: (1) zero-shot, *nessun* modello scopre lo zero, con o senza pretraining linguistico — coerente con l'argomento di impossibilità di Fodor; (2) bastano pochi esempi few-shot e generalizzano, e il **pretraining linguistico dimezza (~50%)** gli esempi necessari — evidenza misurabile del *bootstrapping* alla Carey, il linguaggio come impalcatura alla scoperta concettuale; (3) lo zero è *speciale* (il più difficile, con il 9 che innesca il carry): le cifre centrali si generalizzano meglio → **interpolazione facile, estrapolazione difficile**, verificato sulla geometria degli embedding (curva a V rovesciata). Chiude con la domanda meccanicistica aperta — «possiamo osservare la circuiteria responsabile di queste generalizzazioni?» — che è il gancio verso la parte mech-interp del progetto.

---

### Hupkes et al. — decomporre la composizionalità

Hupkes, D., Dankers, V., Mul, M., & Bruni, E. (2020). **Compositionality Decomposed: How do Neural Networks Generalise?** *Journal of Artificial Intelligence Research, 67*, 757–795.

https://www.jair.org/index.php/jair/article/view/11674

**Rilevanza:** distingue diverse forme di composizionalità e propone test separati per proprietà differenti. È utile per evitare di usare "composizionalità" come singolo concetto monolitico.

---

## 4. Rappresentazioni lineari e probing

### ★ Park, Choe & Veitch — Linear Representation Hypothesis

Park, K., Choe, Y. J., & Veitch, V. (2023). **The Linear Representation Hypothesis and the Geometry of Large Language Models**. *arXiv preprint arXiv:2311.03658*.

https://arxiv.org/abs/2311.03658

**Rilevanza:** formalizza cosa significhi parlare di rappresentazioni lineari di concetti e collega linear probing, steering e interpretazione causale. È un riferimento teorico importante per la parte del progetto relativa al residual stream.

---

### Marks & Tegmark — rappresentazioni lineari e causalità

Marks, S., & Tegmark, M. (2023). **The Geometry of Truth: Emergent Linear Structure in Large Language Model Representations of True/False Datasets**. *arXiv preprint arXiv:2310.06824*.

https://arxiv.org/abs/2310.06824

**Rilevanza:** combina probe, generalizzazione cross-dataset e interventi causali per mostrare che alcune direzioni lineari non sono soltanto decodificabili ma funzionalmente coinvolte nel comportamento del modello.

---

### ★ Hewitt & Liang — limiti interpretativi dei probe

Hewitt, J., & Liang, P. (2019). **Designing and Interpreting Probes with Control Tasks**. *Proceedings of EMNLP-IJCNLP 2019*.

https://arxiv.org/abs/1909.03368

**Rilevanza:** riferimento metodologico fondamentale per non interpretare un probe accurato come prova automatica che la rappresentazione studiata sia causalmente usata dal modello. Giustifica l'uso combinato di probing e interventi causali.

---

### Hewitt & Manning — structural probing

Hewitt, J., & Manning, C. D. (2019). **A Structural Probe for Finding Syntax in Word Representations**. *Proceedings of NAACL-HLT 2019*, 4129–4138.

https://aclanthology.org/N19-1419/

**Rilevanza:** esempio classico di probing della geometria delle rappresentazioni. Utile come precedente metodologico, anche se il dominio è sintattico e non aritmetico.

---

## 5. Mechanistic interpretability e metodi causali

### ★ Elhage et al. — framework dei circuiti Transformer

Elhage, N., Nanda, N., Olsson, C., Henighan, T., Joseph, N., Mann, B., Askell, A., Bai, Y., Chen, A., Conerly, T., DasSarma, N., Drain, D., Ganguli, D., Hatfield-Dodds, Z., Hernandez, D., Jones, A., Kernion, J., Lovitt, L., Ndousse, K., Amodei, D., Brown, T., Clark, J., Kaplan, J., McCandlish, S., & Olah, C. (2021). **A Mathematical Framework for Transformer Circuits**. *Transformer Circuits Thread*.

https://transformer-circuits.pub/2021/framework/index.html

**Rilevanza:** riferimento fondativo per residual stream, circuiti QK/OV, composizione tra attention head e interpretazione dei Transformer come grafi computazionali.

---

### Wang et al. — circuit discovery con interventi causali

Wang, K. R., Variengien, A., Conmy, A., Shlegeris, B., & Steinhardt, J. (2023). **Interpretability in the Wild: A Circuit for Indirect Object Identification in GPT-2 Small**. *International Conference on Learning Representations (ICLR 2023)*.

https://arxiv.org/abs/2211.00593

**Rilevanza:** esempio canonico di ricostruzione end-to-end di un circuito tramite patching, ablazioni e interventi causali. Utile come modello metodologico per la ricerca dei circuiti di retrieval, routing e carry.

---

### Meng et al. — causal tracing

Meng, K., Bau, D., Andonian, A., & Belinkov, Y. (2022). **Locating and Editing Factual Associations in GPT**. *Advances in Neural Information Processing Systems 35 (NeurIPS 2022)*.

https://arxiv.org/abs/2202.05262

**Rilevanza:** introduce il *causal tracing* per localizzare stati interni decisivi nella computazione di un Transformer. Il principio può essere adattato alla ricerca del primo layer/timestep in cui una moltiplicazione corretta e una fallita divergono causalmente.

---

### Conmy et al. — automated circuit discovery

Conmy, A., Mavor-Parker, A. N., Lynch, A., Heimersheim, S., & Garriga-Alonso, A. (2023). **Towards Automated Circuit Discovery for Mechanistic Interpretability**. *Advances in Neural Information Processing Systems (NeurIPS 2023)*.

https://arxiv.org/abs/2304.14997

**Rilevanza:** formalizza e automatizza parte del processo di circuit discovery, usando activation patching per identificare componenti e connessioni causali. Potrebbe essere utile quando l'analisi manuale dei circuiti aritmetici diventa troppo ampia.

---

### ★ Ameisen et al. — attribution graphs e circuit tracing

Ameisen, E., Lindsey, J., Pearce, A., Gurnee, W., Turner, N. L., Chen, B., Citro, C., Abrahams, D., Carter, S., Hosmer, B., Marcus, J., Sklar, M., Templeton, A., Bricken, T., McDougall, C., Cunningham, H., Henighan, T., Jermyn, A., Jones, A., Persic, A., Qi, Z., Thompson, T. B., Zimmerman, S., Rivoire, K., Conerly, T., Olah, C., & Batson, J. (2025). **Circuit Tracing: Revealing Computational Graphs in Language Models**. *Transformer Circuits Thread*.

https://transformer-circuits.pub/2025/attribution-graphs/methods.html

**Rilevanza:** introduce attribution graphs e una metodologia per ricostruire passaggi computazionali interni e validarli con interventi. È particolarmente pertinente alla proposta di rappresentare la moltiplicazione come pipeline causale `compute → cache → retrieve → route → accumulate → carry`.

---

## 6. Fondamenti cognitivi e neuroscientifici della composizionalità

### ★ Frankland & Greene — la composizionalità nel cervello e il language of thought

Frankland, S. M., & Greene, J. D. (2020). **Concepts and Compositionality: In Search of the Brain's Language of Thought**. *Annual Review of Psychology, 71*, 273–303.

https://doi.org/10.1146/annurev-psych-122216-011829 · [PDF locale](pdf/Frankland-Greene_Concepts-Compositionality-LoT-AnnRevPsy20.pdf)

**Rilevanza:** review di riferimento sul *grounding* cognitivo e neuroscientifico della composizionalità — il "perché" che sta a monte di tutto il progetto sperimentale. Inquadra la questione con l'ipotesi del **language of thought** di Fodor & Pylyshyn (la stessa systematicity che motiva [Lake & Baroni](#-lake--baroni--scan-e-systematicity)) e la mappa su meccanismi cerebrali concreti: combinazione concettuale nel *default mode network*, codici map-like/grid-cell per il contenuto amodale, e soprattutto la rappresentazione di **relazioni strutturate esplicite** ("who did what to whom") tramite *role binding* nel solco temporale superiore medio-sinistro, con rappresentazioni ruolo-invarianti riusate tra frasi.

È il punto in cui la domanda diventa la stessa del progetto ma su un altro substrato: **come si implementa fisicamente il binding tra concetto e ruolo, e come si separano memoria e computazione (pointer)** — esattamente ciò che la parte meccanicistica cerca nel residual stream e nei circuiti di routing. Fornisce il ponte tra il filo [language of thought / program induction](../compressione-astrazione/scoperta-di-astrazioni-letteratura.md) (e il corso [NYU CCM](../../formazione/nyu-ccm-lake-gureckis.md)) e l'interpretabilità dei Transformer: non è un riferimento per il *design* dell'esperimento, ma per la sua *motivazione teorica* e per il vocabolario (binding, ruoli, pointer, riuso strutturato) con cui interpretarne i risultati.

---

# Lettura consigliata

Per avviare concretamente l'esperimento, l'ordine di lettura più utile è:

1. **Quirke, Neo & Barez (2024)** — capire il modello e i circuiti aritmetici di base.
2. **Bai et al. (2025)** — capire partial products, cache DAG, long-range dependencies e auxiliary loss.
3. **Lee et al. (2024)** — controllare formato, dataset e length generalization.
4. **Dziri et al. (2023)** — inquadrare la moltiplicazione come problema composizionale strutturato.
5. **Lake & Baroni (2018)** — chiarire cosa significhi systematic recombination.
6. **Hewitt & Liang (2019)** — evitare interpretazioni eccessive dei probe.
7. **Wang et al. (2023)** e **Conmy et al. (2023)** — progettare patching, ablazioni e circuit discovery.
8. **Lindsey et al. (2025)** — comprendere i limiti del transfer dai piccoli modelli ai frontier model.

Come **background teorico** (non necessario al design, utile a inquadrare il "perché"): **Frankland & Greene (2020)** — cosa significa composizionalità nel cervello, binding tra concetti e ruoli, language of thought.

---

# Nucleo minimo da citare nel README

Se il README deve rimanere molto compatto, i riferimenti indispensabili sono:

1. Quirke, Neo & Barez (2024) — *Arithmetic in Transformers Explained*.
2. Bai et al. (2025) — *Why Can't Transformers Learn Multiplication?*
3. Lee et al. (2024) — *Teaching Arithmetic to Small Transformers*.
4. Dziri et al. (2023) — *Faith and Fate: Limits of Transformers on Compositionality*.
5. Lake & Baroni (2018) — *Generalization without Systematicity*.
6. Hewitt & Liang (2019) — *Designing and Interpreting Probes with Control Tasks*.
7. Wang et al. (2023) — *Interpretability in the Wild*.
8. Lindsey et al. (2025) — *On the Biology of a Large Language Model*.
