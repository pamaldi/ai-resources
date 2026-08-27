# Computational Cognitive Modeling — NYU (Lake & Gureckis)

Corso NYU **PSYCH-GA 3405 / DS-GA 1016**, edizione Spring 2024. Materiale pubblico su GitHub Pages: slide, bibliografia, idee di progetto. I compiti e i video restano dietro credenziali NYU, quindi come risorsa autodidatta vale per **slide + readings + spunti di progetto**, non per l'esperienza completa.

- **Sito**: <https://brendenlake.github.io/CCM-site/>
- **Repo**: <https://github.com/brendenlake/CCM-site>
- **Docenti**: [Brenden Lake](https://cims.nyu.edu/~brenden/) · [Todd Gureckis](https://todd.gureckislab.org/)
- **Prerequisiti reali**: algebra lineare, calcolo, probabilità, Python *già solido*. Non è un corso introduttivo.

---

## Perché conta (per i miei fili)

Il punto di forza vero è che **non è un corso di ML travestito**: il filo conduttore è *modellare la mente*, non massimizzare un'accuratezza. Lo si vede dalla scelta di mettere in bibliografia il dibattito **Jones & Love (*Bayesian Fundamentalism or Enlightenment?*)** e **Griffiths et al. sui livelli di analisi** — cioè fa riflettere su *cosa spiega* un modello (livello computazionale vs algoritmico di Marr), non solo su come implementarlo. È la prospettiva che manca a quasi tutti i corsi di deep learning.

Lake è l'autore del lavoro su *human-level concept learning through probabilistic program induction* (Science 2015, in bibliografia) e di gran parte del dibattito su composizionalità e apprendimento sistematico nelle reti — aggancio diretto a [composizionalita_transformer](../topics/composizionalita_transformer/BIBLIOGRAFIA_composizionalita_transformer.md).

> **Corso gemello.** [Categories and Concepts](nyu-categories-concepts-lake.md), sempre di Lake, è il complemento di *contenuto*: la psicologia dei concetti (teorie, modelli, sviluppo, conceptual combination) di cui questo corso dà i *metodi*. La lezione *Categorization* del CCM lì diventa un semestre.

---

## Mappa: argomenti del corso → fili di ricerca

| Blocco del corso | Filo nel repo | Aggancio |
|---|---|---|
| Program induction, language of thought (Lake 2015, Goodman-Tenenbaum) | [Compressione → astrazione](../topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) · [Intensione/autonomia](../topics/intensione-autonomia/bibliografia.md) | scoperta di primitivi, library learning, riuso algoritmico |
| Reti neurali / PDP (Elman, McClelland-Rogers) | [composizionalita_transformer](../topics/composizionalita_transformer/) | strutture in sequenze, sistematicità |
| Modelli grafici probabilistici (Kemp-Tenenbaum, *discovery of structural form*) | [Reasoning neuro-simbolico](../topics/reasoning-neurosimbolico/neurosimbolico-nlp.md) | struttura latente e inferenza |
| Rational vs mechanistic (Jones-Love, Griffiths) | [Interpretability](../topics/interpretability/papers.md) | livelli di spiegazione, cosa significa "spiegare" un modello |
| Reinforcement learning | [Fondamenti — MDP](stanford-ai-mdp.md) | prediction error, decisione |

---

## Struttura

**Argomenti (14 lezioni)**: reti neurali/deep learning → reinforcement learning → modellazione bayesiana → model comparison & fitting → categorizzazione → modelli grafici probabilistici → program induction / language of thought → active learning → neuroscienze cognitive computazionali.

**Valutazione**: homework 65% + progetto finale 35%. Il progetto (gruppi di 3-4, ~6 pagine in stile paper scientifico) deve connettersi alla mente/comportamento umano, non essere puro ML — [lista di idee](https://brendenlake.github.io/CCM-site/final_project_ideas.html).

**Slide pubbliche** (le più utili da sole): [introduzione](https://brendenlake.github.io/CCM-site/slides/lecture-01-introduction.pdf) · [reti neurali 1](https://brendenlake.github.io/CCM-site/slides/lecture-02-neural_nets.pdf) · [2](https://brendenlake.github.io/CCM-site/slides/lecture-03-neural_nets.pdf) · [RL 1](https://brendenlake.github.io/CCM-site/slides/lecture-04-reinforcementlearning.pdf) · [2](https://brendenlake.github.io/CCM-site/slides/lecture-05-reinforcementlearning.pdf) · [3](https://brendenlake.github.io/CCM-site/slides/lecture-06-reinforcementlearning.pdf) · [bayesian](https://brendenlake.github.io/CCM-site/slides/lecture-07%2B08-bayesian_modeling.pdf) · [model fit](https://brendenlake.github.io/CCM-site/slides/lecture-09-modelfit.pdf) · [categorizzazione](https://brendenlake.github.io/CCM-site/slides/lecture-10-categorization.pdf) · [modelli grafici](https://brendenlake.github.io/CCM-site/slides/lecture-11-graphical_models.pdf) · [active learning](https://brendenlake.github.io/CCM-site/slides/lecture-12-activelearning.pdf) · [program induction](https://brendenlake.github.io/CCM-site/slides/lecture-13-program_induction.pdf) · [neuroscienze](https://brendenlake.github.io/CCM-site/slides/lecture-14-computational_cognitive_neuroscience.pdf)

---

## Bibliografia — i "classici obbligati"

Selezione che regge da sola come reading list, a prescindere dalle lezioni. I più rilevanti per i miei fili in **grassetto**.

**Reti neurali / deep learning**
- McClelland, Rumelhart & Hinton — *The Appeal of Parallel Distributed Processing* (PDP, Vol. I, Ch. 1)
- **Elman (1990) — *Finding structure in time*, Cognitive Science 14(2)**
- McClelland & Rogers (2003) — *The PDP approach to semantic cognition*, Nat. Rev. Neuroscience
- LeCun, Bengio & Hinton (2015) — *Deep learning*, Nature 521
- Peterson, Abbott & Griffiths (2016) — *Adapting Deep Network Features to Capture Psychological Representations*

**Reinforcement learning**
- Gureckis & Love (2015) — *Reinforcement learning: a computational perspective*
- Daw (2013) — *Advanced Reinforcement Learning*
- Niv & Schoenbaum (2008) — *Dialogues on prediction errors*, TiCS 12(7)
- Daw et al. (2006) — *Cortical substrates for exploratory decisions in humans*, Nature 441

**Modellazione bayesiana**
- Tenenbaum & Griffiths (2001) — *Generalization, similarity, and Bayesian inference*, BBS 24(4)
- Tenenbaum, Kemp, Griffiths & Goodman (2011) — *How to grow a mind*, Science 331
- Ghahramani (2015) — *Probabilistic machine learning and AI*, Nature 521
- MacKay (2003) — *Monte Carlo Methods* (cap. 29, *Information Theory, Inference, and Learning Algorithms*)

**Rational vs mechanistic** (il cuore metodologico)
- **Jones & Love (2011) — *Bayesian Fundamentalism or Enlightenment?*, BBS (target article)**
- **Griffiths, Lieder & Goodman (2015) — *Rational use of cognitive resources: levels of analysis...*, TopiCS 7(2)**

**Model comparison & fitting**
- Wilson & Collins (2019) — *Ten simple rules for the computational modeling of behavioral data*, eLife
- Pitt & Myung (2002) — *When a good fit can be bad*, TiCS 6(10)
- Roberts & Pashler (2000) — *How persuasive is a good fit?*, Psych. Review 107

**Modelli grafici probabilistici**
- Charniak (1991) — *Bayesian networks without tears*, AI Magazine
- **Kemp & Tenenbaum (2008) — *The discovery of structural form*, PNAS 105(31)**

**Program induction / language of thought**
- Goodman, Tenenbaum & Gerstenberg (2014) — *Concepts in a probabilistic language of thought*, CBMM
- **Lake, Salakhutdinov & Tenenbaum (2015) — *Human-level concept learning through probabilistic program induction*, Science 350**

**Neuroscienze cognitive computazionali**
- Kriegeskorte & Douglas (2018) — *Cognitive computational neuroscience*, Nat. Neuroscience 21(9)
- Turner et al. (2017) — *Approaches to analysis in model-based cognitive neuroscience*, J. Math. Psych.

---

## Verdetto

Tra le migliori risorse pubbliche sul computational cognitive modeling. Come materiale da archiviare vale alto: slide + reading list + [idee di progetto](https://brendenlake.github.io/CCM-site/final_project_ideas.html) sono usabili subito e si integrano col tema composizionalità già in corso.

**Limiti**: non introduttivo (prerequisiti reali); homework e video non pubblici; taglio 2024 volutamente "senza hype" — inquadra gli LLM come *uno* dei framework, non li insegue. A seconda dell'obiettivo è pregio (fondamenti duraturi) o limite (poco sulle architetture recenti).

**Azioni possibili**
- [ ] Scaricare le slide di *program induction* e *rational vs mechanistic* → alimentano [scoperta-di-astrazioni](../topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) e [interpretability](../topics/interpretability/papers.md)
- [ ] Leggere Elman (1990) e Kemp & Tenenbaum (2008) come ancora per [composizionalita_transformer](../topics/composizionalita_transformer/)
