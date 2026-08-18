# AI Resources

Archivio di lavoro personale: bibliografie ragionate, note di studio, progetti di ricerca in corso.
L'organizzazione è **per funzione**: cosa ha una scadenza, cosa è sapere sedimentato, cosa è ancora da triare.

```
projects/     lavori con una deadline
topics/       dossier tematici — bibliografie e note che restano
formazione/   corsi, valutazioni, appunti di corso
library/      PDF (libri, paper, materiali di corso)
inbox.md      link grezzi non ancora triati
```

---

## Progetti attivi

| Progetto | Scadenza | Stato |
|---|---|---|
| [NEmo 2026 — astrazioni performativamente stabili](projects/nemo-neurips-2026/) | submission 9–10 set 2026 | specifica e piano completi, implementazione da avviare |
| [SemEval 2027 — CoCo-NLI vs AgentRisk](projects/semeval-2027/) | sample data dal 1 set 2026 | valutazione candidati |

**NEmo 2026** — i documenti in ordine di lettura:
1. [Contesto del progetto](projects/nemo-neurips-2026/progetto-nemo-2026-contesto.md) — idea, letteratura, decisioni prese
2. [Verifica di originalità e riposizionamento](projects/nemo-neurips-2026/nemo-verifica-originalita-e-riposizionamento.md) — cosa è già stato fatto, dove resta il gap
3. [Specifica sperimentale](projects/nemo-neurips-2026/specifica-sperimentale.md) — il disegno completo
4. [Piano di implementazione](projects/nemo-neurips-2026/piano-implementazione.md) — 12 milestone, due gate di arresto
5. [Reading list v4](projects/nemo-neurips-2026/reading-list-v4.md) — ~11 ore, razionate per quando servono
6. [Formazione, corsi e letture](projects/nemo-neurips-2026/formazione-corsi-e-letture.md) — *da splittare: la parte corsi va in `formazione/`*

---

## I fili di ricerca

Le cartelle sono per funzione, ma il materiale segue cinque fili. Questa è la mappa trasversale.

### 1. Compressione → astrazione
Perché predire è comprimere, e cosa serve perché un sistema passi da una descrizione di livello *n* a una di livello *n+1*.

- [Sintesi: compressione, ripetizione e scoperta autonoma di astrazioni](topics/compressione-astrazione/sintesi-compressione-astrazione.md) — MDL, neuroscienze della ripetizione, automi cellulari, HashLife
- [Il testo come mondo pre-compresso vs. la durezza dell'AI fisica](topics/compressione-astrazione/testo-mondo-pre-compresso.md) — reading list ragionata, Moravec in versione moderna
- → sfocia direttamente in [NEmo 2026](projects/nemo-neurips-2026/)

### 2. Intensione, autonomia e nuovi primitivi
Un sistema può estendere il proprio alfabeto, o solo ricombinare i primitivi che ha ricevuto?

- [Bibliografia ragionata](topics/intensione-autonomia/bibliografia.md) — ~60 voci in 17 sezioni: le due tradizioni e il loro disaccordo, le definizioni, i limiti formali, il percorso di lettura, la disponibilità gratuita dei testi
- [Cariani 1991 — dispositivi che costruiscono i propri sensori](topics/intensione-autonomia/cariani-1991-sintesi.md)

### 3. Reasoning e neuro-simbolico
- [Neuro-simbolico e NLP](topics/reasoning-neurosimbolico/neurosimbolico-nlp.md) — theorem proving su spiegazioni, sillogistica, persone e tutorial
- [LLM reasoning](topics/reasoning-neurosimbolico/llm-reasoning.md) — workshop e risorse
- → alimenta [SemEval 2027](projects/semeval-2027/)

### 4. Interpretability
- [Papers per livello di profondità](topics/interpretability/papers.md) — dai framework concettuali (Lipton, Rudin) ai metodi meccanicistici

### 5. Fondamenti
- [P e NP — riassunto](topics/fondamenti-cs/riassunto-p-np.md)
- [MDP, V e Q](formazione/stanford-ai-mdp.md)
- [Risorse CS](topics/fondamenti-cs/risorse-cs.md)

---

## Formazione

- [Corsi singoli UniBO — semiotica e filosofia del linguaggio](formazione/unibo.md) — costi, calendari, verdetti
- [Appunti Stanford — MDP](formazione/stanford-ai-mdp.md)

---

## Lavori aperti

- [x] ~~Fondere le due bibliografie intensione/autonomia in un solo documento canonico~~
- [ ] Splittare `formazione-corsi-e-letture.md`: la valutazione corsi in `formazione/`, la mappa dei libri in `topics/compressione-astrazione/`
- [ ] Riconciliare i verdetti sui corsi UniBO (`formazione/unibo.md` dice Cognitive Semantics, `formazione-corsi-e-letture.md` dice Universal Semantics)
- [ ] Triare [inbox.md](inbox.md) verso i dossier tematici

---

## Contatti

pamaldi@gmail.com · licenza MIT
