# Scoperta autonoma di astrazioni — mappa della letteratura

Note bibliografiche su library learning, skill discovery e compressione come criterio di valore. Raccolte tra luglio e agosto 2026 durante la valutazione di un progetto poi abbandonato: **il progetto è chiuso, questa ricognizione no**. I riferimenti al disegno sperimentale specifico sono stati rimossi; quello che resta è la mappa del campo, il gap trovato, e le letture che valgono la pena.

Il filo concettuale a monte è in [sintesi-compressione-astrazione.md](sintesi-compressione-astrazione.md); la versione filosofica della stessa domanda è in [bibliografia intensione/autonomia](../intensione-autonomia/bibliografia.md).

> ⚠️ **Data di validità: agosto 2026.** In un campo che pubblica venticinque sistemi `Skill*` in un anno, la sezione sulla saturazione invecchia in fretta.

---

## 1. I tre filoni

### A — Self-improvement e length generalization (neurale)

- **Lee, Cai, Schwarzschild, Lee, Papailiopoulos — *Self-Improving Transformers Overcome Easy-to-Hard and Length Generalization Challenges*** (arXiv:2502.01612, ICML 2025). Il baseline diretto: loop genera → filtra i corretti → ri-addestra; generalizza da addizione a 10 cifre a 100 cifre; miglioramenti esponenziali OOD filtrando gli esempi auto-generati. Il filtro di correttezza è il punto d'ingresso naturale di un verificatore simbolico.
- *Learning to Add, Multiply, and Execute Algorithmic Instructions Exactly with Neural Networks* (arXiv:2502.16763)
- Zhou et al. — *What Algorithms can Transformers Learn?* (arXiv:2310.16028), congettura RASP-L
- *Extrapolation by Association: Length Generalization Transfer* (arXiv:2506.09251) — transfer tra task
- *Recursive Latent Space Reasoning* per OOD (arXiv:2510.14095); bound sulla training length (arXiv:2510.27015)

> **Messaggio del filone**: i transformer imparano scorciatoie. Serve self-improvement con verifica, oppure bias strutturali.

### B — Library learning e induzione di astrazioni (simbolico)

- **DreamCoder** (Ellis et al., PLDI 2021) — wake-sleep + compressione per scoprire astrazioni riusabili. Fondazionale.
- **Stitch** (Bowers et al., POPL 2023) — library induction come ottimizzazione MDL greedy
- *Prospective Compression in Human Abstraction Learning* (arXiv:2605.09985, 2026) — library learning **online**, vicino a un agente che si evolve mentre agisce
- **LaSR** — *Symbolic Regression with a Learned Concept Library* (arXiv:2409.09359)
- *Combining Induction and Transduction for Abstract Reasoning* (arXiv:2411.02272, filone ARC)
- *LLM-guided compositional program synthesis* (arXiv:2503.15540)
- Ren et al. 2026 — library learning con e-graph su armonia jazz (pattern e-graph + deduzione)

### C — Compressione come valore, skill discovery

- **Skill Reuse as Compression in Agentic RL** (arXiv:2605.31509, 2026) — il match più diretto: skill discovery come compressione MDL in setting agentico. Related work ricca: codebook di skill, BPE-style merging (Kozma & Voderholzer 2024 — la versione più letterale dell'intuizione), PRISE
- **Kong et al. — *From Reasoning Traces to Reusable Modules*** (arXiv:2606.18089, ICML 2026) — skill discovery nel **post-training** di LLM di reasoning, con teoria dell'identificabilità (modello a variabili latenti). Tesi asimmetrica: l'SFT fornisce il *materiale* (tracce composte che contengono gli atomi), e l'**RL decompone** quelle tracce in moduli riusabili — **skill** (operazioni locali) e **routing mechanism** (come l'intermedio è selezionato/riusato/instradato) — poi li ricombina su composizioni OOD. Due punti che valgono: (a) la composabilità va imparata da esperienza *composta* — re-iniettare atomi isolati non ripara una skill mancante, serve re-iniettarla dentro composizioni; (b) protocollo di data-design: SFT copre tutti gli atomi *via tracce composte*, RL punta a composizioni *fuori* dal supporto SFT — i set disgiunti danno il miglior OOD. È la controparte RL/neurale del caso didattico DreamCoder qui sotto (addizione→moltiplicazione), con decomposizione guidata da reward invece che da compressione MDL, e il lato "teoria del meccanismo" della [frontiera del riuso algoritmico](../composizionalita_transformer/composizionalita_transformer_frontiera_riuso_algoritmico.md). [PDF](papers/Kong-etal-Reasoning-Traces-Reusable-Modules-ICML26.pdf)
- *Learning options via compression* (NeurIPS 2022, gruppo Levine)
- Garcia, da Silva, Thomas — *compression-inspired macro discovery* (arXiv:1711.09048, 2017)
- Molinaro et al. — *Reward function compression facilitates goal-dependent RL* (arXiv:2509.06810) — plausibilità cognitiva
- **Schmidhuber** — *Formal Theory of Creativity, Fun, and Intrinsic Motivation* (2010) — compression progress drive, il lignaggio teorico di tutto il filone

