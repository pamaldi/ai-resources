# NEmo 2026 — Verifica di originalità e riposizionamento

**Note di lavoro — 3 agosto 2026**
Esito della ricerca bibliografica sull'idea originale, opzioni alternative, e verdetto finale.
Deadline submission: **10 settembre 2026** → cinque settimane e mezzo.

---

## 1. Verdetto sull'idea originale

### 1.1 Il colpo peggiore: il toy aritmetico è l'esempio da manuale di DreamCoder

Non "qualcosa di simile". È **l'esempio didattico** con cui si spiega DreamCoder.

Dal memo CBMM (MIT, n.113, 2020), *Dreaming with ARC*:

> Dato il solo modulo di addizione, DreamCoder impara a risolvere task di moltiplicazione tramite addizione ripetuta. Poi, durante la fase di "compressione", rifattorizza quei programmi esprimendoli in termini di un modulo di moltiplicazione di livello superiore. Il nuovo modulo può essere usato per task più difficili come il calcolo del fattoriale.

Addizione → moltiplicazione per compressione, con promozione in libreria e riuso al livello sopra. Il progetto, usato come illustrazione introduttiva sei anni fa.

### 1.2 E il livello 2 è stato fatto autonomamente

Dal paper DreamCoder (Ellis et al.):

> Il linguaggio iniziale include la ricorsione primitiva (combinatore Y) ma nessun'altra funzione ricorsiva. […] DreamCoder ha ripercorso la scoperta dell'*origami programming*: prima reinventando fold, poi unfold, poi definendo tutte le altre funzioni ricorsive in termini di folding e unfolding.

Il salto identificato come tecnicamente più duro — dalla famiglia `double/triple/quintuple` al `fold` — è stato compiuto autonomamente cinque anni fa.

### 1.3 Il livello 2 ha anche un lavoro dedicato

**STEVIE** — Hocquette, Dumančić, Cropper, *Learning Logic Programs by Discovering Higher-Order Abstractions*, IJCAI 2024:

- introduce il problema dell'**higher-order refactoring**: comprimere un programma logico scoprendo astrazioni di ordine superiore come map, filter e **fold**
- formulato come problema di ottimizzazione a vincoli
- migliora l'accuratezza predittiva di un sistema ILP del 27%, riduce i tempi del 47%
- le astrazioni trasferiscono tra domini

È il passo mancante, dentro ILP, con Cropper — la persona già in lista per Popper.

### 1.4 Il meccanismo di proposta

**Babble** — Cao, Kunkel, Nandi, Willsey, Tatlock, Polikarpova, POPL 2023: *learning better abstractions with e-graphs and anti-unification*. Esattamente l'architettura di proposta progettata.

### 1.5 Il resto della pila

| Componente | Già fatto in |
|---|---|
| Macro-operatori nella pianificazione | Korf 1985; Knoblock 1994 (gerarchie con ordered monotonicity); Botea et al., **Macro-FF**, JAIR 2005; Chrpa 2008 |
| Astrazione in ASP | Saribatur & Eiter 2021 |
| Loop genera → filtra → chunk → riusa | *Action abstractions for amortized sampling* (2410.15184): traiettorie generate, filtrate per alta reward, un tokenizer identifica i chunk frequenti e li aggiunge allo spazio d'azione, ripetuto fino a convergenza |
| Invenzione autonoma di option + astrazione simbolica | Nayyar & Srivastava, AAAI 2025 |
| Predicate invention per pianificazione bilevel | Silver et al. (2203.09634) |
| La noia come trigger | **HHVG** — Yu, Chang, Kanai, *Boredom-Driven Curious Learning*, Front. Neurorobot. 2019: l'agente tratta l'alta predicibilità come stato intrinsecamente non gratificante |
| Crescita online della libreria + criterio di accettazione + certificati | *Self-Evolving Agents with Anytime-Valid Certificates* (2607.00871, **luglio 2026**): nota che il loop endogeno di DreamCoder non ha teoremi di convergenza e che il passo MDL di Stitch è one-shot; accetta un'astrazione solo se ΔJ supera una soglia minima di utilità e se la libreria risultante è nuova o migliorativa |

### 1.6 Conclusione

**Il progetto "compressione gated dalla verifica scopre la moltiplicazione" non è difendibile in questa forma.** Un revisore che conosce DreamCoder risponde in tre righe; e il memo CBMM è trovabile con una ricerca su Google.

---

## 2. La strada LLM: più affollata, non meno

### 2.1 Saturazione

Voyager (2023) ha fondato il paradigma skill library. Nel 2026 l'area è in consolidamento — esiste già una **SoK sulle agentic skills** con ricerca strutturata su sei database.

Sistemi censiti nella sola ricerca preliminare: SkillOps, SkillDAG, SkillFlow, SkillRL, SkillOS, SkillX, SkillFoundry, SkillWeaver, SkillLearnBench, SkillRet, SkillRouter, SkillMaster, SkillBrew, SkillLens, GoS, GraSP, ParametricSkills, MASA, SkVM, EvoSkill, EvoSkills, AutoSkill, Skill-Pro, Trace2Skill, CoEvoSkills, SkillForge.

