# Physical AI — mappa mondiale dei corsi e piano di studio

*Versione consolidata — agosto 2026*

Questa mappa raccoglie corsi universitari e materiali pubblici su **Robot Learning, Embodied AI, Physical AI, Reinforcement Learning, World Models e Vision-Language-Action models**.

La premessa importante è che **“Physical AI” non è ancora una denominazione accademica standard**. Nei cataloghi universitari gli stessi temi compaiono soprattutto sotto:

- **Robot Learning**
- **Embodied AI / Embodied Intelligence**
- **Sensorimotor Learning**
- **Robot Autonomy**
- **Learning-based Robotics**
- **Reinforcement Learning for Robotics**

Il campo che ci interessa può essere schematizzato così:

**percezione → rappresentazione del mondo → decisione → planning → controllo → azione fisica → feedback → apprendimento**

---

# 1. I cinque corsi principali

## 1. CMU 16-831 — Introduction to Robot Learning

**Carnegie Mellon University — Spring 2024**

### Ruolo nella mappa

È probabilmente il miglior **corso di fondazione sistematico** della lista.

Non parte direttamente dai VLA: costruisce prima il linguaggio necessario per comprenderli.

Il corso comprende una progressione molto ordinata:

| Lezioni | Argomento |
|---|---|
| 1–2 | Introduzione al Robot Learning |
| 3–4 | ML / Deep Learning refresher |
| 5–6 | Imitation Learning |
| 7–11 | Model-free Reinforcement Learning |
| 12–16 | Model-based RL e Optimal Control |
| 17–18 | Offline RL e Inverse RL |
| 19–20 | Bandits ed Exploration |
| 21 | Simulation e Sim2Real |
| 22 | Safe Robot Learning |
| 23 | Multi-task / Transfer |
| 24 | Foundation Models in Robotics |

Le lezioni arrivano quindi da value iteration, DQN e policy gradient fino a **Dreamer, TD-MPC, world models strutturati, offline RL, Diffuser, sim-to-real e foundation models**.

### Le lezioni particolarmente importanti

**L16 — Structured World Models**

Il robot non deve necessariamente modellare il mondo come una gigantesca immagine. Può imparare dinamiche su rappresentazioni strutturate di oggetti ed entità.

**L17 — Offline RL**

Cruciale quando non è possibile fare milioni di tentativi direttamente nel mondo reale.

**L19–20 — Bandits ed exploration**

È il ponte verso sistemi che devono scegliere cosa esplorare e quali esperimenti effettuare.

**L21 — Sim2Real**

Come trasferire una politica imparata in simulazione al sistema fisico.

**L24 — Foundation Models in Robotics**

SayCan, CLIPort, RT-1, Code as Policies.

### Perché partire da qui

Gli altri corsi spesso presentano lavori di frontiera assumendo già familiari:

- MDP
- Q-learning
- policy gradients
- actor-critic
- model-based RL
- imitation learning
- offline RL

CMU li costruisce progressivamente.

**Valutazione: ★★★★★ — corso base ideale**

---

# 2. ETH Zürich — Robot Learning: From Fundamentals to Foundation Models

**ETH Zürich — Spring 2026 — Oier Mees**

Questo è probabilmente il **corso pubblico più vicino alla definizione moderna di Physical AI**.

Il titolo stesso è significativo:

> **Robot Learning: From Fundamentals to Foundation Models**

Parte dalle basi e arriva direttamente alla frontiera 2026.

### Programma

1. Introduction to Robot Learning
2. Robot Control & MDPs
3. Imitation Learning
4. Reinforcement Learning I
5. Reinforcement Learning II
6. Generative Models
7. Sequence Modeling and Transformers
8. **World Models**
9. **Generalist Robot Policies**
10. **Embodied Reasoning and Test-time Scaling**
11. Frontier & Open Problems

Il corso dichiara esplicitamente come obiettivo quello di passare da imitation/RL e policy learning fino a **Vision-Language-Action models e foundation models per la robotica**.

### Perché è particolarmente importante

ETH collega in un solo percorso:

**Robot Control**
↓  
**Imitation Learning**
↓  
**RL**
↓  
**Generative Models**
↓  
**Transformers**
↓  
**World Models**
↓  
**VLA / Generalist Policies**
↓  
**Embodied Reasoning**

È precisamente la sequenza concettuale che manca in molti corsi precedenti al 2024.

### Materiale

Un altro enorme vantaggio è la disponibilità pubblica di:

- slide;
- registrazioni;
- paper;
- esercitazioni;
- codice.

Sono presenti anche tutorial pratici su PyTorch, robot control, MDP, imitation learning e RL.

### Le lezioni che considero più importanti

**Generative Models**

Diffusion/planning e politiche generative.

**Transformers**

Decision Transformer, ALOHA e controllo visto come sequence modeling.

**World Models**

Qui compare esplicitamente anche *World Action Models are Zero-shot Policies* del 2026.

**Generalist Robot Policies**

Il passaggio dai singoli task a modelli generalisti.

**Embodied Reasoning**

Il problema diventa non soltanto generare un'azione, ma ragionare durante l'interazione con il mondo.

### Posizione nella sequenza

Se CMU insegna il **vocabolario**, ETH mostra come quel vocabolario si sta trasformando nella **Physical AI moderna**.

**Valutazione: ★★★★★+ — corso centrale**

---

# 3. Berkeley CS 294-277 — Robots That Learn

**UC Berkeley — Spring 2026 — Jitendra Malik**

Questo rimane il corso più interessante se con Physical AI intendiamo letteralmente:

> **intelligenza che deve controllare un corpo nel mondo fisico.**

Malik struttura il corso attorno a tre componenti:

1. basi biologiche del controllo motorio;
2. paradigmi di acquisizione delle skill;
3. locomozione, navigazione e manipolazione.

La caratteristica particolare è la preferenza esplicita per **gambe rispetto a ruote, mani multi-dito rispetto alle pinze, percezione visiva e tattile ricca e umanoidi negli ambienti quotidiani**.

## Blocchi

### A. Embodiment biologico

- biomeccanica;
- controllo motorio;
- mano umana;
- propriocezione;
- tatto;
- sviluppo delle capacità motorie.

È ciò che distingue maggiormente Berkeley da un normale corso di ML.

### B. Robotica fisica

- cinematica;
- dinamica;
- motion planning;
- robot control.

### C. Modelli generativi

- normalizing flows;
- flow matching;
- behavior cloning;
- visual imitation;
- Diffusion Policy;
- UMI.

### D. World models e frontiera

- Video World Models;
- sim-to-real;
- dexterous manipulation;
- long-horizon planning;
- VLA;
- π0.5;
- MolmoSpaces.

La struttura originale che avevi raccolto distingue molto bene questi blocchi.

### Differenza rispetto a ETH

**ETH**

> Come costruiamo oggi modelli generalisti che imparano a controllare robot?

**Berkeley**

> Che cosa significa realmente collegare percezione, apprendimento e controllo di un corpo?

Sono complementari.

**Valutazione: ★★★★★ — miglior corso per embodiment e motor intelligence**

---

# 4. University of Washington — CSE 571 AI-Robotics

**University of Washington — Winter 2026 — Dieter Fox**

Questo corso colma una lacuna importante degli altri:

> **la robotica classica necessaria prima del robot learning moderno.**

Parte infatti da:

- Bayes filters;
- motion/sensor models;
- particle filters;
- Kalman filters;
- mapping;
- path planning;
- RRT.

Poi passa a:

- manipulation;
- rigid-body transformations;
- kinematics;
- RL;
- imitation learning.

Infine arriva a:

- Transformers;
- PerAct;
- ACT;
- DDPM;
- Diffusion Policy;
- data collection;
- VLA;
- OpenVLA.

### È quindi un corso particolarmente equilibrato

**Probabilistic Robotics**
↓  
**Planning**
↓  
**Kinematics**
↓  
**Manipulation**
↓  
**RL / Imitation**
↓  
**Diffusion**
↓  
**VLA**

### Libri di riferimento

Il corso utilizza soprattutto:

- *Probabilistic Robotics* — Thrun, Burgard & Fox
- *Modern Robotics* — Lynch & Park.