### Il gap, come si presentava a luglio 2026

Nessuno combinava **compressione online come reward intrinseca** con un **gate di verifica simbolica** che promuove l'astrazione candidata a primitiva riusabile solo se certificata corretta e generale. Skill-Reuse-as-Compression resta neurale/statistico; DreamCoder e Stitch sono simbolici ma offline. Il ponte **online + verificato** sembrava lo spazio libero.

**Poi la verifica bibliografica di agosto ha mostrato che non lo era.** Vedi §2 e la tabella qui sotto.

### La pila, componente per componente — chi l'ha già fatto

Ricognizione di agosto 2026. Utile come mappa di prior art per chiunque riprenda il filo: quasi ogni pezzo isolato ha già un lavoro dedicato.

| Componente | Già fatto in |
|---|---|
| **Scoperta di astrazioni ricorsive di ordine superiore** | **STEVIE** — Hocquette, Dumančić, Cropper, *Learning Logic Programs by Discovering Higher-Order Abstractions*, IJCAI 2024. Higher-order refactoring: comprimere un programma logico scoprendo map, filter e **fold**, come problema di ottimizzazione a vincoli. +27% di accuratezza predittiva su un sistema ILP, −47% sui tempi, e le astrazioni trasferiscono tra domini |
| **Proposta via anti-unificazione** | **Babble** — Cao, Kunkel, Nandi, Willsey, Tatlock, Polikarpova, POPL 2023: *learning better abstractions with e-graphs and anti-unification* |
| Macro-operatori nella pianificazione | Korf 1985; Knoblock 1994 (gerarchie con ordered monotonicity); Botea et al., **Macro-FF**, JAIR 2005; Chrpa 2008 |
| Astrazione in ASP | Saribatur & Eiter 2021 |
| Loop genera → filtra → chunk → riusa | *Action abstractions for amortized sampling* (arXiv:2410.15184): traiettorie generate, filtrate per alta reward, un tokenizer identifica i chunk frequenti e li aggiunge allo spazio d'azione, ripetuto fino a convergenza |
| Invenzione autonoma di option + astrazione simbolica | Nayyar & Srivastava, AAAI 2025 |
| Predicate invention per pianificazione bilevel | Silver et al. (arXiv:2203.09634) |
| La noia come trigger | **HHVG** — Yu, Chang, Kanai, *Boredom-Driven Curious Learning*, Front. Neurorobot. 2019: l'agente tratta l'alta predicibilità come stato intrinsecamente non gratificante |
| Crescita online della libreria + criterio di accettazione + certificati | *Self-Evolving Agents with Anytime-Valid Certificates* (arXiv:2607.00871, luglio 2026): accetta un'astrazione solo se ΔJ supera una soglia minima di utilità e se la libreria risultante è nuova o migliorativa |

> **Il caso didattico di DreamCoder.** Dal memo CBMM (MIT, n. 113, 2020), *Dreaming with ARC*: dato il solo modulo di addizione, DreamCoder impara a risolvere task di moltiplicazione tramite addizione ripetuta, poi in fase di compressione rifattorizza quei programmi esprimendoli in termini di un modulo di moltiplicazione di livello superiore, riusabile per il fattoriale. E nel paper originale (Ellis et al.) il sistema ripercorre autonomamente la scoperta dell'*origami programming*: prima reinventa `fold`, poi `unfold`, poi definisce le altre funzioni ricorsive in termini di questi. **Addizione → moltiplicazione per compressione è l'esempio introduttivo con cui si spiega DreamCoder, dal 2020.**

