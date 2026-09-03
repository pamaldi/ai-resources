# Lavori

Cosa ho fatto e cosa sto facendo: shared task, workshop, progetti software, talk. Un lavoro entra qui quando ha **una data**; un argomento sta in [`argomenti/`](../argomenti/) perché non ne ha.

## La convenzione

Un lavoro è **un file** `AAAA-MM_slug.md`, o **una cartella** `AAAA-MM_slug/` con un `README.md` quando produce più di un documento. Il prefisso dà il diario in ordine cronologico senza bisogno di crearne uno: la data è quella di inizio, non di fine.

Ogni scheda apre con la stessa intestazione a campi fissi:

```markdown
# <Nome>

tipo: shared task | workshop | progetto sw | talk
stato: in corso | chiuso | abbandonato
periodo: 2026-06 → 2026-09
codice: <URL del repo, o il percorso locale se il codice non è qui>
argomenti: [reasoning, interpretability]
```

Poi tre sezioni, sempre le stesse:

- **Cosa fa / cos'era** — tre righe.
- **Cosa ho imparato** — il pezzo che vale, e l'unica cosa che il codice da solo non conserva.
- **Dove si è rotto** — l'altra cosa che il codice non conserva.

**Il codice non sta qui.** Il campo `codice:` punta al repository vero; questa cartella tiene la *memoria* del lavoro. Fra sei mesi il codice lo ritrovi da solo, il motivo per cui l'avevi scritto no.

Il campo `argomenti:` è il legame nell'altro verso: la scheda dell'argomento cita il lavoro sotto «Cosa ci ho fatto», il lavoro cita l'argomento qui. Nessuno dei due duplica l'altro.

---

## Indice

| Lavoro | Tipo | Stato | Argomenti |
|---|---|---|---|
| [2026-09 — SemEval 2027](2026-09_semeval-2027/) | shared task | in corso · valutazione 10-31 gen 2027 | reasoning, interpretability |

**Da recuperare** — lavori già fatti che non hanno ancora una scheda:

- [ ] **SemEval 2026 Task 11 — pipeline NS-EDL** (96,34% di accuratezza, TCE ~1.02). È citata come precedente in mezzo archivio e non ha un documento proprio da nessuna parte.
- [ ] **Progetto NEmo 2026**, chiuso il 18 agosto 2026. Le note bibliografiche sono in [scoperta-di-astrazioni-letteratura.md](../argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md), il resto solo nella storia di git.
- [ ] I workshop seguiti e i piccoli progetti software: una scheda ciascuno, anche di dieci righe.
