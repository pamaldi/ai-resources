# AI Resources

Archivio di lavoro personale: bibliografie ragionate, note di studio, progetti di ricerca in corso.
L'organizzazione è **per funzione**: cosa ha una scadenza, cosa è sapere sedimentato, cosa è ancora da triare.

```
projects/     lavori con una deadline
topics/       dossier tematici — bibliografie e note che restano
formazione/   corsi, valutazioni, appunti di corso
library/      PDF (libri, paper, materiali di corso)
conferenze.md conference e venue da tenere d'occhio
inbox.md      link grezzi non ancora triati

bibliografia-trasversale.md   lettura incrociata delle otto bibliografie
```

---

## Progetti attivi

| Progetto | Scadenza | Stato |
|---|---|---|
| [SemEval 2027 — CoCo-NLI vs AgentRisk](projects/semeval-2027/) | sample data dal 1 set 2026 | valutazione candidati |

---

## I fili di ricerca

Le cartelle sono per funzione, ma il materiale segue sei fili. Questa è la mappa trasversale.

> Per cosa i fili hanno **in comune** — le voci che ricorrono in più bibliografie, le domande su cui i dossier convergono senza citarsi, e dove i criteri si contraddicono — vedi [bibliografia trasversale](bibliografia-trasversale.md).

### 1. Compressione → astrazione
Perché predire è comprimere, e cosa serve perché un sistema passi da una descrizione di livello *n* a una di livello *n+1*.