---

## 2. La saturazione dell'area skill-library

Voyager (2023) ha fondato il paradigma. Nel 2026 l'area è in consolidamento: esiste già una **SoK sulle agentic skills** con ricerca strutturata su sei database.

Sistemi censiti nella sola ricerca preliminare: SkillOps, SkillDAG, SkillFlow, SkillRL, SkillOS, SkillX, SkillFoundry, SkillWeaver, SkillLearnBench, SkillRet, SkillRouter, SkillMaster, SkillBrew, SkillLens, GoS, GraSP, ParametricSkills, MASA, SkVM, EvoSkill, EvoSkills, AutoSkill, Skill-Pro, Trace2Skill, CoEvoSkills, SkillForge.

### Le mosse principali sono occupate

| mossa | occupata da |
|---|---|
| **Verificatore come gate** | **ReGAL** (Stengel-Eskin et al., ICML 2024) — rifattorizza programmi primitivi in astrazioni verificate e immagazzinate |
| **LLM nomina + compressione comprime** | **LILO** (Grand et al., ICLR 2024) — wake-sleep, LLM nella sintesi, Stitch per comprimere, LLM di nuovo per documentare |
| **Internalizzazione nei pesi** | **ParametricSkills** (arXiv:2606.30015, giugno 2026) — converte skill testuali in parametri a test time |

### Il fatto empirico che invece vale

Dal survey *Recursive Self-Improvement in AI* (arXiv:2607.07663, luglio 2026):

> Il fatto empirico centrale del 2026 è che gli LLM sono cattivi a scrivere skill: su **SkillsBench**, le skill scritte da umani migliorano il pass rate di **16,2 punti**, mentre quelle scritte da LLM non danno **nessun guadagno misurabile**.

Il paradigma dominante non funziona, e c'è un benchmark che lo misura. La reazione della letteratura è ingegneristica — manutenzione, grafi tipizzati, riscrittura adattiva — e **nessuno spiega perché**.

> ⚠️ **Da verificare**: SkillsBench è citato di seconda mano, mai letto direttamente.

---

## 3. Due sistemi letti da vicino

### SkillBrew (arXiv:2605.29440, 28 maggio 2026)

*Multi-Objective Curation of Skill Banks for LLM Agents* — City University of Hong Kong et al.

Formula la curation come ottimizzazione multi-obiettivo vincolata su **utilità, diversità, copertura**, risolta con un loop bi-livello propose-then-verify. Tre paradigmi distinti: (A) accumulo senza rimozione, (B) editing su segnale per-skill, (C) ottimizzazione globale a livello di banca — il loro.

Quattro elementi che vale la pena conoscere:

1. **Il gate su holdout.** Partizionano in `D_support` (proposta) e `D_query` (verifica), perché la separazione impedisce alla banca di fare overfitting sulle traiettorie che hanno motivato le sue stesse modifiche. È la condizione di indipendenza dai dati di scoperta, implementata.
2. **L'utility analysis di Minton, reinventata.** Utilità per **replay controfattuale leave-one-out**: `Δ(τ,s) = r(τ,s) − r(τ,∅)`, rimuovendo la skill e rieseguendo per isolare il contributo marginale.
3. **Ritenzione selettiva.** La banca **si contrae** dal cold-start e si stabilizza in 9–10 round invece di crescere illimitatamente.
4. **Garanzia di non-degradazione** per round, con soglia di utilità front-adaptive e candidato *null* (non modificare nulla).

**Risultati**: ALFWorld 59,0% medio (Voyager 47,0%, Skill-Pro 49,3%, ReAct 31,2%) su Qwen2.5-7B congelato; su GPT-4o da 46,4 a 88,1.

### SkillLens (arXiv:2605.08386, 8 maggio 2026)

*Adaptive Multi-Granularity Skill Reuse for Cost-Efficient LLM Agents* — Emory + CausalDynamics.

Grafo di skill a **quattro livelli** — policy, strategy, procedure, primitive. Dichiara esplicitamente di adattare le gerarchie di astrazione temporale dal **framework delle option**, dai design **feudali** manager-worker, dalle **architetture robotiche a tre strati** e dalla pianificazione **HTN**. Obiettivo `J = M(correttezza) − C(costo)`.

