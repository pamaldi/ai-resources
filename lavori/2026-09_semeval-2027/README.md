# SemEval 2027

tipo: shared task
stato: in corso — training data dall'8 settembre 2026 · valutazione 10-31 gennaio 2027 · paper febbraio · notifica marzo · camera-ready aprile 2027
periodo: 2026-08 →
codice: —
argomenti: [reasoning, interpretability]

---

## Cos'è

Scelta e preparazione delle task SemEval 2027 su cui partecipare, in continuità con la pipeline neuro-simbolica NS-EDL usata al Task 11 del 2026 (96,34% di accuratezza, TCE ~1.02).

**Il criterio di selezione è uno solo: verificabilità formale.** La task deve avere un punto in cui un componente simbolico *decide* invece di *stimare* — e quel punto deve essere dentro la metrica di ranking, non a lato. È il motivo per cui quasi tutte le task vengono scartate.

## Dove sto

| Task | Verdetto | In una riga |
|---|---|---|
| **2 — DiCo-NLI** (ex CoCo-NLI) | **primaria** | verificabilità dentro la metrica, edge architetturale garantito, costo basso |
| **11 — VAKRA cap. 4** | seconda, opportunistica | 26 template di policy formalizzabili, verificati programmaticamente |
| **10 — AgentRisk** | aperta | dipende se le policy sono formali o vaghe; ora c'è VAKRA come precedente |
| 8 — StereoQueerEval | no come task | ma il dataset HODIAT apre un filone mech int indipendente e già disponibile |
| 7 — CLaS · 6 — MMCultureQA · 1 — RETECO | no | metrica neurale o ranking puro: niente da validare |

**Vincolo di realtà**: tre task in parallelo, tutte valutate a gennaio 2027, non stanno in piedi.

## Cosa c'è qui

| Documento | Cos'è |
|---|---|
| [valutazione-task.md](valutazione-task.md) | **il riferimento corrente**: sette task valutate con lo stesso criterio, il calendario corretto, e il filone mech int su HODIAT |
| [task-2-dico-nli-organizzatori.md](task-2-dico-nli-organizzatori.md) | repository, trial data, starter kit, scorer e profili degli organizzatori della task primaria |
| [agentrisk-autori-pubblicazioni.md](agentrisk-autori-pubblicazioni.md) | organizzatori e pubblicazioni recenti della Task 10 |
| [reading-list.md](reading-list.md) | la prima valutazione, su due sole task — superata in parte, resta per il dettaglio bibliografico |
| [pdf/](pdf/) | l'overview paper NumEval come modello di system paper |

## Le prossime mosse

- [ ] Issue su `IBM/vakra`: richiedere il PolicyJudge, che non è nel repo e senza cui il gate di policy non è misurabile in locale
- [ ] Issue su DiCo-NLI per l'artefatto `NEGATIVE_OTHER` singleton
- [ ] Email a Cignarella per l'accesso a HODIAT — il filone mech int non ha scadenza SemEval, ed è l'unico portabile avanti fuori dal budget di gennaio
- [ ] Parsare i piani gold del train VAKRA cap. 1 e verificare che il type-checker accetti il 100% dei gold

## Aperto

- **Sul sito ufficiale la Task 2 è ancora registrata come CoCo-NLI**, mentre il repository degli organizzatori usa DiCo-NLI. Stessa task, stessi autori: vanno tenuti entrambi i nomi per cercare letteratura e comunicazioni.
- **Manca la scheda del lavoro del 2026** (Task 11, NS-EDL). È il precedente su cui poggia tutto il criterio di selezione e non esiste come documento.