### Quando studiarlo

Non lo userei per sostituire CMU.

Lo userei per riempire il lato:

> **“Ma fisicamente, come funziona un robot?”**

che un percorso troppo ML-centrico rischia di trascurare.

**Valutazione: ★★★★★ — miglior ponte robotica classica ↔ Physical AI**

---

# 5. Stanford CS237B — Principles of Robot Autonomy II

**Stanford**

Altro corso molto importante perché mette insieme:

- reinforcement learning;
- optimal control;
- contact dynamics;
- prehensile manipulation;
- non-prehensile manipulation;
- imitation learning;
- human intent inference;
- robot architectures.

L'obiettivo ufficiale è insegnare a costruire robot capaci di **apprendere autonomamente nuove skill e interagire fisicamente con l'ambiente e con esseri umani**.

Gli studenti implementano inoltre i concetti su piattaforme di mobile manipulation e utilizzano ROS.

### Perché è complementare

CMU ed ETH sono maggiormente:

**learning-centric**

Stanford CS237B è maggiormente:

**learning + dynamics + manipulation + interaction**

**Valutazione: ★★★★½**

---

# 6. Secondo gruppo: corsi specialistici molto utili

## Seoul National University — Robot Learning

**Spring 2026**

È più RL-centrico rispetto a Berkeley/ETH, ma l'edizione 2026 è decisamente interessante.

Comprende:

- MDP/POMDP;
- behavior cloning;
- DAgger;
- DQN;
- policy gradients;
- TRPO/PPO;
- actor-critic;
- maximum-entropy RL;
- inverse RL;
- GAIL;
- safe RL;
- offline RL.

E soprattutto l'edizione 2026 aggiunge esplicitamente:

### Vision-Language-Action Models

con letture su:

- RT-1;
- RT-2;
- Open X-Embodiment;
- Octo;
- OpenVLA;
- CogACT;
- π0;
- GR00T N1.



Questo lo rende molto più interessante rispetto alla semplice descrizione “corso di deep RL”.

**Valutazione: ★★★★½**

---

# 7. Stanford EE/CS 381 — Sensorimotor Learning for Embodied Agents

**Shuran Song — materiale 2023**

È un seminario, non il corso da cui partire.

Il suo valore sta in alcuni temi poco coperti altrove.

### Co-design hardware/software

La morfologia stessa del robot diventa parte del problema di apprendimento.

Non:

**corpo fisso → impara controller**

ma potenzialmente:

**impara struttura del corpo + controller**

### Multimodalità

Oltre alla visione:

- tatto;
- audio;
- propriocezione;
- interazione con oggetti deformabili.

### Benchmark e Sim2Real

Come capire se un risultato ottenuto in simulazione rappresenta davvero progresso nel mondo fisico.

### Code as Policies

Interessante perché invece di produrre direttamente traiettorie continue, un LLM può generare **programmi eseguibili** che vengono poi verificati/eseguiti.

Il limite è temporale: il materiale raccolto è del 2023 e precede buona parte dell'attuale ondata VLA/world-model.

**Valutazione: ★★★★ — da studiare selettivamente**

---

# 8. Stanford CS422 — Interactive and Embodied Learning

**Winter 2026 — Nick Haber**

Il nome può trarre in inganno:

**non è un corso di robotica fisica.**

È interessante per un'altra ragione.

Studia come dovrebbe apprendere un agente che può:

- esplorare;
- scegliere problemi;
- costruirsi un curriculum;
- migliorare durante l'interazione;
- fare self-play;
- usare intrinsic motivation.

Nel materiale raccolto emergono in particolare:

- Minimo;
- Quiet-STaR;
- self-play;
- auto-curriculum;
- test-time training;
- energy-based models;
- looped transformers.



È quindi un corso parallelo sulla domanda:

> **Come passa un modello dall'apprendere passivamente un dataset all'apprendere attivamente tramite interazione?**

Questo problema potrebbe rivelarsi fondamentale anche per la futura Physical AI.

**Valutazione: ★★★★ — parallelo concettuale**

---