Il verificatore instrada ogni unità visitata su quattro azioni: **ACCEPT / DECOMPOSE / REWRITE / SKIP**. Doppio registro: registro agente (cosa recuperare) + registro verificatore (come instradare), co-evoluti sullo stesso gap report.

**Risultati**: ALFWorld da 45,00% a 51,31%; MuLocbench Acc@1 +6,31 punti a livello funzione. Il rewrite selettivo costa 16,4M token contro 115,5M del rewrite-all.

---

## 4. Il gap che resta aperto — l'astrazione parametrica

Il caso di studio pubblicato in SkillLens è la cosa più interessante emersa da tutta la ricognizione, e vale indipendentemente dal progetto che l'ha trovata.

### L'esempio

Task ALFWorld: mettere una mela **raffreddata** sul tavolo. Skill recuperata: *«pulisci l'oggetto e poi posizionalo»*.

Il verificatore:
- **mantiene**: cerca nei contenitori, prendi la mela, naviga al tavolo, posiziona
- **riscrive una sola unità**: «pulisci la mela nel lavandino» → **«raffredda la mela nel frigo»**
- **scarta**: le azioni specifiche del lavandino

La loro gap analysis lo dice esplicitamente: il trasferimento riesce perché la struttura di alto livello combacia, e **il mismatch è isolato al passo di trasformazione di stato**, non all'intera skill.

### Cosa sta realmente succedendo

Hanno una **famiglia di procedure identiche tranne che per un componente**, e la soluzione adottata è **riscrivere quel componente a ogni query, con una chiamata LLM, ogni volta**.

La soluzione corretta sarebbe una skill **parametrica**:

```
porta_oggetto_trasformato(Oggetto, Trasformazione, Destinazione)
    Trasformazione ∈ {lavandino, frigo, microonde, fornello}
```

Scoperta una volta, applicata per sostituzione, senza costo di riscrittura e senza rischio di allucinazione a ogni uso.

> **Pagano un rewrite per query dove servirebbe un'astrazione una volta sola.** È il livello 1 contro il livello 2, con dentro un esempio pubblicato e numeri sui costi.

### Il corollario

La gerarchia a quattro strati di SkillLens è **data a mano**. Policy/strategy/procedure/primitive sono livelli fissati dal progettista, e **nessuno scopre che le procedure formano una famiglia parametrica**.

### La condizione che nessuno ha formulato

> Un'astrazione parametrica è legittima solo se l'ambiente varia lungo la dimensione parametrizzata.

Sopravvissuta intatta alla verifica bibliografica: nessuno l'aveva scritta, e ora ha un bersaglio concreto.

---

## 5. Simbolizzazione dentro gli LLM

Si può «simbolizzare» *dentro* un LLM? Due direzioni esplorate in letteratura.

**Simboli emergenti (mech interp)**: grokking sull'aritmetica modulare (Nanda et al. — il transformer inventa internamente un algoritmo via DFT); *Emergent Symbolic Mechanisms* (ICML 2025 — symbol abstraction heads → symbolic induction heads → retrieval heads); function/task vectors (Todd et al.). Ma sono quasi-simboli: direzioni continue, superposition, nessuna garanzia composizionale, non nominabili né verificabili.

**Simbolizzazione forzata**: (a) bottleneck discreti (VQ-VAE, Gumbel, codebook) — fragili per il reasoning; (b) token nuovi appresi: neologismi (Hewitt et al.), gist tokens (Mu et al.); (c) **simboli esterni**, la via su cui il campo è convergito — **Voyager** (skill library di funzioni riusabili, ambiente come verificatore), **LILO** (Stitch comprime, LLM nomina e documenta), **ReGAL** (refactoring in astrazioni).

**Conclusione**: la simbolizzazione interna genuina — discreta, verificabile, componibile — non è stata ottenuta. L'architettura «il neurale propone, il simbolo vive fuori, la verifica lo promuove» è dove sono atterrati tutti.

L'anello **scoperta → verifica → internalizzazione** (macro scoperta per compressione, verificata logicamente, poi distillata nel modello come token nuovo o via fine-tuning sul curriculum auto-generato) sembrava libero a luglio 2026. **Non lo era**: ParametricSkills lo occupa dal lato dell'internalizzazione. → §2.