### 2.2 Le mosse principali sono occupate

- **Verificatore come gate** → **ReGAL** (Stengel-Eskin et al., ICML 2024): rifattorizza programmi primitivi in astrazioni che vengono verificate e immagazzinate
- **LLM nomina + compressione comprime** → **LILO** (Grand et al., ICLR 2024): wake-sleep, LLM nella sintesi, Stitch per comprimere, LLM di nuovo per documentare
- **Internalizzazione nei pesi** → **ParametricSkills** (2606.30015, giugno 2026): converte skill testuali in parametri a test time, accoppiando l'evoluzione delle skill all'apprendimento del modello

> ⚠️ **Aggiornare la sezione 6 del documento di contesto**: la nota "verificare che l'anello scoperta → verifica → internalizzazione sia libero" ha ricevuto risposta. **Non è libero.**

### 2.3 Il fatto empirico che invece vale

Dal survey *Recursive Self-Improvement in AI* (2607.07663, luglio 2026):

> Il fatto empirico centrale del 2026 è che gli LLM sono cattivi a scrivere skill: su **SkillsBench**, le skill scritte da umani migliorano il pass rate di **16,2 punti**, mentre quelle scritte da LLM non danno **nessun guadagno misurabile**.

Il paradigma dominante non funziona, e c'è un benchmark che lo misura. La reazione della letteratura è ingegneristica (manutenzione, grafi tipizzati, riscrittura adattiva) — nessuno spiega *perché*.

**⚠️ Da verificare direttamente**: SkillsBench è citato di seconda mano.

---

## 3. I due paper letti — SkillBrew e SkillLens

### 3.1 SkillBrew (arXiv 2605.29440, 28 maggio 2026)

*Multi-Objective Curation of Skill Banks for LLM Agents* — City University of Hong Kong et al.

**Cosa fa**: formula la curation come ottimizzazione multi-obiettivo vincolata su **utilità, diversità, copertura**, risolta con un loop bi-livello propose-then-verify. Tre paradigmi distinti in figura 1: (A) accumulo senza rimozione, (B) editing su segnale per-skill, (C) ottimizzazione globale a livello di banca (il loro).

**Cosa occupa del progetto originale**:

1. **Il gate su holdout.** Partizionano in `D_support` (proposta) e `D_query` (verifica), dichiarando che la separazione impedisce alla banca di fare overfitting sulle traiettorie che hanno motivato le sue stesse modifiche. È la condizione di indipendenza dai dati di scoperta, implementata.
2. **L'utility analysis di Minton, reinventata.** Utilità per **replay controfattuale leave-one-out**: `Δ(τ,s) = r(τ,s) − r(τ,∅)`, rimuovendo la skill e rieseguendo per isolare il contributo marginale.
3. **Ritenzione selettiva.** La banca **si contrae** dal cold-start e si stabilizza in 9-10 round invece di crescere illimitatamente.
4. **Garanzia di non-degradazione** per round, con soglia di utilità front-adaptive e candidato *null* (non modificare nulla).

**Risultati**: ALFWorld 59.0% avg (vs Voyager 47.0%, Skill-Pro 49.3%, ReAct 31.2%) su Qwen2.5-7B frozen; su GPT-4o da 46.4 a 88.1.

### 3.2 SkillLens (arXiv 2605.08386, 8 maggio 2026)

*Adaptive Multi-Granularity Skill Reuse for Cost-Efficient LLM Agents* — Emory + CausalDynamics.

**Cosa fa**: grafo di skill a **quattro livelli** — policy, strategy, procedure, primitive. Dichiara esplicitamente di adattare le gerarchie di astrazione temporale dal **framework delle option**, dai design **feudali** manager-worker, dalle **architetture robotiche a tre strati** e dalla pianificazione **HTN**. Obiettivo `J = M(correttezza) − C(costo)`.

Il verificatore instrada ogni unità visitata su quattro azioni: **ACCEPT / DECOMPOSE / REWRITE / SKIP**. Doppio registro: registro agente (cosa recuperare) + registro verificatore (come instradare), co-evoluti sullo stesso gap report.

**Risultati**: ALFWorld da 45.00% a 51.31%; MuLocbench Acc@1 +6.31 punti a livello funzione. Il rewrite selettivo costa 16.4M token contro 115.5M del rewrite-all.

---

## 4. Impatto sulle proposte precedenti

### 4.1 Indebolita: "il problema dell'utilità è tornato"

Non falsa — né SkillBrew né SkillLens citano Minton o l'EBL. Ma il valore cala molto: se la comunità ha già reinventato **le soluzioni** (analisi controfattuale dell'utilità, ritenzione selettiva, obiettivo correttezza-meno-costo), dirgli come si chiamava nel 1988 è erudizione, non contributo.

E SkillLens *cita* la letteratura classica di pianificazione (HTN, option, architetture a tre strati) — quindi non è nemmeno vero che i due mondi si ignorino del tutto.

