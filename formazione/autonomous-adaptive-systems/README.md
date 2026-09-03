# Autonomous and Adaptive Systems — UniBO (Musolesi)

Corso UniBO **92858**, 8 CFU, ING-INF/05, in inglese, in presenza. Vale per la LM in **Artificial Intelligence** (cod. 9063) e per la LM in **Computer Engineering** (cod. 5826). Edizione 2025/26: **27 febbraio – 5 giugno 2026**.

- **Docente**: [Mirco Musolesi](https://www.mircomusolesi.org/) — UCL, Department of Computer Science · UniBO, DISI
- **Scheda ufficiale**: <https://www.unibo.it/en/study/course-units-transferable-skills-moocs/course-unit-catalogue/course-unit/2025/468076>
- **Materiale**: [slide di tutte le lezioni](https://www.mircomusolesi.org/courses/AAS25-26/AAS25-26-main), pubbliche e scaricabili senza credenziali
- **Esame**: orale (90%) con **progetto di ricerca obbligatorio** da consegnare prima dell'orale — implementazione e valutazione di un algoritmo, con relazione in forma di paper — più partecipazione (10%)
- **Testi consigliati**: Richard S. Sutton e Andrew G. Barto, *Reinforcement Learning: An Introduction* · Christopher M. Bishop e Hugh Bishop, *Deep Learning: Foundations and Concepts* · Dario Floreano e Claudio Mattiussi, *Bio-inspired Artificial Intelligence* · Stuart Russell e Peter Norvig, *Artificial Intelligence: A Modern Approach*

---

## Perché conta (per i miei fili)

**È l'ossatura di RL che all'archivio manca.** Il [filo 6](../../README.md#6-fondamenti) oggi ha solo gli [appunti Stanford su MDP, V e Q](../stanford-ai-mdp.md): una definizione isolata. Qui c'è la sequenza intera e nell'ordine canonico di Sutton e Barto — bandit → Monte Carlo → differenze temporali → approssimazione di valore → policy gradient — con le slide pubbliche. È la risorsa che rende leggibili gli altri dossier quando usano "reward", "policy" o "valore" senza definirli.

**Dà la definizione *ingegneristica* di autonomia, ed è in tensione con quella dell'archivio.** La lezione *Intelligent Agents* definisce l'agente autonomo come entità che si basa solo sulla propria percezione, agisce indipendentemente dal progettista e deve compensare la conoscenza parziale; l'autonomia si conquista imparando, fino a rendersi «effectively independent of its prior knowledge». È la linea di Stuart Russell e Peter Norvig. Il [filo 2](../../topics/intensione-autonomia/bibliografia.md) usa la stessa parola per un'altra cosa: in **Peter Cariani, *Epistemic Autonomy through Adaptive Sensing*** autonomo è il dispositivo che si costruisce nuovi sensori, cioè che estende il proprio alfabeto invece di ricombinare quello ricevuto. Le due definizioni non si contraddicono, si ignorano — e la seconda è precisamente ciò che la prima dà per scontato. Vale come voce nel dossier intensione/autonomia, non come nota a margine.

**Il gap è lo stesso già rilevato su Cognitive Neuroscience.** Il syllabus copre l'apprendimento del *valore* (bandit, TD, approssimazione, policy gradient) ma non l'astrazione dell'*azione*: niente option, niente hierarchical RL, niente skill discovery. È esattamente la lacuna annotata in [corsi.md §2](../corsi.md) per il corso di Starita e Di Pellegrino, e il motivo per cui [scoperta-di-astrazioni](../../topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) resta il posto dove quel pezzo va cercato.

**Una delle letture del corso è del docente stesso** ed è il ponte con il lato generativo: **Giorgio Franceschelli e Mirco Musolesi, *Reinforcement Learning for Generative AI: State of the Art, Opportunities and Open Research Challenges*** (Journal of Artificial Intelligence Research, 2024) — RL come modo di generare senza obiettivo specificato, di massimizzare un obiettivo durante la generazione, e di iniettare nel processo generativo caratteristiche che una funzione obiettivo non cattura. Copia locale in [papers/](papers/).

---

## Mappa: lezioni → fili di ricerca

| Blocco del corso | Filo nel repo | Aggancio |
|---|---|---|
| Intelligent Agents — definizioni di agente intelligente, adattivo, autonomo | [Intensione e autonomia](../../topics/intensione-autonomia/bibliografia.md) | la definizione ingegneristica di autonomia accanto a quella epistemica di Cariani; le due non si citano |
| Introduction to RL · Bandits · Monte Carlo · Temporal Difference | [Fondamenti — MDP](../stanford-ai-mdp.md) | il seguito naturale degli appunti Stanford: dalla definizione di V e Q agli algoritmi che le stimano |
| Value Approximation · Policy Gradient | [Fondamenti](../../topics/fondamenti-cs/risorse-cs.md) | dove il RL smette di essere tabellare e diventa deep |
| Deep Learning and Neural Architectures (3 parti) | [Interpretability](../../topics/interpretability/papers.md) | l'architettura che la mech interp poi apre |
| Multi-agent Systems | [Reasoning neuro-simbolico](../../topics/reasoning-neurosimbolico/llm-reasoning.md) · [corsi.md — Bellucci](../corsi.md) | coordinazione e teoria dei giochi; l'aggancio speech act ↔ FIPA-ACL è già annotato nella scheda di Philosophy of Language |
| Generative Learning and LLM Agents | [LLM](../../topics/llm/watermarking-llm-sampling.md) · [inbox](../../inbox.md) | RLHF, agenti generativi; la survey sugli LLM-based autonomous agents in inbox appartiene qui |
| Machine Creativity (seminario Franceschelli) | [Compressione → astrazione](../../topics/compressione-astrazione/sintesi-compressione-astrazione.md) | generazione vincolata e novità: il lato produttivo della domanda sull'astrazione |

---

## Cosa c'è in locale

- [`AAS25-26_IntelligentAgents.pdf`](AAS25-26_IntelligentAgents.pdf) — lezione 2, 54 slide.
- [`papers/`](papers/) — **9 paper citati nelle slide**, scaricati e verificati, con [indice ragionato e citazioni complete](papers/README.md).

Sulla lezione, due note di lettura:

- **I riferimenti non sono in bibliografia.** La slide *Suggested Readings* cita un solo testo (Stuart Russell e Peter Norvig, *Artificial Intelligence: A Modern Approach*, quarta edizione, capitolo 2). Tutti gli altri riferimenti sono **screenshot della prima pagina del paper**, senza didascalia: per ricostruirli è stato necessario leggere le immagini delle slide, non il testo del PDF. Vale la pena saperlo prima di cercare una bibliografia che non c'è.
- **Il deck è un aggiornamento incrementale.** Molte slide portano ancora il piè di pagina *2024-2025*: il materiale nuovo dell'edizione 2025/26 è concentrato nella parte su agenti generativi e LLM.

---

## Il resto del materiale pubblico (non ancora scaricato)

Tutte le lezioni sono su <https://www.mircomusolesi.org/courses/AAS25-26/AAS25-26-main>:

**Teoria** — Introduction to the Course · *Intelligent Agents* (in locale) · Introduction to Reinforcement Learning · Multi-armed Bandits · Monte Carlo Methods · Temporal Difference Methods · Deep Learning and Neural Architectures (parti 1-3) · Value Approximation Methods · Policy Gradient Methods (parti 1-2) · Multi-agent Systems · Generative Learning and LLM Agents · Machine Creativity (seminario di Giorgio Franceschelli)

**Laboratori** — Introduction to Gym · Introduction to TensorFlow · Advanced TensorFlow for Reinforcement Learning

**Progetto** — Project Guidelines

---

## Verdetto

Come materiale autodidatta vale alto e costa zero: slide pubbliche, sequenza RL completa e ordinata, e un docente che sul lato generativo pubblica la survey di riferimento. Non ha i vincoli delle risorse NYU dell'archivio ([CCM](../nyu-ccm-lake-gureckis.md), [Categories and Concepts](../nyu-categories-concepts-lake.md)), dove video e compiti restano dietro credenziali: qui il materiale è tutto quello che c'è, e c'è tutto.

**Limiti**: le slide sono supporto alla lezione, non dispense — dense di figure e povere di prosa, si leggono bene solo con Sutton e Barto accanto. Niente astrazione dell'azione (option, hierarchical RL). Il taglio è ingegneristico: l'autonomia è una proprietà da progettare, non una domanda da porre — l'opposto del registro del [filo 2](../../topics/intensione-autonomia/bibliografia.md), ed è proprio per questo che serve confrontarli.

**Azioni possibili**

- [ ] Scaricare le slide di *Introduction to RL*, *Multi-armed Bandits*, *Monte Carlo Methods* e *Temporal Difference Methods* → chiudono il buco fra [stanford-ai-mdp.md](../stanford-ai-mdp.md) e il resto dell'archivio
- [ ] Portare la tensione fra le due definizioni di autonomia (Russell e Norvig vs Cariani) nella [bibliografia intensione/autonomia](../../topics/intensione-autonomia/bibliografia.md) — è una convergenza non dichiarata, del tipo che la [bibliografia trasversale §3](../../bibliografia-trasversale.md) esiste per intercettare
- [ ] Leggere **Giorgio Franceschelli e Mirco Musolesi, *Reinforcement Learning for Generative AI*** e decidere se apre una voce nel filo LLM o resta materiale di corso
- [ ] Verificare se le slide di *Generative Learning and LLM Agents* rendono superflua la survey sugli LLM-based autonomous agents ferma in [inbox.md](../../inbox.md)
