# Categories and Concepts — NYU (Lake)

Corso NYU **PSYCH-GA 2207**, edizione Fall 2023. Seminario avanzato di psicologia dei concetti, formato lecture-discussion. Complementare al [CCM](nyu-ccm-lake-gureckis.md): quello è un corso di *metodi* (come si costruiscono i modelli), questo è un corso di *contenuto* su un singolo dominio. Stesso docente ([Brenden Lake](https://cims.nyu.edu/~brenden/)), taglio da psicologia, non da data science.

- **Sito**: <https://brendenlake.github.io/CC-site/>
- **Repo**: <https://github.com/brendenlake/CC-site>
- **Textbook**: Greg Murphy, *The Big Book of Concepts* (MIT Press) — la sintesi canonica del campo; il corso è costruito attorno a questo
- **Prerequisiti reali**: coursework in psicologia. **Niente programmazione, niente implementazione** — i modelli si discutono, non si scrivono. Aver fatto il CCM (o algebra lineare + statistica) aiuta a seguire i dettagli di modellazione, ma non è richiesto.

---

## Perché conta (per i miei fili)

Dà il **dominio** su cui la lezione *Categorization* del CCM è solo un'ora. I due corsi sono pensati per stare insieme — Lake lo dice nei prerequisiti («se hai fatto Computational Cognitive Modeling sei in ottima posizione»): il CCM fornisce gli strumenti, questo la genealogia teorica su cui applicarli.

La struttura della prima metà è la sequenza classica delle teorie dei concetti — *classical view → prototipi → esemplari → knowledge/theory view* — cioè esattamente da dove vengono i modelli computazionali di categorizzazione (ALCOVE, il rational model di Anderson, l'approccio bayesiano di Tenenbaum), tutti in programma coi paper primari.

L'ultima settimana — **conceptual combination and exemplar generation** — è lo stesso tema di [Frankland & Greene](../argomenti/composizionalita-transformer/bibliografia.md#6-fondamenti-cognitivi-e-neuroscientifici-della-composizionalità), visto però dal lato psicologico-comportamentale invece che neuroscientifico. Aggancio diretto al filo [composizionalità](../argomenti/composizionalita-transformer/).

---

## Mappa: argomenti del corso → fili di ricerca

| Blocco del corso | Filo nel repo | Aggancio |
|---|---|---|
| Conceptual combination & exemplar generation (Murphy 1988, Ward 1994) | [composizionalità nei Transformer](../argomenti/composizionalita-transformer/) | come si combinano i concetti per formarne di nuovi — lato psicologico di Frankland & Greene |
| Concepts as theories / knowledge view (Murphy & Medin, Barsalou) | [Intensione / autonomia](../argomenti/intensione-autonomia/bibliografia.md) | il significato come teoria, non come lista di feature |
| Modelli bayesiani di apprendimento concettuale (Xu & Tenenbaum, Goodman et al., Kemp & Tenenbaum) | [Compressione → astrazione](../argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) | rule-based concept learning, induzione come inferenza |
| Category-based induction (Osherson et al., Kemp & Tenenbaum 2009) | [Reasoning neuro-simbolico](../argomenti/reasoning/neurosimbolico-nlp.md) | inferenza strutturata su categorie |
| Modelli computazionali (ALCOVE, Anderson rational, AlexNet come contrappunto) | [CCM — lezione Categorization](nyu-ccm-lake-gureckis.md) | espansione del blocco categorizzazione del CCM |

---

## Struttura

**Argomenti (13 settimane)**: introduzione + classical view → prototipi ed esemplari → concepts as theories / knowledge view → **modelli computazionali di category learning (4 settimane)** → organizzazione tassonomica e basic level → category-based induction → concetti nell'infanzia → sviluppo concettuale → categorizzazione e percezione → conceptual combination.

**Valutazione**: response papers settimanali 35% (mini-paper ~600 parole di critica alle letture, su EdStem prima della lezione) + final paper 65% (~12 pagine, review critica della letteratura su un tema del corso; proposal da mezza pagina a metà semestre). Niente esame, niente codice — tutto scrittura.

**Slide pubbliche** (la parte davvero fruibile senza credenziali NYU): [intro/classical](https://brendenlake.github.io/CC-site/lecture_slides/01_introduction.pdf) · [prototipi ed esemplari](https://brendenlake.github.io/CC-site/lecture_slides/02_prototype_exemplar.pdf) · [knowledge view](https://brendenlake.github.io/CC-site/lecture_slides/03_knowledge.pdf) · [modelli p1-2](https://brendenlake.github.io/CC-site/lecture_slides/04_models_part1.pdf) · [modelli p3](https://brendenlake.github.io/CC-site/lecture_slides/05_models_part3.pdf) · [modelli p4](https://brendenlake.github.io/CC-site/lecture_slides/06_models_part4.pdf) · [basic level](https://brendenlake.github.io/CC-site/lecture_slides/07_basic_level.pdf) · [induzione](https://brendenlake.github.io/CC-site/lecture_slides/08_induction.pdf) · [sviluppo 1](https://brendenlake.github.io/CC-site/lecture_slides/09_development.pdf) · [sviluppo 2](https://brendenlake.github.io/CC-site/lecture_slides/10_development.pdf) · [percezione](https://brendenlake.github.io/CC-site/lecture_slides/11_perception.pdf)

---

## Reading list — i classici del dominio

Selezione ordinata per tema, oltre ai capitoli del *Big Book of Concepts* (Murphy). I più rilevanti per i miei fili in **grassetto**.

**Teorie dei concetti**
- Rosch & Mervis (1975) — *Family resemblances: studies in the internal structure of categories*, Cognitive Psychology 7(4)
- Medin & Schaffer (1978) — *Context theory of classification learning* (modello a esemplari), Psych. Review 85
- **Murphy & Medin (1985) — *The role of theories in conceptual coherence*, Psych. Review 92**
- Barsalou (1983) — *Ad hoc categories*, Memory & Cognition 11(3)

**Modelli computazionali di category learning**
- Kruschke (1992) — *ALCOVE: an exemplar-based connectionist model of category learning*, Psych. Review 99
- Anderson (1991) — *The adaptive nature of human categorization* (rational model), Psych. Review 98(3)
- Krizhevsky, Sutskever & Hinton (2012) — *ImageNet classification with deep CNNs* (contrappunto deep learning)
- **Xu & Tenenbaum (2007) — *Word learning as Bayesian inference*, Psych. Review 114(2)**
- **Goodman, Tenenbaum, Feldman & Griffiths (2008) — *A rational analysis of rule-based concept learning*, Cognitive Science 32(1)**
- Rehder (2007) — *Essentialism as a generative theory of classification*

**Tassonomia, induzione, sviluppo, percezione**
- Rosch et al. (1976) — *Basic objects in natural categories*, Cognitive Psychology 8
- Osherson et al. (1990) — *Category-based induction*, Psych. Review 97
- **Kemp & Tenenbaum (2009) — *Structured statistical models of inductive reasoning*, Psych. Review 116(1)**
- Mandler & McDonough (1993) — *Concept formation in infancy*
- Goldstone (1994) — *Influences of categorization on perceptual discrimination*, JEP: General 123(2)

**Conceptual combination** (l'aggancio al filo composizionalità)
- **Murphy (1988) — *Comprehending complex concepts*, Cognitive Science 12(4)**
- **Ward (1994) — *Structured imagination: the role of category structure in exemplar generation*, Cognitive Psychology 27(1)**

---

## Verdetto

Ottima **mappa concettuale del dominio "concetti e categorie"** e complemento naturale al [CCM](nyu-ccm-lake-gureckis.md). Il valore per me è la reading list canonica (Rosch, Medin, Murphy, Kruschke, Anderson, Xu & Tenenbaum, Kemp & Tenenbaum) e l'aggancio dell'ultima settimana al filo composizionalità/LoT.

**Limiti**: non computazionale in senso stretto (discute i modelli, non li implementa — il codice è nel CCM); risorsa pubblica solo per slide + reading list (libro e paper dietro Brightspace/rete NYU); taglio sui fondamenti, non sugli LLM (l'unico cenno moderno è AlexNet come contrappunto).

**Azioni possibili**
- [ ] Scaricare le slide di *conceptual combination* e *knowledge view* → alimentano il filo [composizionalità](../argomenti/composizionalita-transformer/) e [intensione/autonomia](../argomenti/intensione-autonomia/bibliografia.md)
- [ ] Leggere Murphy (1988) e Ward (1994) come lato psicologico-comportamentale di [Frankland & Greene](../argomenti/composizionalita-transformer/bibliografia.md#6-fondamenti-cognitivi-e-neuroscientifici-della-composizionalità)
- [ ] Valutare *The Big Book of Concepts* (Murphy) come testo di riferimento del dominio