# 9. MIT 6.S186 — Modern Robot Learning

**MIT IAP 2025**

Corso breve ma molto interessante perché estremamente pratico.

Gli argomenti dichiarati comprendono:

- robot data collection;
- Action Chunking Transformer;
- Diffusion Policy;
- MuJoCo;
- Real2Sim;
- Sim2Real;
- training di policy.

Gli studenti raccolgono dati tramite teleoperazione, costruiscono ambienti simulati e addestrano una policy per eseguire autonomamente un task.

Non è equivalente a un semestre universitario, ma è probabilmente uno dei migliori complementi pratici.

**Valutazione: ★★★★ per pratica; ★★½ come corso teorico completo**

---

# 10. UCL — IEEE RAS Embodied Intelligence Summer School

**Londra — 6–10 luglio 2026**

È durata soltanto cinque giorni, ma il programma è quasi una miniatura dell'intero stack Physical AI:

### Day 1
State estimation + SLAM

### Day 2
Navigation + planning + safety

### Day 3
Humanoid dynamics + whole-body control

### Day 4
Dexterous manipulation + tactile sensing + VLA

### Day 5
Project e dimostrazioni su hardware.

Sono previste simulazioni e lavoro su robot reali.

Molto interessante per capire quale sia ormai il **curriculum implicito della Physical AI**:

**state estimation → planning → whole-body control → manipulation → VLA**

**Valutazione: ★★★★ come immersione pratica**

---

# 11. EPFL — Learning and Adaptive Control for Robots

Questo corso va classificato diversamente.

Non è centrato sui foundation models.

Studia soprattutto:

- dynamical systems;
- learning control laws;
- stability guarantees;
- obstacle avoidance;
- force control;
- impedance control;
- robust manipulation.

È quindi prezioso per capire il lato:

> **Come garantisco che un robot fisico rimanga stabile e controllabile?**

Il booklet EPFL 2025-26 specifica però che il corso **non è stato erogato nel 2025-26** ed è offerto ogni due anni.

**Valutazione: ★★★½ — ottimo complemento di controllo, non corso centrale di Physical AI**

---

# 12. MIT — AI in Robotics: Learning Algorithms, Design and Safety

**MIT Professional Education — luglio 2026**

È un corso professionale di soli **3 giorni**, non un corso universitario semestrale.

Comprende:

- reinforcement learning;
- imitation learning;
- simulazione e sim-to-real;
- LLM;
- generative AI;
- robot design;
- multi-agent control;
- verification;
- safety.

Costo dell'edizione 2026: **$3.750**.

Concettualmente interessante, ma per studio autonomo il rapporto contenuto/costo è molto meno interessante dei materiali pubblici ETH/CMU/Berkeley.

---

# La mappa complessiva

Possiamo ora organizzare tutti questi corsi per ciò che insegnano davvero.

| Problema | Corso migliore |
|---|---|
| Fondamenti Robot Learning | **CMU 16-831** |
| Physical AI moderna end-to-end | **ETH Robot Learning 2026** |
| Embodiment / motor intelligence | **Berkeley Robots That Learn** |
| Robotica classica + AI moderna | **Washington CSE571** |
| Manipulation + autonomy | **Stanford CS237B** |
| Deep/Offline/Safe RL + VLA | **SNU Robot Learning** |
| Sensorimotor / multimodalità | **Stanford EE381** |
| Self-learning / agentic learning | **Stanford CS422** |
| ACT / Diffusion Policy pratica | **MIT 6.S186** |
| Humanoids + hardware + VLA | **UCL Summer School** |
| Stable/adaptive control | **EPFL** |

---

# Il curriculum ideale

Se dovessi costruire **un unico “Master virtuale in Physical AI” usando questi corsi**, non li seguirei tutti dall'inizio alla fine.

Li combinerei.

## Fase 0 — prerequisiti

### Deep Learning

**Bishop & Bishop — Deep Learning: Foundations and Concepts**

### Reinforcement Learning

**Sutton & Barto — Reinforcement Learning: An Introduction**

### Robotica

**Lynch & Park — Modern Robotics**

Per:

- coordinate transformations;
- kinematics;
- dynamics;
- trajectory generation;
- motion planning;
- manipulation.

### Probabilistic Robotics

**Thrun, Burgard & Fox — Probabilistic Robotics**

Per:

- state estimation;
- Kalman filtering;
- particle filtering;
- localisation;
- mapping;
- SLAM.

---

# Fase 1 — imparare veramente il Robot Learning

## CMU 16-831

Studiare almeno:

**L5–6**
Imitation learning

**L7–11**
Model-free RL

**L12–15**
Model-based RL

**L16**
Structured World Models

**L17**
Offline RL

**L19–20**
Exploration

**L21**
Sim2Real

**L23**
Transfer

**L24**
Foundation Models

Questo crea la base algoritmica.

---

# Fase 2 — entrare nella Physical AI 2026

## ETH Robot Learning

Seguire integralmente soprattutto dalla Week 3 in poi:

**Imitation Learning**
↓
**RL**
↓
**Generative Models**
↓
**Transformers**
↓
**World Models**
↓
**Generalist Robot Policies**
↓
**Embodied Reasoning**

ETH è il passaggio naturale da:

> “So cos'è il robot learning”

a:

> “Capisco cosa sta succedendo oggi con VLA e foundation models”.

---

# Fase 3 — capire perché avere un corpo cambia il problema

## Berkeley — Robots That Learn

Prendere soprattutto:

### Biologia e embodiment

- locomozione biologica;
- mani;
- tatto;
- propriocezione;
- motor control.

### Generative robot learning

- flow matching;
- behavior cloning;
- visual imitation;
- Diffusion Policy.

### Frontiera

- Video World Models;
- dexterous manipulation;
- π0.5;
- MolmoSpaces;
- long-horizon planning.

Qui si capisce che Physical AI **non significa semplicemente mettere un LLM dentro un robot**.

---

# Fase 4 — recuperare la robotica che il machine learning tende a nascondere

## Washington CSE571

Studiare:

- Bayes filters;
- Kalman/particle filters;
- SLAM;
- planning;
- kinematics;
- manipulation.

Oppure utilizzare:

## MIT Robotic Manipulation — Russ Tedrake

come testo/corso parallelo.

---

# Fase 5 — specializzarsi

A questo punto sceglierei in funzione della domanda scientifica.

### Autonomy + interaction

→ Stanford CS237B

### Offline/Safe RL

→ SNU

### Morphology / tactile / multimodal

→ Stanford EE381

### Agentic learning / self-generated curriculum

→ Stanford CS422

### ACT / Diffusion Policy / data collection

→ MIT 6.S186

### Stability e adaptive control

→ EPFL

---

# I quattro filoni di ricerca che emergono

Dopo aver fuso tutti questi corsi, secondo me il campo diventa molto più leggibile.

## 1. Learning policies

**osservazione → azione**

Behavior cloning, RL, Diffusion Policy, ACT, VLA.

---

## 2. Learning world models

**stato → previsione del futuro**

Dreamer, TD-MPC, structured world models, video world models, world-action models.

La domanda è:

> un sistema può imparare una rappresentazione causale/dinamica del mondo sufficientemente buona da pianificare?

---

## 3. Generalist robotics

Da:

**un robot + un task**

a:

**un modello + molti robot + molti task**

Qui entrano:

- RT-X;
- Octo;
- OpenVLA;
- π0;
- π0.5;
- GR00T;
- generalist robot policies.

---

## 4. Autonomous learning

Questo è forse il problema ancora più profondo.

Non soltanto:

> “come eseguo un compito che qualcuno mi ha dato?”

ma:

> **“come faccio a sapere che cosa devo imparare?”**

Entrano:

- exploration;
- intrinsic motivation;
- self-play;
- automatic curricula;
- continual learning;
- test-time adaptation;
- embodied reasoning.

Ed è qui che Stanford CS422 diventa interessante pur non essendo un corso di robotica.

---

# Una sequenza consigliata definitiva

