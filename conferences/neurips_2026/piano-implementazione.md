# Piano di implementazione

**Progetto**: astrazioni performativamente stabili nel library learning online
**Riferimento**: `specifica-sperimentale.md`
**Finestra**: 4 agosto – 9 settembre 2026 (submission il 9, non il 10)

---

## 0. Principi che governano il piano

**1. Ogni milestone ha un criterio di uscita verificabile.** Non "ho scritto il modulo" ma "il test passa e produce il numero atteso". Se il criterio non è soddisfatto non si procede, si torna indietro.

**2. Due gate di arresto.** Il primo verifica che il sistema funzioni; il secondo che il fenomeno esista. Ciascuno può chiudere il progetto, ed è il loro scopo.

**3. Nessuna ottimizzazione prima dei risultati.** Python puro, strutture dati ovvie, nessuna parallelizzazione. La scala non lo richiede e ottimizzare un esperimento che potrebbe non servire è il modo più efficiente di perdere una settimana.

**4. Il logging precede l'analisi.** Si logga tutto dall'inizio, in formato append-only. Rieseguire costa più che scrivere righe in più.

**5. La componente ML si costruisce solo dopo il secondo gate.** Se il fenomeno non emerge con il proponente enumerativo, un proponente appreso non lo crea: lo rende soltanto indistinguibile da un difetto di addestramento.

---

## 1. Struttura del repository

```
performative-abstractions/
├── README.md                    flusso di esecuzione, in ordine
├── pyproject.toml               dipendenze (uv)
├── PREDICTION.md                la soglia k* calcolata a mano, DATATA
├── src/
│   └── perfabs/
│       ├── __init__.py
│       ├── config.py            tutti i parametri, nessun hardcode altrove
│       ├── domain.py            ordini, partizioni, costo fisico, espansione
│       ├── stream.py            generatore di ordini, hash di verifica
│       ├── dsl.py               Macro, Plan, encoding_len, L_H
│       ├── mdl.py               delta_J, delta_J_remove, reparse
│       ├── propose.py           candidati chunk/strutturale/oracle, verify
│       ├── proposer_enum.py     ricerca a budget
│       ├── proposer_learn.py    modello autoregressivo (fase 6)
│       ├── loop.py              loop online, logging
│       └── analysis.py          caricamento log, metriche, figure
├── tests/
│   ├── test_domain.py
│   ├── test_stream.py
│   ├── test_dsl.py
│   ├── test_mdl.py
│   └── test_proposer.py
├── experiments/
│   ├── gate_offline.py
│   ├── gate_pilot.py
│   ├── grid_enum.py
│   └── grid_learn.py
├── logs/                        gitignored, JSONL
├── figures/
└── notes/                       decisioni, anomalie, risultati intermedi
```

**Versionato**: codice, test, `PREDICTION.md`, `notes/`, figure finali.
**Gitignored**: `logs/`, artefatti dei modelli.

---

## 2. Le milestone

| # | Milestone | Date | Criterio di uscita |
|---|---|---|---|
| **M0** | Setup e predizione | 4 ago | `PREDICTION.md` committato con `k*` calcolato |
| **M1** | Dominio e costo fisico | 4–5 ago | test: ottimo = `⌈N/C⌉` per ogni `N` |
| **M2** | Stream deterministico | 5 ago | test: hash stabile, flussi identici tra condizioni |
| **M3** | DSL e MDL | 6 ago | test: `L(H)` e `encoding_len` coerenti, `reparse` corretto |
| **M4** | Proposta e promozione offline | 6–7 ago | **GATE OFFLINE** |
| **M5** | Proponente enumerativo | 8–9 ago | il budget morde: piani diversi con `B` diversi |
| **M6** | Loop online, `B = ∞` | 9–10 ago | riproduce il comportamento offline |
| **M7** | Budget finito, pilot | 11–14 ago | **GATE DEL PILOT** |
| **M8** | Griglia ENUM completa | 15–19 ago | diagramma di fase, diagnosi |
| **M9** | Proponente appreso | 20–23 ago | il fenomeno compare anche in LEARN? |
| **M10** | Analisi e figure | 24–27 ago | tutte le figure da log esistenti |
| **M11** | Stesura | 28 ago – 5 set | draft completo, 4 pagine |
| **M12** | Revisione e submission | 6–9 set | inviato il 9 |

---

# Fase 1 — Fondamenta (4–7 agosto)

## M0 — La predizione, prima del codice

**Mezza giornata, nessun codice.**

Fissare i valori di `L_H` e calcolare a mano il punto di pareggio tra famiglia di chunk e schema:

```
costo famiglia di k chunk    ≈  k · c_macro
costo schema                 ≈  c_fold
k* ≈ c_fold / c_macro
```

Scrivere in `PREDICTION.md`:
- i valori scelti per `N_PRIMITIVES`, `C`, `fold_overhead`
- la derivazione
- **il valore numerico di `k*`**
- la data

**Criterio di uscita**: `k*` cade tra 3 e 5.

> Se `k* = 2`, lo schema conviene subito e il fenomeno non emergerà mai. Se `k* = 15`, non emergerà nemmeno in condizione favorevole — con `C = 6` non si arriva a quindici dimensioni di lotto distinte. Aggiustare `fold_overhead` **ora**, e dichiararlo nel paper come parametro del dominio con analisi di sensibilità.

Questo è il calcolo con il miglior rapporto tra informazione e costo dell'intero progetto.

## M1 — Dominio e costo fisico

**Contenuto**: `domain.py`

```python
Order = tuple[str, int]                    # (oggetto, N)
Batch = int                                # 1 ≤ q ≤ C
Partition = list[Batch]

def all_partitions(N: int, C: int) -> Iterator[Partition]
def physical_cost(partition, w_move=10) -> int
def expand_to_primitives(partition, obj) -> list[Action]
def optimal_trips(N, C) -> int             # ⌈N/C⌉
```

**Test obbligatori** (`test_domain.py`):

```python
def test_optimum_is_ceiling():
    for N in range(2, 31):
        for C in (4, 6, 8):
            best = min(all_partitions(N, C), key=physical_cost)
            assert len(best) == ceil(N / C)

def test_expansion_length():
    # 2 spostamenti + 2q azioni per lotto
    for p in all_partitions(11, 6):
        assert len(expand_to_primitives(p, "x")) == sum(2 + 2*q for q in p)

def test_cost_monotone_in_trips():
    # a parità di N, più lotti = più costo
    ...
```

**Criterio di uscita**: i tre test passano per `N ∈ [2,30]`, `C ∈ {4,6,8}`.

> Se il costo fisico è definito male, ogni misura a valle è priva di significato. È il test che si è più tentati di saltare e quello che protegge di più.

**Output collaterale utile**: la tabella del regret del chunk da 4 (§2.5 della specifica), generata dal codice invece che a mano.

## M2 — Stream deterministico

**Contenuto**: `stream.py`

```python
def make_stream(schedule, k_poor, seed, seq_len, N_range, objects) -> list[Order]
def stream_hash(stream) -> str
```

**Test** (`test_stream.py`):

```python
def test_determinism():
    a = make_stream("poor_then_rich", 100, seed=0, ...)
    b = make_stream("poor_then_rich", 100, seed=0, ...)
    assert a == b

def test_schedules_differ():
    assert make_stream("rich", ...) != make_stream("poor_then_rich", ...)

def test_poor_phase():
    s = make_stream("poor_then_rich", k_poor=100, ...)
    assert all(N == 4 for _, N in s[:100])
    assert len({N for _, N in s[100:]}) > 5
```

**Criterio di uscita**: hash riproducibile tra sessioni diverse.

Generare subito `experiments/expected_hashes.json` con gli hash di tutte le combinazioni `(schedule, k_poor, seed)` della griglia. Ogni run li verifica prima di partire.

## M3 — DSL e costo MDL

**Contenuto**: `dsl.py`, `mdl.py`

```python
@dataclass(frozen=True)
class Macro:
    name: str
    q: int | None

def encoding_len(plan, lib, C) -> float
def L_H(lib, C, fold_overhead) -> float
def J(lib, buffer, C) -> float
def delta_J(candidate, lib, buffer, C) -> float
def reparse(trace, lib, C) -> Plan
def delta_J_remove(macro_name, lib, buffer, C) -> float
```

**Test** (`test_mdl.py`):

```python
def test_chunk_cheaper_to_invoke():
    # l'asimmetria di §11.3 deve emergere, non essere imposta
    lib_chunk = Library([Macro("lotto_4", 4)])
    lib_schema = Library([Macro("trasporta_lotto", None)])
    p_chunk = [MacroCall("lotto_4", "x", 4)]
    p_schema = [MacroCall("trasporta_lotto", "x", 4)]
    assert encoding_len(p_chunk, lib_chunk, C) < encoding_len(p_schema, lib_schema, C)

def test_reparse_preserves_semantics():
    # ricodificare non cambia la traccia primitiva
    for trace in sample_traces:
        p = reparse(trace, reduced_lib, C)
        assert expand_to_primitives(p) == trace

def test_schema_wins_above_threshold():
    # con k > k* lo schema deve avere ΔJ < 0
    buf = synthetic_buffer(distinct_counts=k_star + 2)
    assert delta_J(Macro("trasporta_lotto", None), lib_family, buf, C) < 0

def test_schema_loses_below_threshold():
    buf = synthetic_buffer(distinct_counts=k_star - 2)
    assert delta_J(Macro("trasporta_lotto", None), lib_family, buf, C) > 0
```