- [Sintesi: compressione, ripetizione e scoperta autonoma di astrazioni](topics/compressione-astrazione/sintesi-compressione-astrazione.md) — MDL, neuroscienze della ripetizione, automi cellulari, HashLife
- [Il testo come mondo pre-compresso vs. la durezza dell'AI fisica](topics/compressione-astrazione/testo-mondo-pre-compresso.md) — reading list ragionata, Moravec in versione moderna
- [La mappa dei libri](topics/compressione-astrazione/mappa-dei-libri.md) — MacKay, Mitchell, Hofstadter; *The Neural Mind* e la critica; citare come strumento vs come legittimità
- [Scoperta di astrazioni — mappa della letteratura](topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) — library learning, skill discovery, la saturazione dell'area e il gap dell'astrazione parametrica

### 2. Intensione, autonomia e nuovi primitivi
Un sistema può estendere il proprio alfabeto, o solo ricombinare i primitivi che ha ricevuto?

- [Bibliografia ragionata](topics/intensione-autonomia/bibliografia.md) — ~60 voci in 17 sezioni: le due tradizioni e il loro disaccordo, le definizioni, i limiti formali, il percorso di lettura, la disponibilità gratuita dei testi
- [Cariani 1991 — dispositivi che costruiscono i propri sensori](topics/intensione-autonomia/cariani-1991-sintesi.md)

### 3. Reasoning e neuro-simbolico
"Reasoning" è un omonimo: almeno dieci programmi di ricerca usano la parola per cose diverse, e non si citano.

- [Bibliografia ragionata](topics/reasoning/reasoning-bibliografia-ragionata.md) — **il documento di riferimento del filo**: undici nuclei (dal metro normativo al sostrato biologico), criterio di inclusione e di uscita espliciti, itinerario in 5 fasi e indice trasversale delle distinzioni
- [Neuro-simbolico e NLP](topics/reasoning-neurosimbolico/neurosimbolico-nlp.md) — theorem proving su spiegazioni, sillogistica, persone e tutorial
- [LLM reasoning](topics/reasoning-neurosimbolico/llm-reasoning.md) — workshop e risorse
- → alimenta [SemEval 2027](projects/semeval-2027/)

### 4. Composizionalità e riuso algoritmico nei Transformer
Dove finisce il riuso di primitive già apprese e dove inizia la costruzione di un algoritmo nuovo. L'aritmetica decimale come banco di prova controllabile.

- [Impostazione del problema](topics/composizionalita_transformer/composizionalita_transformer_frontiera_riuso_algoritmico.md) — la frontiera del riuso algoritmico
- [Disegno sperimentale](topics/composizionalita_transformer/README_composizionalita_transformer_v2.md) — primitive, recupero, routing, memoria intermedia
- [Bibliografia](topics/composizionalita_transformer/BIBLIOGRAFIA_composizionalita_transformer.md) — 21 voci, 12 marcate come portanti per il design
- → il ponte con il filo 2 è [Zeng, P., Griffiths, T. L. & Lake, B. M. (2026), *Nothing from Something: Can a Language Model Discover 0?*](topics/composizionalita_transformer/BIBLIOGRAFIA_composizionalita_transformer.md#-zeng-griffiths--lake--un-modello-può-scoprire-lo-zero), l'unica voce che i due dossier si linkano a vicenda

### 5. Interpretability
- [Papers per livello di profondità](topics/interpretability/papers.md) — dai framework concettuali (Lipton, Rudin) ai metodi meccanicistici
- [Aritmetica e mech interp](topics/interpretability/aritmetica-mech-int.md) — bibliografia operativa per gli esperimenti su addizione e moltiplicazione
- [CoT drift su EDOS + HateXplain](topics/content-drift/bibliografia_drift_mechint.md) — fedeltà della catena di ragionamento, disaccordo annotatoriale, probing e interventi direzionali

### 6. Fondamenti
- [P e NP — riassunto](topics/fondamenti-cs/riassunto-p-np.md)
- [MDP, V e Q](formazione/stanford-ai-mdp.md)
- [Dal campionamento dei token al watermarking](topics/llm/watermarking-llm-sampling.md) — softmax, temperatura, top-p, seed, e il tournament sampling di SynthID
- [Risorse CS](topics/fondamenti-cs/risorse-cs.md)

---

## Formazione

- [Corsi singoli e MOOC](formazione/corsi.md) — 8 corsi tra UniBO e UniFi, costi, calendari, vincoli di iscrizione, azioni
- [Computational Cognitive Modeling — NYU (Lake & Gureckis)](formazione/nyu-ccm-lake-gureckis.md) — corso pubblico, reading list canonica e mappatura ai fili; aggancio forte a composizionalità e program induction
- [Categories and Concepts — NYU (Lake)](formazione/nyu-categories-concepts-lake.md) — seminario sulla psicologia dei concetti; il dominio (contenuto) di cui il CCM dà i metodi, chiude sulla conceptual combination
- [Appunti Stanford — MDP](formazione/stanford-ai-mdp.md)

**Prossime azioni** (dettaglio in [corsi.md §7](formazione/corsi.md)): mail a Garagnani · verifica che la carriera Master AI risulti chiusa · contatto con la Segreteria di Semiotica. Le ultime due maturano da sole, conviene avviarle subito.

---

## Lavori aperti

- [x] ~~Fondere le due bibliografie intensione/autonomia in un solo documento canonico~~
- [x] ~~Splittare `formazione-corsi-e-letture.md` e riconciliare i verdetti sui corsi UniBO~~
- [x] ~~Triare `inbox.md` verso i dossier tematici~~
- [x] ~~Progetto NEmo 2026: chiuso il 18 agosto 2026.~~ Le note bibliografiche sopravvissute sono in [scoperta-di-astrazioni-letteratura.md](topics/compressione-astrazione/scoperta-di-astrazioni-letteratura.md); il resto è recuperabile dalla storia di git
- [ ] Ruotare la password su nemo.semantic.review — è ancora nella storia di git
- [ ] Sostituire i redirect `lnkd.in` in [inbox.md](inbox.md) con gli URL reali
- [ ] Committare `topics/reasoning/` e `topics/content-drift/`: ~1050 righe ancora untracked, tra cui la bibliografia più curata dell'archivio
- [ ] Riscrivere [interpretability/papers.md](topics/interpretability/papers.md) — porta residui di conversazione (riga 124), il livello 0 è in coda invece che in testa, l'indice annuncia voci che non esistono
- [ ] Fondere [neurosimbolico-nlp.md](topics/reasoning-neurosimbolico/neurosimbolico-nlp.md) (appunti grezzi) nel nucleo K della [bibliografia reasoning](topics/reasoning/reasoning-bibliografia-ragionata.md), che copre la stessa area meglio
- [ ] Scegliere **una** convenzione di verifica delle citazioni: oggi convivono `[V]`/`[M]`, `✔`/`⚠` e nessuna. È l'annotazione che serve davvero sei mesi dopo

---

## Contatti

pamaldi@gmail.com · licenza MIT