### 4.2 Occupata: l'ablazione gate / no-gate

SkillBrew ha sia il vincolo di utilità sia la separazione support/query. Le condizioni C2/C3 non sono più un contributo autonomo.

### 4.3 Sopravvive e si rafforza: la C5

*Un'astrazione parametrica è legittima solo se l'ambiente varia lungo la dimensione parametrizzata.* Nessuno l'ha formulata, e ora ha un bersaglio concreto.

---

## 5. Il gap vero, regalato dal caso studio di SkillLens

### 5.1 L'esempio

Task ALFWorld: mettere una mela **raffreddata** sul tavolo. Skill recuperata: **"pulisci l'oggetto e poi posizionalo"**.

Il verificatore:

- **mantiene**: cerca nei contenitori, prendi la mela, naviga al tavolo, posiziona
- **riscrive una sola unità**: "pulisci la mela nel lavandino" → **"raffredda la mela nel frigo"**
- **scarta**: le azioni specifiche del lavandino

La loro gap analysis lo dice esplicitamente: il trasferimento riesce perché la struttura di alto livello combacia, e **il mismatch è isolato al passo di trasformazione di stato**, non all'intera skill.

### 5.2 Cosa sta realmente succedendo

Hanno una **famiglia di procedure identiche tranne che per un componente**, e la soluzione adottata è **riscrivere quel componente a ogni query, con una chiamata LLM, ogni volta**.

La soluzione corretta sarebbe:

```
porta_oggetto_trasformato(Oggetto, Trasformazione, Destinazione)
    Trasformazione ∈ {lavandino, frigo, microonde, fornello}
```

Una skill **parametrica**: scoperta una volta, applicata per sostituzione, senza costo di riscrittura e senza rischio di allucinazione a ogni uso.

> **Pagano un rewrite per query dove servirebbe un'astrazione una volta sola.**

È il livello 1 contro il livello 2, con dentro un esempio pubblicato e numeri sui costi.

### 5.3 Il secondo gap, minore ma reale

La gerarchia a quattro strati di SkillLens è **data a mano**. Policy/strategy/procedure/primitive sono livelli fissati dal progettista. **Nessuno scopre che le procedure formano una famiglia parametrica.**

---

## 6. Il paper proposto

> **Le skill library rifattorizzano dove dovrebbero astrarre.**
>
> I sistemi attuali gestiscono la variazione tra skill simili riscrivendo localmente a ogni query. Funziona, ma paga un costo lineare nel numero di usi ed è soggetto a errore ogni volta. La mossa corretta è promuovere la dimensione variabile a **parametro** — operazione una tantum, verificabile, a costo zero al riuso.
>
> Mostriamo (a) quanta parte del costo di rewrite nei sistemi esistenti è attribuibile a variazione parametrizzabile, e (b) sotto quali condizioni la parametrizzazione è giustificata dai dati e quando invece il rewrite locale è la scelta corretta.

### 6.1 Perché la parte (b) è forte

È la C5, che ora ha un bersaglio: **la variazione dev'essere osservata su più valori perché il parametro sia legittimo.** Se il sistema ha visto solo il frigo, `Trasformazione` non è un parametro giustificato — e il rewrite locale è la scelta corretta. L'ambiente è co-autore dell'astrazione.

### 6.2 Come si misura, a basso costo

1. prendere i log di rewrite di un sistema esistente
2. classificare quanti rewrite differiscono **solo per un valore in una posizione strutturalmente fissa**
3. stimare il risparmio (token, latenza, tasso di errore) di una skill parametrica equivalente
4. incrociare con quante volte quel valore è stato osservato variare → frontiera della giustificazione

**Nessun sistema da battere, solo un'analisi.**

### 6.3 Aggancio al workshop

Tema (a) *long-horizon planning*: modelli d'azione simbolici e loro revisione.
Motivo conduttore *affidabilità*: il rewrite per query è una fonte ricorrente di allucinazione; l'astrazione parametrica verificata la elimina per costruzione.

---

## 7. Il rischio principale

**La velocità del campo.** SkillBrew e SkillLens sono di maggio 2026, trovati oggi. Nell'area escono più paper alla settimana. Con il 10 settembre come deadline, si scrive sapendo che qualcuno potrebbe pubblicare la stessa idea nel frattempo.

Corollario operativo:

> **Il valore aggiunto non è trovare l'angolo perfetto, è misurare qualcosa.**
> L'angolo "rewrite vs astrazione" è buono oggi; fra tre settimane non è garantito. La misura sui log invece resta.

---

## 8. Da verificare prima di muoversi

- [ ] Il memo CBMM n.113 sulla moltiplicazione in DreamCoder (fonte primaria)
- [ ] La sezione origami/fold del paper DreamCoder
- [ ] SkillsBench: i 16,2 punti umani vs zero LLM (citato di seconda mano)
- [ ] Scholar: `"utility problem" Minton skill library LLM` — se il collegamento storico è già stato fatto
- [ ] Disponibilità pubblica dei log di rewrite di SkillLens o sistemi analoghi (senza quelli, la misura non si fa)