**Criterio di uscita**: gli ultimi due test passano **con il `k*` scritto in `PREDICTION.md`**.

> Se non passano, o la predizione era sbagliata o `L_H` non è quello che si credeva. In entrambi i casi si corregge qui, non dopo.

## M4 — Proposta, promozione, GATE OFFLINE

**Contenuto**: `propose.py`, `experiments/gate_offline.py`

```python
def propose(buffer, lib, C, oracle=False) -> list[Macro]
def verify(macro, lib, C, holdout) -> bool
def promote_offline(corpus, C, ...) -> Library
```

**Il gate**: si costruisce a mano un corpus ricco — partizioni ottime per `N ∈ [2,12]`, tutti gli oggetti, nessuna retroazione — e si esegue la promozione fino a convergenza.

**Criterio di uscita**:

```
la libreria finale contiene una Macro con q is None
```

| Se non ci arriva | Cosa controllare |
|---|---|
| non propone mai lo schema | la regola strutturale non scatta: la libreria non arriva a 2 chunk distinti? |
| lo propone ma `ΔJ > 0` | `fold_overhead` troppo alto — tornare a M0 |
| lo promuove ma anche mille chunk | `L_H` non penalizza la crescita del vocabolario |

> **Questo gate è al 7 agosto.** Se non passa, il problema è nel sistema, non nel fenomeno. Si risolve prima di procedere, o si chiude il progetto avendo speso quattro giorni.

---

# Fase 2 — Il ciclo (8–14 agosto)

## M5 — Proponente enumerativo

**Contenuto**: `proposer_enum.py`

```python
def plan_enum(order, lib, budget, C) -> tuple[Plan, int, bool]
```

Ricerca su partizioni parziali, priorità = `encoding_len` del parziale, arresto dopo `budget` nodi, ritorno del piano di **costo fisico** minimo tra quelli completati.

**Test** (`test_proposer.py`):

```python
def test_unbounded_finds_optimum():
    p, _, trunc = plan_enum(("x", 11), lib, budget=10**6, C=6)
    assert not trunc
    assert len(p) == optimal_trips(11, 6)

def test_budget_bites():
    # IL TEST CRITICO: con lotto_4 in libreria e budget stretto,
    # il piano trovato deve essere peggiore dell'ottimo
    lib = Library([Macro("lotto_4", 4)])
    p_small, _, _ = plan_enum(("x", 11), lib, budget=20, C=6)
    p_large, _, _ = plan_enum(("x", 11), lib, budget=10**6, C=6)
    assert physical_cost(p_small) > physical_cost(p_large)

def test_library_changes_search_order():
    # senza libreria, budget stretto → risultato diverso che con libreria
    ...
```

**Criterio di uscita**: `test_budget_bites` passa.

> **Rischio concreto**: con `C = 6` e `N ≤ 12` le partizioni sono poche decine. Se `B = 20` basta comunque a trovare l'ottimo, il budget non morde e il fenomeno non può emergere.
>
> **Correzione**: ampliare `N_range` a `[2, 30]`, o abbassare `B`. Da scoprire qui, non a M7.

Produrre un grafico diagnostico: costo del piano trovato in funzione di `B`, per alcuni `N`. Serve a scegliere il range di `B` della griglia.

## M6 — Loop online, `B = ∞`

**Contenuto**: `loop.py`

```python
def run(stream, C, budget, eps, promotion_interval, seed, oracle=False,
        proposer="enum", log_path=...) -> RunResult
```

Ciclo: ordine → proponente → esecuzione → buffer → (ogni `promotion_interval`) proposta, valutazione, verifica, promozione, log di `ΔJ_remove`.

**Criterio di uscita**: con `B = ∞`, schedule `rich`, il sistema arriva allo schema — **cioè riproduce il comportamento offline**.

Se online e offline divergono con budget infinito, c'è un bug nel loop, non un fenomeno.

### Il logging, da subito

Una riga JSONL per episodio:

```json
{"t":142, "order":["bottiglia",11], "batch_sizes":[4,4,3],
 "phys_cost":83, "n_trips":3, "optimal_trips":2, "regret":1,
 "proposer":"enum", "nodes_expanded":20, "budget_truncated":true,
 "encoding_len":12.4, "lib":["lotto_4"], "L_H":31.2,
 "explored_random":false,
 "k_orders_so_far":9, "k_buffer_so_far":4}
```

> **`k_orders_so_far` e `k_buffer_so_far` vanno loggate fin da subito.** La loro divergenza è la misura centrale del fenomeno, non una metrica accessoria.

Una riga per intervallo di promozione:

```json
{"t":150, "proposed":["lotto_3","trasporta_lotto"],
 "rejected":[{"cand":"trasporta_lotto","reason":"delta_J","value":4.1}],
 "promoted":["lotto_3"],
 "delta_J_remove":{"lotto_4":8.3,"lotto_3":1.2},
 "structural_candidate_fired":true}
```

## M7 — GATE DEL PILOT

**Contenuto**: `experiments/gate_pilot.py`

Le tre condizioni diagnostiche, 5 semi ciascuna:

| | budget | schedule |
|---|---|---|
| A | ∞ | poor_then_rich |
| B | stretto | poor_then_rich |
| C | stretto | rich |

**Le quattro domande, in ordine:**

**1. B si blocca?** `reached_schema == False` in B, `True` in A e C.

**2. `ΔJ_remove` del chunk è positivo in B?**
> Se negativo: la macro resta solo perché la rimozione è vietata. È inerzia, non autoconferma. **Non c'è il fenomeno.**

**3. Le metriche interne di B sono buone?** Costo dei piani nel suo vocabolario basso, MDL soddisfatto, verifica superata.
> Se anche le metriche interne sono cattive, è un fallimento già documentato in letteratura, non questo.

**4. `k_buffer` di B diverge da `k_orders`?**
> È la firma del fenomeno. Se le due curve coincidono, il comportamento non si è impoverito e il blocco ha un'altra causa.

**Criterio di uscita**: tutte e quattro affermative.

| Esito | Decisione |
|---|---|
| Tutte e quattro sì | procedere a M8 |
| `ΔJ_remove < 0` | il fenomeno è inerzia. Provare a rendere reversibili le promozioni e vedere se resta qualcosa. Se no, chiudere |
| B non si blocca | provare budget più stretto, `k_poor` più lungo, `N_range` più ampio. **Al massimo due giorni di tentativi**, poi chiudere |
| Metriche interne cattive | non è il fenomeno cercato. Chiudere o riposizionare |

> **14 agosto.** Se il gate non passa, si sono spesi undici giorni e si è imparato che il fenomeno non emerge in questo disegno. È un esito accettabile e va accettato senza estendere la deadline interna.

---

# Fase 3 — Risultati (15–23 agosto)

## M8 — Griglia ENUM completa

**Contenuto**: `experiments/grid_enum.py`

```
B          ∈ {∞, 500, 200, 100, 50, 20, 10}
schedule   ∈ {poor_then_rich, rich, poor_forever, slow_drift}
k_poor     ∈ {50, 100, 200}                    solo poor_then_rich
semi       10
```

Più le condizioni diagnostiche:
- `oracle_proposal` attivo, su B
- promozioni reversibili, su B
- ablazione del candidato strutturale
- sensibilità: `ε ∈ {0.05,0.1,0.2}`, `C ∈ {4,6,8}`, `promotion_interval ∈ {10,25,50}`, due codifiche di `L_H`

**Ogni run verifica l'hash dello stream prima di partire.**

**Criterio di uscita**: `logs/` completo, nessuna run fallita, hash tutti verificati.

**Analisi immediata, prima di procedere:**

1. **La transizione in `B` è netta o graduale?** Determina la forza del risultato.
2. **Il confine cade a un valore costante di `k_buffer`?** Se sì, è il risultato migliore possibile: la soglia non dipende da come ci si arriva.
3. **La transizione cade dove `PREDICTION.md` diceva?**

## M9 — Proponente appreso

**Contenuto**: `proposer_learn.py`, `experiments/grid_learn.py`

**Solo se M7 è passato.**

```python
class PartitionModel:
    def fit(self, executed_partitions, incremental=True)
    def sample_partition(self, order, lib, C) -> Partition

def plan_learn(order, lib, model, k_samples, C) -> Plan
```

GRU o transformer minimo: 2 layer, hidden 64. Cross-entropy sulle partizioni eseguite. Fine-tuning incrementale a ogni `promotion_interval`.

