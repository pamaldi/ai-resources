Ecco la lista unificata, organizzata per livello di profondità crescente. Ho numerato tutto in sequenza.

---

**Livello 1 — Framework concettuali e riflessioni fondative**

Questi inquadrano il campo: cosa significa "interpretabilità", perché serve, quali sono le distinzioni chiave.

1. **"The Mythos of Model Interpretability"** — Lipton, 2018. Position paper che mette ordine nella confusione terminologica: cosa intendiamo per interpretabilità? Distingue trasparenza, simulabilità, decomponibilità. Breve ma essenziale per leggere tutto il resto con le idee chiare.

2. **"Stop Explaining Black Box Machine Learning Models for High Stakes Decisions and Use Interpretable Models Instead"** — Rudin, Nature Machine Intelligence 2019. Tesi provocatoria: per applicazioni ad alto rischio non servono spiegazioni post-hoc, servono modelli intrinsecamente interpretabili. Cambia prospettiva su tutto il campo.

---

**Livello 2 — Visualizzazione e comprensione delle CNN (i classici vision)**

I primi lavori a "guardare dentro" le reti convoluzionali.

3. **"Visualizing and Understanding Convolutional Networks"** — Zeiler & Fergus, ECCV 2014. Usa deconvolutional networks per visualizzare cosa attiva i singoli filtri a ogni layer. Uno dei primissimi a mostrare che le CNN costruiscono gerarchie di feature (bordi → texture → parti → oggetti). → [arxiv.org/abs/1311.1901](https://arxiv.org/abs/1311.1901)

4. **"Deep Inside Convolutional Networks: Visualising Image Classification Models and Saliency Maps"** — Simonyan, Vedaldi & Zisserman, 2014. Introduce le saliency map basate su gradienti e collega visualizzazione ConvNet a deconvolutional networks. → [arxiv.org/abs/1312.6034](https://arxiv.org/abs/1312.6034)

5. **"Network Dissection: Quantifying Interpretability of Deep Visual Representations"** — Bau, Zhou et al., CVPR 2017. Framework per quantificare l'interpretabilità delle rappresentazioni latenti delle CNN, valutando l'allineamento tra singole hidden unit e concetti semantici — oggetti, parti, scene, texture, materiali, colori. Risultato chiave: l'interpretabilità è axis-aligned, non isotropa. → [netdissect.csail.mit.edu](https://netdissect.csail.mit.edu/)

---

**Livello 3 — Metodi di attribuzione model-agnostic (il trittico fondamentale)**

Funzionano su qualsiasi rete neurale — CNN, RNN, feed-forward, transformer.

6. **"Why Should I Trust You? Explaining the Predictions of Any Classifier" (LIME)** — Ribeiro, Singh & Guestrin, KDD 2016. Perturba l'input localmente e addestra un modello surrogato semplice per spiegare la singola predizione. → [arxiv.org/abs/1602.04938](https://arxiv.org/abs/1602.04938)

7. **"A Unified Approach to Interpreting Model Predictions" (SHAP)** — Lundberg & Lee, NeurIPS 2017. Unifica i metodi di attribuzione sotto la teoria dei giochi cooperativi (valori di Shapley). Spiegazioni locali e globali. → [arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)

8. **"Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization"** — Selvaraju et al., ICCV 2017. Gradienti nell'ultimo layer convoluzionale → mappe di attivazione che evidenziano le regioni rilevanti. Specifico per CNN, molto intuitivo. → [arxiv.org/abs/1610.02391](https://arxiv.org/abs/1610.02391)

---

**Livello 4 — Metodi avanzati di attribuzione e analisi causale**

Tecniche più sofisticate, con fondamenta assiomatiche o causali.

9. **"Axiomatic Attribution for Deep Networks" (Integrated Gradients)** — Sundararajan, Taly & Yan, ICML 2017. Definisce assiomi che un buon metodo di attribuzione deve soddisfare e propone Integrated Gradients. Matematicamente elegante. → [arxiv.org/abs/1703.01365](https://arxiv.org/abs/1703.01365)

10. **"Learning Important Features Through Propagating Activation Differences" (DeepLIFT)** — Shrikumar, Greenside & Kundaje, ICML 2017. Propaga differenze di attivazione rispetto a un riferimento, catturando dipendenze che i gradienti puri possono mancare. → [arxiv.org/abs/1704.02685](https://arxiv.org/abs/1704.02685)

11. **"On Pixel-Wise Explanations for Non-Linear Classifier Decisions by Layer-Wise Relevance Propagation" (LRP)** — Bach et al., PLOS ONE 2015. Propaga la "rilevanza" all'indietro fino ai pixel, layer per layer. Molto usato in medicina e industria. → [doi.org/10.1371/journal.pone.0130140](https://doi.org/10.1371/journal.pone.0130140)

12. **"Understanding Black-box Predictions via Influence Functions"** — Koh & Liang, ICML 2017. Approccio diverso: usa influence function dalla statistica robusta per identificare quali training example hanno impattato una predizione. Non guarda i neuroni, guarda i dati. → [arxiv.org/abs/1703.04730](https://arxiv.org/abs/1703.04730)

---

**Livello 5 — Concept-based interpretability (oltre i pixel e i token)**

Spiegazioni a livello di concetti umani, non singole feature grezze. Ponte tra vision e linguaggio.

13. **"Interpretability Beyond Feature Attribution: Quantitative Testing with Concept Activation Vectors" (TCAV)** — Kim et al., ICML 2018. Invece di "quali pixel contano?", chiede "quanto conta il concetto 'strisce' per classificare come zebra?". → [arxiv.org/abs/1711.11279](https://arxiv.org/abs/1711.11279)

14. **"Towards Automatic Concept-based Explanations" (ACE)** — Ghorbani, Wexler & Kim, NeurIPS 2019. Estrae automaticamente concetti di alto livello che influenzano le predizioni, senza annotazioni umane.

---

**Livello 6 — Mechanistic interpretability per transformer e LLM**

I fondamenti teorici e le tecniche specifiche per capire "come pensano" i transformer.

15. **"A Mathematical Framework for Transformer Circuits"** — Elhage et al., Anthropic 2021. Formalizza come analizzare i transformer come circuiti: residual stream, attention heads come operazioni interpretabili, induction heads. Il punto zero della mechanistic interpretability moderna. → [transformer-circuits.pub/2021/framework](https://transformer-circuits.pub/2021/framework)

16. **"Toy Models of Superposition"** — Elhage et al., Anthropic 2022. Spiega perché i singoli neuroni non sono interpretabili: le reti comprimono più feature di quante dimensioni hanno. Introduce il concetto di superposition con modelli giocattolo eleganti. → [transformer-circuits.pub/2022/toy_model](https://transformer-circuits.pub/2022/toy_model)

17. **"Towards Monosemanticity: Decomposing Language Models With Dictionary Learning"** — Bricken et al., Anthropic 2023. Applica sparse autoencoder a un transformer a un layer, decompone le attivazioni MLP in oltre 4000 feature monosemantiche — DNA, linguaggio legale, richieste HTTP, testo ebraico. → [transformer-circuits.pub/2023/monosemantic-features](https://transformer-circuits.pub/2023/monosemantic-features)

18. **"Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet"** — Templeton et al., Anthropic 2024. Scala le SAE a un modello di produzione. Feature estratte multilingue, multimodali, utilizzabili per steerare il comportamento del modello. → [transformer-circuits.pub/2024/scaling-monosemanticity](https://transformer-circuits.pub/2024/scaling-monosemanticity)

19. **"Sparse Autoencoders Find Highly Interpretable Features in Language Models"** — Cunningham et al., ICLR 2024. Conferma indipendente della validità delle SAE su Pythia-70M/410M: le feature apprese sono più interpretabili e monosemantiche di quelle trovate con metodi alternativi. → [openreview.net/forum?id=F76bwRSLeK](https://openreview.net/forum?id=F76bwRSLeK)

---

**Livello 7 — Survey e panoramiche (reti neurali generali)**

Per avere il quadro completo attraverso architetture diverse.

20. **"On Interpretability of Artificial Neural Networks: A Survey"** — Classifica in post-hoc interpretability (feature analysis, saliency, proxy, analisi matematica/fisica avanzata) e ad-hoc interpretable modeling. Include la classe "advanced mathematical/physical analysis" assente nelle survey precedenti. → [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC9105427/)

21. **"Explainable Convolutional Neural Networks: A Taxonomy, Review, and Future Directions"** — ACM Computing Surveys. Classifica i modelli XAI per CNN in: modifica architettura, semplificazione rappresentazioni, analisi rilevanza feature, visualizzazione. Include il caso della CNN che classificava alberi guardando gli edifici sullo sfondo.

22. **"A Survey on Interpretability in Visual Recognition"** — Luglio 2025. Survey recentissimo: metodi con vincoli semantici (Network Dissection), concept representations, spiegazioni in linguaggio naturale, prototype-based interpretability (ProtoTree). → [arxiv.org/abs/2507.11099](https://arxiv.org/abs/2507.11099)

23. **"Interpretability of Deep Neural Networks: A Review of Methods, Classification and Hardware"** — Neurocomputing 2024. Classificazione in prediction explanation vs network explanation, con discussione sull'implementazione hardware dei metodi XAI.

---

**Livello 8 — Survey specifiche per mechanistic interpretability (LLM-focused)**

24. **"A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models"** — 2024, aggiornato Oct 2025. Survey task-centrico con dettagli tecnici su ogni tecnica MI, limiti, avanzamenti, e roadmap per principianti. → [arxiv.org/abs/2407.02646](https://arxiv.org/abs/2407.02646)

25. **"Mechanistic Interpretability for AI Safety — A Review"** — Bereska & Gavves, 2024. Collega MI alla AI safety. Copre intrinsic, developmental e post-hoc interpretability, con focus su scalabilità e automazione. → [arxiv.org/abs/2404.14082](https://arxiv.org/abs/2404.14082)

26. **"Unboxing the Black Box"** — Nov 2025. Tassonomia unificata: observation-based (visualizzazione pesi, attivazioni, gradienti) vs intervention-based (modifiche causali), con pseudo-code ed esempi. → [arxiv.org/abs/2511.19265](https://arxiv.org/abs/2511.19265)

27. **"Open Problems in Mechanistic Interpretability"** — Sharkey et al., Anthropic, Jan 2025 (arXiv:2501.16496). Mappa i problemi aperti del campo. Ottimo per capire dove va la ricerca.

---

**Livello 9 — Frontiera e questioni aperte**

Paper che mettono in discussione i fondamenti o aprono nuove direzioni.

28. **"Everything, Everywhere, All at Once: Is Mechanistic Interpretability Identifiable?"** — ICLR 2025. Risultato provocatorio: circuiti multipli replicano lo stesso comportamento, interpretazioni multiple per lo stesso circuito, algoritmi diversi si allineano causalmente alla stessa rete. Solleva il problema dell'unicità delle spiegazioni.

29. **"From Neurons to Neutrons: A Case Study in Mechanistic Interpretability"** — Meta AI. Le reti ad alta dimensionalità apprendono rappresentazioni a bassa dimensionalità utili oltre la predizione: MI può derivare nuova comprensione di un dominio (fisica nucleare) dai modelli. Applicazione fuori dal NLP.

---

**Percorso di lettura consigliato:**

**Se parti da zero:** 1 → 2 → 3 → 4 → 6 → 7 → 8 (basi generali NN + XAI classico) → poi 15 → 16 → 17 (fondamenti MI per transformer) → una survey a scelta (20-23 per NN generali, 24-26 per MI/LLM).

**Se vuoi approfondire l'attribuzione:** dopo il trittico LIME/SHAP/GradCAM, vai su 9 → 11 → 12 → 13.

**Se vuoi la frontiera critica:** 28 → 29 → 27.


Ottima osservazione — nella lista mancava il "perché" fondamentale. Aggiungo un nuovo livello che va inserito prima di tutto il resto, perché spiega le ragioni profonde per cui le NN sono black box. Ecco i paper da aggiungere:

---

**Nuovo Livello 0 — Perché le reti neurali non sono interpretabili**

Questi paper spiegano le cause strutturali dell'opacità, non le soluzioni.

**0a. "Distributed Representations"** — Hinton, McClelland & Rumelhart, 1986 (capitolo in *Parallel Distributed Processing*). Il testo fondativo: le reti neurali codificano i concetti come pattern distribuiti su molti neuroni, non come singole unità. Un concetto = attivazione di molti neuroni, un neurone = partecipa a molti concetti. Questo è il motivo originario per cui non puoi "leggere" una rete neurone per neurone. È il punto di partenza storico.

**0b. "Toy Models of Superposition"** — Elhage et al., Anthropic 2022. Già nella lista come n.16, ma va concettualmente qui perché risponde alla domanda "perché?". Le reti neurali "vogliono rappresentare più feature di quanti neuroni hanno", sfruttando la quasi-ortogonalità degli spazi ad alta dimensionalità per simulare un modello con molti più neuroni. La superposition produce polisemanticity: un singolo neurone risponde a concetti non correlati. Dimostra con toy model che superposition e polisemanticity emergono come fenomeni reali governati da transizioni di fase.

**0c. "Incidental Polysemanticity"** — Alignment Forum, 2024. Mostra che la polisemanticity può emergere anche quando ci sono abbastanza neuroni per tutte le feature: l'inizializzazione random può per caso assegnare più feature allo stesso neurone, e le dinamiche di training rinforzano questa sovrapposizione. Seconda origine della non-interpretabilità, complementare alla superposition.

**0d. "Zoom In: An Introduction to Circuits"** — Olah et al., Distill 2020. Paper seminale di Chris Olah che introduce la visione delle reti come circuiti composti da feature e connessioni. Documenta empiricamente sia neuroni monosemantici (curve detector, high-low frequency detector) sia neuroni polisemantici nelle CNN vision. È il paper che per primo articola chiaramente il problema e propone i circuiti come framework per affrontarlo.

**0e. "Why Should I Trust You?" + la prospettiva Rudin** — Qui convergono due argomenti complementari sul perché le NN non sono interpretabili. Il paper di Rudin (già n.2 nella lista) argomenta che la complessità non è necessaria — spesso modelli interpretabili raggiungono la stessa accuratezza dei black box, specialmente su dati strutturati, e che i black box possono mascherare errori gravi, come reti che classificano raggi X guardando il tipo di apparecchiatura invece del contenuto medico.

**0f. "From Superposition to Sparse Codes: Interpretable Representations in Neural Networks"** — 2025. Collega formalmente il dibattito neuroscienza (local coding vs distributed coding) con la superposition nei modelli AI. Usa teoria dell'identificabilità e compressed sensing per mostrare che lo sparse coding può recuperare feature interpretabili dalla superposition. Ponte elegante tra neuroscienze e MI.

---

Quindi la lista completa aggiornata diventa:

**Livello 0** — Perché le NN non sono interpretabili (0a–0f)
**Livello 1** — Framework concettuali (ex 1–2)
**Livello 2** — Visualizzazione CNN classica (ex 3–5)
**Livello 3** — Attribuzione model-agnostic: LIME, SHAP, GradCAM (ex 6–8)
**Livello 4** — Attribuzione avanzata e causale: IntGrad, DeepLIFT, LRP, Influence Functions (ex 9–12)
**Livello 5** — Concept-based: TCAV, ACE (ex 13–14)
**Livello 6** — Mechanistic interpretability per transformer/LLM (ex 15–19)
**Livello 7** — Survey NN generali (ex 20–23)
**Livello 8** — Survey MI/LLM (ex 24–27)
**Livello 9** — Frontiera e questioni aperte (ex 28–30)

Il percorso di lettura aggiornato parte da: **0a → 0d → 0b → 0c** (capisci il problema) → **1 → 2** (framework concettuale) → poi scegli se andare verso vision (livello 2–4) o verso LLM (livello 6).