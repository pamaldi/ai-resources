# Riferimenti — aritmetica e interpretabilità meccanicistica

Bibliografia di lavoro per gli esperimenti su addizione (e successivamente moltiplicazione).
Ordinata per rilevanza operativa, non cronologicamente.

---

## Tier 1 — Da leggere prima di scrivere codice

### Quirke, Neo, Barez — *Understanding Addition and Subtraction in Transformers*
`arXiv:2402.02619` · https://arxiv.org/abs/2402.02619
Codice: https://github.com/PhilipQuirke/quanta_maths · Modelli su Hugging Face

Il riferimento centrale. 46 modelli piccoli (2–3 layer, 3–4 head, ~10M param) addestrati
da zero su 5–15 cifre; 29 superano 99.999%. Deriva un algoritmo esatto left-to-right basato
sul raffinamento progressivo dell'incertezza di riporto:

- **SA** — somma cifra per cifra mod 10
- **ST** (TriCase) — tri-stato: riporta / non riporta / **incerto** (somma = 9)
- **SV** — combina gli ST via `TriAdd` per risolvere le cascate multi-cifra

Sottrazione strutturalmente identica (SA→MD, ST→MB, SV→MV) più ND e SGN per il segno.

**Cosa prendere**: lo scheletro di circuito condiviso, la conferma causale di SV via
activation + edge path-patching, il test di sufficienza (mappa 0.94 vs. random 0.00),
il riuso polisemantico nei modelli mixed.

**Cosa notare**: l'addizione è la categoria **meno** sensibile al seed (App. G) — non
servono 10 seed. I dati sono **arricchiti** al 60% con edge case (App. B): senza
arricchimento il modello fallisce sulle cascate lunghe.

### Bai et al. — *Why Can't Transformers Learn Multiplication? Reverse-engineering Reveals Long-Range Dependency Pitfalls*
`arXiv:2510.00184` (set. 2025) · https://arxiv.org/abs/2510.00184
Codice: https://github.com/ajyl/icot

Confronta un modello ICoT (100% su 4×4 cifre) con uno standard fine-tuned (<1%),
stessa architettura 2 layer 4 head. Tre risultati:

1. **Dipendenze a lungo raggio** — `ĉ_k = s_k + r_{k-1}` come firma di probing;
   MAE ~1 (ICoT) contro ~80 (SFT).
2. **Meccanismo** — il layer 1 attende a *coppie* di cifre e mette in **cache** il
   prodotto parziale; il layer 2 recupera dai cache site. Un DAG tipo albero binario.
3. **Geometria** — prodotti parziali come **somme di Minkowski**; cifre in **base di
   Fourier** su un prisma pentagonale.

Il fallimento di SFT è un ottimo locale: impara le cifre esterne, le centrali mai.
Scalare a 12 layer non aiuta. Fix: loss ausiliaria che predice `ĉ_k` → 99% senza CoT.

**Perché conta**: la moltiplicazione richiede una cache di prodotti parziali che
addizione e sottrazione **non hanno motivo di sviluppare**. È l'ipotesi precisa sul
punto di rottura del transfer.

---

## Tier 2 — Contesto diretto

### Quirke & Barez — *Understanding Addition in Transformers*
`arXiv:2310.13121` · ICLR 2024 · https://arxiv.org/abs/2310.13121

Il predecessore, su modello a **1 layer**. Cifre calcolate in parallelo, non in sequenza.
Si ferma al ~99% perché usa un SC binario invece del tri-stato ST: fallisce esattamente
sulle cascate. **Non usarlo come baseline architetturale** — servono 2 layer.

### Qiu et al. — *Dissecting Multiplication in Transformers: Insights into LLMs*
`arXiv:2407.15360` · https://arxiv.org/abs/2407.15360

Moltiplicazione a n cifre, scomposta in sottocompiti paralleli per cifra. Diagnosi del
fallimento: riporti successivi + **caching dei risultati intermedi**. Raggiungono >99.9%
su 5 cifre con un transformer minuscolo, battendo GPT-4.
Meno rigoroso di Quirke (8 pagine, "we infer" più che validazione causale con controlli):
mappa del territorio, non ground truth.

### Lee et al. — *Teaching Arithmetic to Small Transformers*
`arXiv:2307.03381` · https://arxiv.org/abs/2307.03381

Formato dei dati e inversione delle cifre. Il motivo per cui si genera il risultato con
la cifra meno significativa per prima: allinea la direzione della generazione
autoregressiva con quella di propagazione del riporto.

### Kantamneni & Tegmark — *Language Models Use Trigonometry to Do Addition*
`arXiv:2502.00873` · https://arxiv.org/abs/2502.00873

Le cifre decimali sono codificate in base di Fourier anche negli LLM veri. Base reale con
k ∈ {0,1,2,5}. Fonte della geometria a prisma pentagonale in Bai et al.
**Nota**: le rappresentazioni di Fourier non sono un artefatto dell'addizione modulare —
ricorrono nell'aritmetica decimale.

---

## Tier 3 — Da consultare se serve

| Riferimento | arXiv | Perché |
|---|---|---|
| Nanda et al., *Progress Measures for Grokking* | `2301.05217` | Addizione modulare via DFT. Ground truth completo ma **nessun transfer** verso l'aritmetica posizionale. |
| McLeish et al., *Transformers Can Do Arithmetic with the Right Embeddings* | `2405.17399` | Abacus embeddings: sblocca la generalizzazione in lunghezza. |
| Cho et al., *Position Coupling* | `2405.20671` | Allinea il flusso computazionale con la propagazione del riporto. |
| Nikankin et al., *Arithmetic Without Algorithms* | `2410.21272` | Gli LLM usano un "sacco di euristiche", non algoritmi puliti. Contrasto utile. |
| Zhang et al., *Interpreting and Improving LLMs in Arithmetic Calculation* | `2409.01659` | Simmetrie tra circuiti di addizione e sottrazione. |
| Lindsey et al., *On the Biology of a Large Language Model* | — (Transformer Circuits) | Claude 3.5 Haiku fa addizione con circuiti ibridi lookup + stima di magnitudine. I modelli di produzione **non** usano gli algoritmi puliti dei modelli specializzati. |
| Deng et al., *From Explicit CoT to Implicit CoT* | `2405.14838` | Il metodo ICoT usato da Bai et al. |

---

## Strumenti citati nei paper

- **Logit lens** — nostalgebraist (2020), AlignmentForum
- **Activation patching / interchange intervention** — Meng et al. (`2202.05262`)
- **Path patching** — Goldowsky-Dill et al. (`2304.05969`)
- **Causal scrubbing** — Jenner et al. (LessWrong, 2023)
- **Sparse autoencoders** — Cunningham et al. (`2309.08600`)
- **Framework circuiti** — Elhage et al. (2021), Transformer Circuits Thread

---

## Note operative

- **Architettura minima**: 2 layer, 3 head. A 1 layer il riporto a cascata non si risolve.
- **Tokenizzazione**: carattere per carattere, 14 token (0-9, +, -, =, *, /).
- **Formato**: cifre meno significative per prime, padding a larghezza fissa.
- **Etichettatura**: ogni esempio va etichettato con la lunghezza della catena di riporto
  *prima* del training. Senza, l'accuratezza aggregata nasconde tutto.
- **SAE**: non necessari sul compito di addizione (poche feature note, nessuna pressione
  a sovrapporre). Eventualmente sul modello di moltiplicazione.
- **Iperparametri di Quirke**: batch 64, AdamW lr 8e-5, weight decay 0.1, betas (0.9, 0.98),
  warmup lineare sul primo quinto poi cosine annealing.