Griglia ridotta:

```
k_samples  ∈ {1, 3, 10, 30, 100}
retrain    ∈ {incremental, from_scratch}
schedule   ∈ {poor_then_rich, rich}
semi       15
```

Più sensibilità alla capacità: `hidden ∈ {32, 64, 128}`.

**Criterio di uscita**: il fenomeno compare anche in LEARN, oppure non compare e lo si dichiara.

**L'ablazione dei canali** è il risultato specifico di questa fase: `incremental` contro `from_scratch` a parità di tutto. Se il blocco sparisce con `from_scratch`, la retroazione passa per i pesi del proponente e non solo per il vocabolario.

> Se M9 sfora, si taglia. Il paper regge con la sola variante ENUM, dichiarando LEARN come lavoro futuro.

---

# Fase 4 — Paper (24 agosto – 9 settembre)

## M10 — Analisi e figure

**Contenuto**: `analysis.py`

Tutte le figure da log esistenti, nessuna riesecuzione.

| Figura | Contenuto |
|---|---|
| **F1** | Diagramma di fase: `B` × `k_poor`, colore = P(raggiunge lo schema). Due pannelli, ENUM e LEARN |
| **F2** | Istogramma delle dimensioni di lotto in A e B, stessi ordini |
| **F3** | `k_orders` e `k_buffer` nel tempo, curve per condizione |
| **F4** | Costo fisico sul test set congelato in funzione di `B` |
| **F5** | Diagnosi: distribuzione delle run bloccate tra i quattro meccanismi |
| **F6** | `ΔJ_remove` nel tempo |

Il paper ne conterrà **due o tre**. Le altre vanno nel repository.

> **F3 è la candidata a figura principale.** Mostra il fenomeno nella sua forma più diretta: stessi ordini in ingresso, esperienza osservata diversa.

## M11 — Stesura

| Sezione | Spazio | Giorni |
|---|---|---|
| Setup e metodo | 0,75 p | 28–29 ago |
| Risultati | 1 p | 30–31 ago |
| Introduzione | 0,5 p | 1–2 set |
| Related work | 0,4 p | 2 set |
| Limiti e discussione | 0,5 p | 3 set |
| Riferimenti | 0,25 p | 4 set |
| Rilettura | | 5 set |

> **Scrivere il metodo per primo e l'introduzione per ultima.** L'introduzione va scritta sapendo cosa si è trovato; scritta prima, si finisce a difendere una tesi che i dati non sostengono.

**Nel related work**: mezza pagina sul ponte con i sistemi a skill library, ancorata al caso pubblicato della riscrittura per query invece della parametrizzazione una volta sola. Da dichiarare come analogia argomentata, non come evidenza.

## M12 — Revisione e submission

| | |
|---|---|
| 6 set | rilettura a freddo, taglio |
| 7 set | repository pubblico: codice, `PREDICTION.md`, log aggregati, figure |
| 8 set | verifica riproducibilità da repo pulito |
| **9 set** | **submission** |

> Il 10 resta libero per problemi tecnici di OpenReview.

---

# Gestione del rischio

| Rischio | Probabilità | Rilevato a | Mitigazione |
|---|---|---|---|
| `k*` fuori dal range utile | media | **M0** | aggiustare `fold_overhead`, dichiarare la sensibilità |
| Il budget non morde | **alta** | **M5** | ampliare `N_range` o abbassare `B` |
| Il sistema non arriva allo schema offline | media | **M4** | rivedere `L_H` o la regola di proposta |
| Il fenomeno non emerge | media | **M7** | due giorni di tentativi, poi chiudere |
| `ΔJ_remove < 0` | media | **M7** | è inerzia: riposizionare o chiudere |
| Transizione graduale invece che netta | media | **M8** | risultato più debole, riportarlo comunque |
| LEARN sfora | media | M9 | tagliare, dichiarare come futuro |
| Sforamento della stesura | bassa | M11 | il metodo è scritto per primo: c'è sempre qualcosa da consegnare |

**I tre rischi in grassetto per data sono rilevati entro il 14 agosto.** È il disegno del piano: i modi di fallire si scoprono nella prima metà, quando restano ancora quattro settimane.

---

# Cosa fare il primo giorno

1. Creare il repository e la struttura
2. **Calcolare `k*` a mano** e committare `PREDICTION.md` con la data
3. Scrivere `domain.py` e `test_domain.py`
4. Far passare `test_optimum_is_ceiling`

Mezza giornata di calcolo, mezza di codice. E alla fine si sa se l'esperimento ha una finestra in cui vivere.
