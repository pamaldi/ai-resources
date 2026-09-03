# SemEval 2027 Task 2 — DiCo-NLI

Repository, profili degli organizzatori e letture mirate per **Directional Consistency in Fine-Grained Natural Language Inference**.

Ultima verifica delle fonti: **1 settembre 2026**.

## Nota sul nome e sullo stato

La [pagina centrale dei task SemEval 2027](https://semeval.github.io/SemEval2027/tasks.html) presenta ancora il Task 2 con il nome **CoCo-NLI — Coherence-Aware Compositional Fine Grained Natural Language Inference**. Il [repository degli organizzatori](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI) e la [proposta revisionata](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/blob/main/latex/task_proposal_v2/dico_nli_proposal_v2.tex) usano invece **DiCo-NLI**: la revisione dichiara esplicitamente il cambio da *coherence* a *directional consistency*.

Per cercare comunicazioni e letteratura conviene quindi mantenere entrambi i nomi. Per codice, dati e definizione operativa, il riferimento più aggiornato è il repository DiCo-NLI. Nel README lo stato è indicato come **conditionally accepted for SemEval 2027**; date e regole possono ancora cambiare.

## Link operativi

| Risorsa | Link | Utilità |
|---|---|---|
| Repository ufficiale degli organizzatori | [SemEval-2027-Task-2-DiCo-NLI](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI) | Specifica corrente, news, regole e riferimenti |
| Trial data | [trial_data](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/tree/main/trial_data) | 461 coppie sorgente, file per i quattro track, gold locali e template di submission |
| Starter kit | [starter_kit](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/tree/main/starter_kit) | Fine-tuning Hugging Face, predizione, Optuna e script SLURM |
| Scorer | [evaluation_functions](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/tree/main/evaluation_functions) | Implementazione di weighted F1, SoftCons e HardCons |
| Proposta tecnica revisionata | [dico_nli_proposal_v2.tex](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/blob/main/latex/task_proposal_v2/dico_nli_proposal_v2.tex) | Motivazione, costruzione dei dati, organizzazione e piano di valutazione |
| Pagina centrale SemEval | [SemEval-2027 Tasks](https://semeval.github.io/SemEval2027/tasks.html) | Conferma dell'inclusione del Task 2 e nome storico CoCo-NLI |
| Segnalazioni e domande tecniche | [GitHub Issues](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI/issues) | Canale pubblico preferibile per dubbi riproducibili |

La scadenza preliminare indicata per i training data è il 1 settembre 2026, ma una data nel piano non equivale alla conferma di pubblicazione: prima di iniziare esperimenti estesi va ricontrollato il contenuto effettivo del repository.

## Il task in breve

DiCo-NLI valuta NLI fine-grained su **coppie ordinate di frasi brevi**. Ogni coppia viene presentata anche in ordine inverso, così da misurare sia la correttezza della classificazione sia la compatibilità logica delle due predizioni.

| Etichetta | Etichetta dopo l'inversione |
|---|---|
| **EQUIVALENCE** | **EQUIVALENCE** |
| **FORWARD_ENTAILMENT** | **BACKWARD_ENTAILMENT** |
| **BACKWARD_ENTAILMENT** | **FORWARD_ENTAILMENT** |
| **NEGATIVE_OTHER** | Non entra nelle metriche di consistenza |

I quattro track annunciati sono inglese, spagnolo, basco e mixed multilingual. Le metriche principali sono:

- **weighted F1**: qualità delle etichette sui singoli esempi;
- **SoftCons**: compatibilità delle predizioni nelle due direzioni, anche quando sono entrambe sbagliate;
- **HardCons**: entrambe le direzioni devono essere corrette.

Questo rende il task adatto a un approccio neuro-simbolico: un classificatore neurale può produrre distribuzioni sulle etichette, mentre un secondo livello può imporre o apprendere il vincolo deterministico di inversione. Lo scorer ufficiale permette di separare il guadagno classificativo da quello di consistenza.

## Organizzatori

Tutti e quattro gli organizzatori afferiscono al **HiTZ Basque Center for Language Technology — Ixa NLP Group, University of the Basque Country (UPV/EHU)**.

### Iñigo López-Gazpio — lead organizer

Docente e ricercatore UPV/EHU in intelligenza artificiale e NLP. Il suo profilo per il task è particolarmente centrato su semantic evaluation, Semantic Textual Similarity (STS), semantica fine-grained e progettazione di benchmark. Ha co-organizzato task SemEval su STS e interpretabilità nel 2015, 2016 e 2017; è inoltre il proprietario del repository DiCo-NLI.

Profili e codice: [profilo UPV/EHU](https://ekoizpen-zientifikoa.ehu.eus/investigadores/326367/detalle?lang=en) · [sito personale](https://inigolopezgazpio.net/) · [GitHub](https://github.com/ilopezgazpio)

Lavori più pertinenti:

- **Lopez-Gazpio et al. (2024), [PhrasIS: Phrase Inference and Similarity benchmark](https://doi.org/10.1093/jigpal/jzae037).** È la sorgente dati diretta del task: circa 10.000 coppie di frasi brevi naturali con annotazioni di inferenza e similarità.
- **Apaolaza Larraya et al. (2026), [Assessing Logical Coherence of LLMs via Fine-Grained NLI](https://aclanthology.org/2026.lrec-1.423/).** Pilot immediatamente precedente al task; introduce la valutazione nelle due direzioni e le varianti soft/hard della consistenza.
- **Cer et al. (2017), [SemEval-2017 Task 1: Semantic Textual Similarity Multilingual and Crosslingual Focused Evaluation](https://aclanthology.org/S17-2001/).** Mostra la sua esperienza nella costruzione e valutazione di benchmark semantici multilingue.
- **Lopez-Gazpio (2024), [Revisiting Challenges and Hazards in Large Language Model Evaluation](https://doi.org/10.26342/2024-72-1).** Utile per impostare controlli robusti, evitare metriche fuorvianti e documentare i limiti sperimentali.

### Jon Felix Apaolaza Larraya — co-organizer

Ricercatore pre-dottorale UPV/EHU. Ha guidato il pilot da cui nasce DiCo-NLI e, secondo la proposta, coordina dati, scoring e analisi. La sua linea più direttamente collegata al task riguarda il fallimento degli LLM nel mantenere relazioni inferenziali coerenti quando premise e hypothesis vengono invertite.

Profili: [profilo UPV/EHU](https://ekoizpen-zientifikoa.ehu.eus/investigadores/1998937/detalle?lang=en) · [pubblicazioni UPV/EHU](https://ekoizpen-zientifikoa.ehu.eus/investigadores/1998937/publicaciones?lang=en)

Lavori più pertinenti:

- **Apaolaza, Altuna, Soroa e Lopez-Gazpio (2025), [Exploring the Dilemma of Causal Incoherence: A Study on the Approaches and Limitations of Large Language Models in Natural Language Inference](https://www.ixa.eus/node/14411?language=en).** Analizza il problema della reversal direction in NLI e strategie di mitigazione: è il predecessore concettuale del task.
- **Apaolaza Larraya, Altuna, Soroa e Lopez-Gazpio (2026), [Assessing Logical Coherence of LLMs via Fine-Grained NLI](https://aclanthology.org/2026.lrec-1.423/).** È il paper da leggere per primo per ricostruire dataset, famiglie di modelli, metriche e failure mode del pilot.

### Aitor Soroa — advisory organizer

Professore associato UPV/EHU e membro Ixa/HiTZ. Lavora su elaborazione semantica, word-sense disambiguation, similarità, modelli per il basco e valutazione robusta. È il principale sviluppatore di UKB, sistema graph-based per disambiguazione e similarità lessicale; nel task porta competenze semantiche e di valutazione.

Profili e codice: [pagina accademica](https://ixa2.si.ehu.eus/asoroa/) · [profilo UPV/EHU](https://www.ehu.eus/en/web/doktoregoa/doctorate-informatics-engineering/teaching-staff?idPdi=5133&redirect=fichaPDI) · [ACL Anthology](https://aclanthology.org/people/aitor-soroa/) · [UKB su GitHub](https://github.com/asoroa/ukb)

Lavori più pertinenti:

- **Apaolaza Larraya et al. (2026), [Assessing Logical Coherence of LLMs via Fine-Grained NLI](https://aclanthology.org/2026.lrec-1.423/).** Collegamento diretto con DiCo-NLI e riferimento per l'analisi della consistenza.
- **Urbizu et al. (2022), [BasqueGLUE: A Natural Language Understanding Benchmark for Basque](https://aclanthology.org/2022.lrec-1.172/).** Rilevante per progettare e confrontare il track basco in modo riproducibile.
- **Etxaniz et al. (2024), [Latxa: An Open Language Model and Evaluation Suite for Basque](https://aclanthology.org/2024.acl-long.799/).** Modelli e benchmark per il basco; utile per baseline e transfer nei track 3 e 4.
- **Agirre, López de Lacalle e Soroa (2014), [Random Walks for Knowledge-Based Word Sense Disambiguation](https://aclanthology.org/J14-1003/).** Background per una possibile componente simbolica basata su relazioni semantiche e grafi.

### Rodrigo Agerri — advisory organizer

Ricercatore permanente UPV/EHU, responsabile della Text Analysis Unit di HiTZ e PhD in Computer Science alla City University of London. La sua ricerca riguarda NLP multilingue e cross-lingue, semantic processing, information extraction e LLM, con particolare attenzione a lingue e domini con meno risorse. Nel task contribuisce soprattutto ai track spagnolo, basco e mixed multilingual e alla valutazione dei sistemi.

Profili e codice: [sito personale](https://ragerri.github.io/) · [profilo UPV/EHU](https://www.ehu.eus/en/web/graduak/bachelor-degree-informatics-engineering/teaching-staff?idPdi=288194&redirect=fichaPDI) · [ACL Anthology](https://aclanthology.org/people/rodrigo-agerri/) · [GitHub](https://github.com/ragerri)

Lavori più pertinenti:

- **Bengoetxea, Gonzalez-Dios e Agerri (2025), [Lost in Variation? Evaluating NLI Performance in Basque and Spanish Geographical Variants](https://aclanthology.org/2025.conll-1.30/).** È il riferimento più diretto per i rischi di generalizzazione NLI nelle varianti basche e spagnole.
- **Urbizu et al. (2022), [BasqueGLUE: A Natural Language Understanding Benchmark for Basque](https://aclanthology.org/2022.lrec-1.172/).** Background di benchmark design e baseline NLU per il track basco.
- **Agerri et al. (2020), [Give your Text Representation Models some Love: the Case for Basque](https://aclanthology.org/2020.lrec-1.588/).** Mostra il valore di modelli monolingui e corpora mirati rispetto a modelli multilingui generici.
- **Artetxe et al. (2022), [Does Corpus Quality Really Matter for Low-Resource Languages?](https://aclanthology.org/2022.emnlp-main.499/).** Utile per decidere quantità, copertura di dominio e qualità dei dati nei track low-resource.

## Mappa rapida delle competenze

| Organizzatore | Contributo più riconoscibile per DiCo-NLI |
|---|---|
| Iñigo López-Gazpio | PhrasIS, STS, benchmark design e valutazione semantica |
| Jon Felix Apaolaza Larraya | Pilot reversal-aware, metriche di consistenza, dati e scorer |
| Aitor Soroa | Semantic processing, risorse basche e valutazione robusta |
| Rodrigo Agerri | NLP multilingue/cross-lingue, low-resource NLU e system evaluation |

## Ordine di lettura consigliato

1. [README e trial data DiCo-NLI](https://github.com/ilopezgazpio/SemEval-2027-Task-2-DiCo-NLI): formato reale, label algebra, track e scorer.
2. [Assessing Logical Coherence of LLMs via Fine-Grained NLI](https://aclanthology.org/2026.lrec-1.423/): il pilot più vicino al task.
3. [PhrasIS](https://doi.org/10.1093/jigpal/jzae037): provenienza e significato delle annotazioni.
4. [Exploring the Dilemma of Causal Incoherence](https://www.ixa.eus/node/14411?language=en): failure mode e possibili mitigazioni.
5. [Lost in Variation?](https://aclanthology.org/2025.conll-1.30/) e [BasqueGLUE](https://aclanthology.org/2022.lrec-1.172/): preparazione dei track multilingui.
6. Come riferimento esterno esplicitamente richiamato dagli organizzatori: Berglund et al. (2024), [The Reversal Curse](https://proceedings.iclr.cc/paper_files/paper/2024/hash/5178b2f2d7c44aa390c0777dc77b3f0c-Abstract-Conference.html). Il task ne riprende il principio di stress test per inversione, ma non valuta la stessa forma di memoria fattuale parametrica.

## Indicazione progettuale

La strada più naturale per riusare una pipeline neuro-simbolica è partire da un encoder multilingue fine-tuned sulle quattro etichette e aggiungere una loss o un reranker di consistenza sulla coppia originale/invertita. Le ablation minime dovrebbero confrontare:

- baseline senza vincolo;
- data augmentation con coppie invertite;
- loss congiunta su label e consistenza;
- correzione post-hoc o constrained decoding;
- risultati separati per weighted F1, SoftCons e HardCons, per evitare di confondere accuratezza e autoconsistenza.

