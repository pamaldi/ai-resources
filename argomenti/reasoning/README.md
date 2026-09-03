# Reasoning e neuro-simbolico

**La domanda.** «Reasoning» è un omonimo: almeno dieci programmi di ricerca usano la parola per cose diverse, e non si citano.

**Stato.** attivo — è l'argomento che alimenta il lavoro SemEval · ultima revisione: 3 settembre 2026 · citazioni al maggio 2026

---

## Cosa c'è qui

| Documento | Cos'è |
|---|---|
| [bibliografia-ragionata.md](bibliografia-ragionata.md) | **il documento di riferimento**: ~120 voci in undici nuclei (dal metro normativo al sostrato biologico), criterio di inclusione e di uscita espliciti, itinerario in 5 fasi, indice trasversale delle distinzioni |
| [neurosimbolico-nlp.md](neurosimbolico-nlp.md) | appunti grezzi: theorem proving su spiegazioni, sillogistica, persone e tutorial |
| [llm-reasoning.md](llm-reasoning.md) | workshop, venue e risorse |

## Voci portanti

- **David Marr — *Vision: A Computational Investigation into the Human Representation and Processing of Visual Information*** (W. H. Freeman, 1982), capitolo 1. I tre livelli di analisi: sette degli undici sensi di "reasoning" si dispongono su di essi, e quasi tutti i disaccordi pubblici sono confusioni di livello.
- **Stephen A. Cook e Robert A. Reckhow — *The Relative Efficiency of Propositional Proof Systems*** (Journal of Symbolic Logic 44(1), 1979) insieme a **Armin Haken — *The Intractability of Resolution*** (Theoretical Computer Science 39, 1985). La difficoltà del problema non è il limite dell'agente: la distinzione più assente dalla letteratura ML sul reasoning.
- **Silvia Bernardi, Marcus K. Benna, Mattia Rigotti, Jérôme Munuera, Stefano Fusi e C. Daniel Salzman — *The Geometry of Abstraction in the Hippocampus and Prefrontal Cortex*** (Cell 183(4), 2020). La CCGP: decodificabile ≠ astratto, con una metrica già costruita.

## Cosa ci ho fatto

- **SemEval 2026 Task 11 — pipeline NS-EDL**: 96,34% di accuratezza, TCE ~1.02. È il precedente concreto su cui si regge la scelta delle task 2027.
- **[SemEval 2027](../../lavori/2026-09_semeval-2027/)** — in corso. Il criterio di selezione — verificabilità formale: deve esistere un punto in cui un componente simbolico *decide* invece di *stimare* — viene da qui.

## Agganci

- [Interpretability](../interpretability/) — la catena di ragionamento come oggetto da verificare, non da leggere
- [Fondamenti](../fondamenti/) — i limiti formali su cui poggia il nucleo F

## Aperto

- **Fondere [neurosimbolico-nlp.md](neurosimbolico-nlp.md) nel nucleo K** della bibliografia ragionata, che copre la stessa area meglio. Averli messi nella stessa cartella è il primo passo; la fusione editoriale è ancora da fare.
