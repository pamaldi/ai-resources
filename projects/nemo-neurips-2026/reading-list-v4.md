# Reading list — specifica sperimentale v4

**Progetto NEmo 2026 — 3 agosto 2026**
Letture per *Performatively stable abstractions*. Ordinate per **quando servono**, non per importanza teorica: con cinque settimane e ~850 righe da scrivere, la lettura va razionata.

**Totale: ~11 ore**, cinque prima di iniziare e sei in parallelo all'implementazione. Circa il 5% del tempo di progetto, che è la proporzione giusta per un paper sperimentale.

---

## Livello 1 — Prima di scrivere codice (~5 ore)

Tre letture. Senza queste si rischia di riscoprire cose già fatte o di formulare male il claim.

### Perdomo, Zrnic, Mendler-Dünner, Hardt — *Performative Prediction* (ICML 2020)

Il framing dell'intero paper. Da qui viene il vocabolario che protegge dall'obiezione di ingenuità: **performatively stable** (punto fisso del retraining) contro **performatively optimal**, e il concetto di *distribution map*.

Il `ΔJ_remove` positivo della specifica è letteralmente una verifica di stabilità performativa.

Leggere sezioni 2-3 con attenzione, saltare le dimostrazioni di convergenza.

→ *Serve per*: §1, §7.4, §12 · **2 ore**

### Machado, Barreto, Precup, Bowling — *Temporal Abstraction in RL with the Successor Representation* (JMLR 2023)

Sezioni **1, 3 e 7** soltanto. È dove il ciclo ROD (Representation-driven Option Discovery) è formalizzato e dichiarato **virtuoso**.

**È il bersaglio del paper**: va citato con precisione e bisogna sapere cosa sostiene davvero, per non attribuirgli una tesi che non ha.

Il resto (successor representation nel dettaglio) non serve.

→ *Serve per*: §12, e per formulare il claim senza esagerare · **1,5 ore**

### Nikishin, Schwarzer, D'Oro, Bacon, Courville — *The Primacy Bias in Deep RL* (ICML 2022)

Corto e leggibile. Commitment prematuro nei pesi, con la cura (reset periodici) che nel caso simbolico non si applica.

È il precedente più vicino e va citato bene, perché è la prima cosa che un revisore RL tirerà fuori.

→ *Serve per*: §12 e per la frase sulle cure non trasferibili · **1 ora**

---

## Livello 2 — Mentre implementi (~6 ore, in parallelo)

### Bowers, Olausson, Wong, Grand, Tenenbaum, Ellis, Solar-Lezama — *Top-down synthesis for library learning* (Stitch, POPL 2023)

La versione pulita e minimale dell'ottimizzazione MDL su libreria. Più vicina al codice da scrivere di quanto lo sia DreamCoder.

**Se si sceglie una sola lettura tra Stitch e DreamCoder, questa.**

→ *Serve per*: §5.2, §5.3 · **1,5 ore**

### Ellis, Wong, Nye, Sablé-Meyer et al. — *DreamCoder* (PLDI 2021)

Solo le sezioni sulla compressione e sulla crescita della libreria. Serve per calibrare `L(H)` e per capire come gestiscono l'espansione del vocabolario.

**Saltare il recognition model**: non è nello scope.

→ *Serve per*: §5.2 · **2 ore**

### Lieder & Griffiths — *Resource-rational analysis* (Behavioral and Brain Sciences, 2020)

Sezioni 1-3. È la giustificazione teorica del planner a budget.

Serve per difendere §6.2: la ricerca limitata non è un'assunzione comoda inventata per far funzionare l'esperimento, è il modello standard di razionalità limitata.

→ *Serve per*: §6.2, §12 · **1,5 ore**

### Plotkin — *A note on inductive generalization* (Machine Intelligence 5, 1970)

Dodici pagine. L'anti-unificazione del primo ordine.

Serve per implementare §5.3.1 correttamente **e** per sapere esattamente perché non produce lo schema: generalizza sui sottotermini, non sulla profondità della struttura.

→ *Serve per*: §5.3 · **1 ora**

---

## Livello 3 — Da consultare, non da leggere

Riferimenti da tenere aperti quando serve difendere una scelta, non da leggere linearmente.

| Fonte | Quando serve |
|---|---|
| **Grünwald**, *The Minimum Description Length Principle* (MIT 2007) | Capitoli 1-2 e 5, quando bisogna difendere una scelta di codifica di `L(H)` |
| **Dohare, Hernandez-Garcia, Rahman, Mahmood, Sutton**, *Loss of Plasticity in Deep Continual Learning* (Nature 2024) | Abstract + sezione sul rango effettivo. Meccanismo analogo: soluzioni a rango basso che restringono lo spazio successivo. Una riga di related work |
| **Minton**, sull'utility problem dell'EBL (1988) | Il fenomeno storico delle macro apprese che rallentano il sistema. Serve una riga, non il paper |
| **Sutton, Precup, Singh**, *Between MDPs and semi-MDPs* (AIJ 1999) | Il framework delle option. Da citare, non da rileggere se già noto |
| **Cao, Kunkel, Nandi, Willsey, Tatlock, Polikarpova**, *Babble* (POPL 2023) | Consultazione tecnica: come si fa l'anti-unificazione con gli e-graph, se l'implementazione diretta si arena |

---

## Livello 4 — Solo se il pilot funziona

Da leggere **dopo** aver verificato che il fenomeno esiste, per la sezione di posizionamento finale.

- **arXiv 2607.00871** — *Self-Evolving Agents with Anytime-Valid Certificates* (luglio 2026). Il lavoro più vicino cronologicamente: nota che il passo MDL di Stitch è one-shot e che DreamCoder non ha teoremi di convergenza. Bisogna sapere esattamente cosa fa per distinguersene.
  > ⚠️ **Da verificare**: finora visto solo tramite ricerca, non letto direttamente.

- **Performative reinforcement learning** — cercare se esiste una versione RL della performatività prima di scrivere il related work. Se esiste, è citazione obbligata.

- **Korf** (1985) e **Botea et al.**, *Macro-FF* (JAIR 2005) — i macro-operatori nella pianificazione classica, se un revisore chiede il collegamento storico.

---

## Cosa NON leggere

**Tutto il materiale accumulato nei mesi scorsi**: Thom e la teoria delle catastrofi, computational mechanics e gli automi cellulari, HashLife, il chunking striatale, la vespa Sphex, MacKay, Elias-Fano.

È stato utile per arrivare fin qui, ma **non entra in quattro pagine**, e ogni ora spesa lì è un'ora tolta al codice.

**Anche la letteratura skill-library LLM** (SkillBrew, SkillLens, e i venticinque sistemi `Skill*`) è fuori scope. Al massimo una riga per osservare che il fenomeno riguarda anche loro.

---

## Piano di lettura

| Quando | Cosa | Ore |
|---|---|---|
| **Questa settimana, prima del gate offline** | Livello 1 — Perdomo, Machado, Nikishin | 5 |
| **Mentre il codice gira** | Livello 2 — Stitch, DreamCoder, Lieder & Griffiths, Plotkin | 6 |
| **Al bisogno** | Livello 3 | — |
| **Dopo il gate del pilot** | Livello 4 | 2-3 |

Le tre del livello 1 vanno fatte **prima** del gate offline: servono a sapere cosa si sta misurando e come chiamarlo. Le altre possono aspettare che il sistema giri.
