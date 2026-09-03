# Interpretability

**La domanda.** Cosa significa spiegare un modello, e quando una spiegazione è una scoperta invece che una proiezione di chi guarda.

**Stato.** attivo · ultima revisione: 3 settembre 2026 · ⚠️ letteratura tutta 2023-2026, senza data di validità dichiarata

---

## Cosa c'è qui

| Documento | Cos'è |
|---|---|
| [bibliografia.md](bibliografia.md) | ~35 voci in livelli 0-9, dai framework concettuali (Lipton, Rudin) ai metodi meccanicistici. I livelli sono profondità, non priorità |
| [bibliografia-drift-mechint.md](bibliografia-drift-mechint.md) | ~55 voci in 10 sezioni: CoT drift su EDOS e HateXplain, fedeltà della catena, disaccordo annotatoriale, probing e interventi direzionali. Ha uno schema di verifica proprio (`✔`/`⚠`) |
| [aritmetica-mech-int.md](aritmetica-mech-int.md) | bibliografia operativa per gli esperimenti su addizione e moltiplicazione |
| [elhage-2021-framework-note.md](elhage-2021-framework-note.md) | note di lettura sulla voce più condivisa dell'archivio |

## Voci portanti

- **Nelson Elhage, Neel Nanda, Catherine Olsson e altri — *A Mathematical Framework for Transformer Circuits*** (Transformer Circuits Thread, Anthropic, 2021). **La voce più condivisa dell'archivio**: compare in quattro argomenti su sei. Non è un risultato, è il vocabolario — residual stream, circuiti QK/OV, composizione fra teste. Senza, tre quarti dell'archivio è illeggibile.
- **Miles Turpin, Julian Michael, Ethan Perez e Samuel R. Bowman — *Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting*** (NeurIPS 2023). Il paper fondativo sull'infedeltà della traccia: bias mai menzionati determinano la risposta.
- **Tamera Lanham, Anna Chen, Ansh Radhakrishnan e altri — *Measuring Faithfulness in Chain-of-Thought Reasoning*** (Anthropic, arXiv:2307.13702, 2023). Le metriche di perturbazione: early answering, adding mistakes, filler token, parafrasi.
- **Yonatan Belinkov — *Probing Classifiers: Promises, Shortcomings, and Advances*** (Computational Linguistics 48(1), 2022). Un probe può imparare il task da sé: il correttivo che regge tutto il resto.

## Agganci

- [Composizionalità nei Transformer](../composizionalita-transformer/) — l'oggetto su cui i metodi qui vengono applicati
- [Reasoning](../reasoning/) — la catena di ragionamento come oggetto da verificare
- [Fondamenti](../fondamenti/) — il campionamento dei token, che è dove finisce l'analisi del residual stream

## Aperto

- **[bibliografia.md](bibliografia.md) va riscritta.** Porta residui di conversazione (la riga 124 comincia con «Ottima osservazione — nella lista mancava il "perché" fondamentale»), il livello 0 è appiccicato in coda invece che in testa, e l'indice annuncia voci che non esistono. È l'unico documento dell'archivio che non è stato riscritto dopo essere stato generato.
- **Le due bibliografie restano separate.** Stanno nella stessa cartella perché sono lo stesso argomento, ma la fusione è un lavoro editoriale che non è stato fatto: hanno criteri di inclusione e schemi di verifica diversi.
- **Sparse autoencoder: giudizio opposto nei due documenti.** In [bibliografia.md](bibliografia.md) sono un livello del percorso di lettura; in [bibliografia-drift-mechint.md](bibliografia-drift-mechint.md) sono «il ramo più probabile a farti perdere due mesi senza risultato». Stesso oggetto, verdetto contrario — e nessuno dei due lo sa.