```text
Bishop / basi Deep Learning
          +
Sutton & Barto / Reinforcement Learning
          +
Modern Robotics
          │
          ▼
CMU 16-831
Robot Learning foundations
          │
          ▼
ETH Zürich 2026
Robot Learning → Foundation Models
          │
          ├───────────────┐
          ▼               ▼
Berkeley 294-277       Washington CSE571
Embodiment             Robotica classica
Motor intelligence     + manipulation
          │               │
          └───────┬───────┘
                  ▼
        Stanford / SNU / MIT
         moduli specialistici
                  │
                  ▼
      progetto personale / ricerca
```

---

# Se volessi ridurre tutto a quattro corsi

La scelta sarebbe:

## 1. CMU 16-831
Per capire **come apprendono le policy**.

## 2. ETH Robot Learning 2026
Per capire **foundation models, world models e VLA**.

## 3. Berkeley Robots That Learn
Per capire **embodiment e interazione fisica**.

## 4. Washington CSE571
Per non perdere **robotica, state estimation, planning e manipulation**.

Insieme costituiscono un curriculum sorprendentemente completo:

**robotica**
+
**deep learning**
+
**reinforcement learning**
+
**imitation learning**
+
**generative modeling**
+
**world models**
+
**embodiment**
+
**VLA**
+
**generalist policies**

---

# Versione minima: circa 3 mesi

Se l'obiettivo non è seguire cinque semestri virtuali ma arrivare velocemente alla frontiera:

### Blocco 1 — RL
**CMU L7–17**

Da Q-learning a actor-critic, model-based RL, world models e offline RL.

### Blocco 2 — Robot policies moderne
**ETH: Imitation + Generative Models + Transformers**

Capire:

**BC → ACT → Diffusion → sequence models**

### Blocco 3 — World Models
**CMU L16 + ETH World Models + Berkeley Video World Models**

Confrontare:

- stato strutturato;
- latent state;
- pixel/video;
- action-conditioned prediction.

### Blocco 4 — Foundation/VLA
**ETH Generalist Robot Policies + SNU VLA + Berkeley Lecture 12**

Da RT-1/RT-2 fino a OpenVLA, π0/π0.5 e modelli generalisti.

### Blocco 5 — Embodiment
Dal Berkeley:

- tatto;
- propriocezione;
- locomozione;
- manipulation.

### Mini-progetto

Riprodurre in simulazione almeno una policy:

**Diffusion Policy / ACT**

e studiare:

- generalizzazione;
- failure cases;
- distribuzione dei dati;
- comportamento fuori distribuzione.

---

# Materiali di supporto

## Reinforcement Learning

**Berkeley CS285 — Deep Reinforcement Learning — Sergey Levine**

**Stanford CS224R — Deep Reinforcement Learning — Chelsea Finn**

Da usare quando CMU introduce un argomento troppo rapidamente.

---

## Robotica e manipolazione

**MIT — Robotic Manipulation — Russ Tedrake**

Libro online + notebook.

**MIT OCW 6.4210 — Robotic Manipulation**

Lezioni video complete.

---

## Altri seminari

**UT Austin CS391R — Robot Learning**

Buona raccolta di paper e slide.

**Stanford Robotics Seminar**

Per seguire la ricerca corrente.

**CVPR 2026 — The Full Stack of Physical AI**

Tutorial breve e molto pratico sullo stack VLA contemporaneo.

---

# Conclusione

Non esiste ancora un singolo corso che possa essere chiamato:

> **“Teoria completa della Physical AI”**

perché il settore stesso sta emergendo dall'unione di discipline che storicamente erano separate:

```text
Robotics
   +
Control
   +
Computer Vision
   +
Machine Learning
   +
Reinforcement Learning
   +
Generative Models
   +
Language Models
   +
Embodied Cognition
```

Ma mettendo insieme **CMU + ETH + Berkeley + Washington** emerge già qualcosa di molto vicino a un vero curriculum organico.

E soprattutto emerge la domanda scientifica comune a tutti:

> **Come può un sistema costruire rappresentazioni sufficientemente generali del mondo da poter prevedere, pianificare, imparare e agire autonomamente in situazioni che non erano state programmate in anticipo?**

È probabilmente questo, più ancora del singolo algoritmo robotico, il problema centrale della Physical AI.