Collegamento naturale con [interpretability](../interpretability/papers.md) sul lato dei simboli emergenti.

---

## 6. Le letture che valgono

Ordinate per priorità. I tempi sono stime di lettura mirata, non integrale.

### Prioritarie

**Perdomo, Zrnic, Mendler-Dünner, Hardt — *Performative Prediction*** (ICML 2020) · ~2 ore
Il vocabolario che protegge dall'obiezione di ingenuità quando un sistema produce i dati che poi lo confermano: **performatively stable** (punto fisso del retraining) contro **performatively optimal**, e il concetto di *distribution map*. Leggere le sezioni 2–3, saltare le dimostrazioni di convergenza.

**Machado, Barreto, Precup, Bowling — *Temporal Abstraction in RL with the Successor Representation*** (JMLR 2023) · ~1,5 ore
Sezioni **1, 3 e 7**. È dove il ciclo ROD (Representation-driven Option Discovery) è formalizzato e dichiarato **virtuoso** — cioè la posizione contro cui vale la pena argomentare. Il resto (successor representation nel dettaglio) non serve.

**Nikishin, Schwarzer, D'Oro, Bacon, Courville — *The Primacy Bias in Deep RL*** (ICML 2022) · ~1 ora
Corto e leggibile. Commitment prematuro nei pesi, con la cura — reset periodici — che nel caso simbolico non si applica. È il precedente più vicino su «l'impegno precoce restringe lo spazio successivo».

### Tecniche

**Bowers, Olausson, Wong, Grand, Tenenbaum, Ellis, Solar-Lezama — *Top-down synthesis for library learning*** (Stitch, POPL 2023) · ~1,5 ore
La versione pulita e minimale dell'ottimizzazione MDL su libreria. **Se si legge una sola cosa tra Stitch e DreamCoder, questa.**

**Ellis, Wong, Nye, Sablé-Meyer et al. — *DreamCoder*** (PLDI 2021) · ~2 ore
Solo le sezioni su compressione e crescita della libreria: come si calibra `L(H)` e come si gestisce l'espansione del vocabolario. Saltare il recognition model.

**Lieder & Griffiths — *Resource-rational analysis*** (Behavioral and Brain Sciences, 2020) · ~1,5 ore
Sezioni 1–3. La giustificazione teorica di un pianificatore a budget: la ricerca limitata non è un'assunzione comoda, è il modello standard di razionalità limitata.

**Plotkin — *A note on inductive generalization*** (Machine Intelligence 5, 1970) · ~1 ora
Dodici pagine, l'anti-unificazione del primo ordine. Serve anche per sapere **perché non basta**: generalizza sui sottotermini, non sulla profondità della struttura.

### Da consultare, non da leggere

| Fonte | Quando serve |
|---|---|
| **Grünwald**, *The Minimum Description Length Principle* (MIT 2007) | Capitoli 1–2 e 5, per difendere una scelta di codifica di `L(H)` |
| **Dohare, Hernandez-Garcia, Rahman, Mahmood, Sutton**, *Loss of Plasticity in Deep Continual Learning* (Nature 2024) | Abstract + sezione sul rango effettivo. Soluzioni a rango basso che restringono lo spazio successivo |
| **Minton**, sull'utility problem dell'EBL (1988) | Il fenomeno storico delle macro apprese che rallentano il sistema |
| **Sutton, Precup, Singh**, *Between MDPs and semi-MDPs* (AIJ 1999) | Il framework delle option |
| **Cao, Kunkel, Nandi, Willsey, Tatlock, Polikarpova**, *Babble* (POPL 2023) | Come si fa l'anti-unificazione con gli e-graph |
| **Korf** (1985) · **Botea et al.**, *Macro-FF* (JAIR 2005) | I macro-operatori nella pianificazione classica, per il collegamento storico |
| arXiv:2607.00871 — *Self-Evolving Agents with Anytime-Valid Certificates* (luglio 2026) | Nota che il passo MDL di Stitch è one-shot e che DreamCoder non ha teoremi di convergenza. ⚠️ Visto solo via ricerca, mai letto |

### Da cercare

**Performative reinforcement learning** — verificare se esiste una versione RL della performatività. Se esiste, è citazione obbligata per chiunque riprenda il filo.
