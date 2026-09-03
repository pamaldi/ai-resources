# Composizionalità e riuso algoritmico nei Transformer

**La domanda.** Dove finisce il riuso di primitive già apprese e dove inizia la costruzione di un algoritmo nuovo. L'aritmetica decimale come banco di prova controllabile.

**Stato.** attivo · ultima revisione: 3 settembre 2026

---

## Cosa c'è qui

| Documento | Cos'è |
|---|---|
| [frontiera-riuso-algoritmico.md](frontiera-riuso-algoritmico.md) | impostazione del problema: dov'è la frontiera del riuso |
| [disegno-sperimentale.md](disegno-sperimentale.md) | primitive, recupero, routing, memoria intermedia |
| [bibliografia.md](bibliografia.md) | 21 voci, 12 marcate ★ come portanti per il design |
| [pdf/](pdf/) | quattro paper |

## Voci portanti

- **John Hewitt e Percy Liang — *Designing and Interpreting Probes with Control Tasks*** (EMNLP-IJCNLP 2019). Il correttivo metodologico che rende non pubblicabile metà di quello che si vorrebbe scrivere.
- **Nouha Dziri e altri — *Faith and Fate: Limits of Transformers on Compositionality*** (NeurIPS 2023). La composizionalità come grandezza graduabile, sul caso aritmetico.
- **P. Zeng, T. L. Griffiths e B. M. Lake — *Nothing from Something: Can a Language Model Discover 0?*** (CCN 2026). Un modello addestrato in un mondo senza lo zero può postularlo quando gli serve? Il ponte con [intensione e autonomia](../intensione-autonomia/). [PDF](pdf/Zeng-Griffiths-Lake_Discover-Zero-CCN26.pdf)
- **Steven M. Frankland e Joshua D. Greene — *Concepts and Compositionality: In Search of the Brain's Language of Thought*** (Annual Review of Psychology, 2020). Il binding fra concetto e ruolo, e la separazione fra memoria e computazione. [PDF](pdf/Frankland-Greene_Concepts-Compositionality-LoT-AnnRevPsy20.pdf)
- **Philip Quirke, Clement Neo e Fazl Barez — *Understanding Addition and Subtraction in Transformers*** (arXiv:2402.02619). [PDF](pdf/Quirke-Neo-Barez_Understanding-Addition-and-Subtraction-in-Transformers.pdf)
- **Geoffrey E. Hinton, James L. McClelland e David E. Rumelhart — *Distributed Representations*** (in *Parallel Distributed Processing*, MIT Press, 1986). Il substrato di cui tutta la domanda è una specificazione. [PDF](pdf/Hinton-McClelland-Rumelhart_Distributed-Representations.pdf)

## Agganci

- [Intensione e autonomia](../intensione-autonomia/) — la giuntura è Zeng, Griffiths e Lake, l'unica voce che i due argomenti si linkano a vicenda
- [Interpretability](../interpretability/) — i circuiti che il disegno sperimentale va a cercare
- [Compressione → astrazione](../compressione-astrazione/) — il lato "teoria del meccanismo"

## Aperto

- **Lo stesso paper è registrato con tre titoli diversi.** `arXiv:2402.02619` compare come *Arithmetic in Transformers Explained* qui, *Understanding Addition and Subtraction in Transformers* in interpretability, *Understanding Addition in Transformers* nel nucleo I.3 di reasoning — e con due liste autori diverse (Quirke, Neo e Barez oppure Quirke e Barez). Da risolvere una volta sola, prima che finisca in un paper.
