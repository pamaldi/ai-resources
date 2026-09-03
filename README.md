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

bibliografia-trasversale.md   lettura incrociata delle nove bibliografie
```

---

## Progetti attivi

| Progetto | Scadenza | Stato |
|---|---|---|
| [SemEval 2027 — DiCo-NLI, VAKRA, AgentRisk](lavori/2026-09_semeval-2027/) | training data 8 set 2026 · valutazione 10–31 gen 2027 | [sette task valutate](lavori/2026-09_semeval-2027/valutazione-task.md): Task 2 primaria, Task 11 cap. 4 opportunistica |

---

## I fili di ricerca

Le cartelle sono per funzione, ma il materiale segue sei fili. Questa è la mappa trasversale.

> Per cosa i fili hanno **in comune** — le voci che ricorrono in più bibliografie, le domande su cui i dossier convergono senza citarsi, e dove i criteri si contraddicono — vedi [bibliografia trasversale](bibliografia-trasversale.md).

### 1. Compressione → astrazione
Perché predire è comprimere, e cosa serve perché un sistema passi da una descrizione di livello *n* a una di livello *n+1*.

- [Sintesi: compressione, ripetizione e scoperta autonoma di astrazioni](argomenti/compressione-astrazione/sintesi-compressione-astrazione.md) — MDL, neuroscienze della ripetizione, automi cellulari, HashLife
- [Il testo come mondo pre-compresso vs. la durezza dell'AI fisica](argomenti/compressione-astrazione/testo-mondo-pre-compresso.md) — reading list ragionata, Moravec in versione moderna
- [La mappa dei libri](argomenti/compressione-astrazione/mappa-dei-libri.md) — MacKay, Mitchell, Hofstadter; *The Neural Mind* e la critica; citare come strumento vs come legittimità
- [Scoperta di astrazioni — mappa della letteratura](argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) — library learning, skill discovery, la saturazione dell'area e il gap dell'astrazione parametrica

### 2. Intensione, autonomia e nuovi primitivi
Un sistema può estendere il proprio alfabeto, o solo ricombinare i primitivi che ha ricevuto?

- [Bibliografia ragionata](argomenti/intensione-autonomia/bibliografia.md) — ~60 voci in 17 sezioni: le due tradizioni e il loro disaccordo, le definizioni, i limiti formali, il percorso di lettura, la disponibilità gratuita dei testi
- [Cariani 1991 — dispositivi che costruiscono i propri sensori](argomenti/intensione-autonomia/cariani-1991-sintesi.md)

### 3. Reasoning e neuro-simbolico
"Reasoning" è un omonimo: almeno dieci programmi di ricerca usano la parola per cose diverse, e non si citano.

- [Bibliografia ragionata](argomenti/reasoning/bibliografia-ragionata.md) — **il documento di riferimento del filo**: undici nuclei (dal metro normativo al sostrato biologico), criterio di inclusione e di uscita espliciti, itinerario in 5 fasi e indice trasversale delle distinzioni
- [Neuro-simbolico e NLP](argomenti/reasoning/neurosimbolico-nlp.md) — theorem proving su spiegazioni, sillogistica, persone e tutorial
- [LLM reasoning](argomenti/reasoning/llm-reasoning.md) — workshop e risorse
- → alimenta [SemEval 2027](lavori/2026-09_semeval-2027/)

### 4. Composizionalità e riuso algoritmico nei Transformer
Dove finisce il riuso di primitive già apprese e dove inizia la costruzione di un algoritmo nuovo. L'aritmetica decimale come banco di prova controllabile.

- [Impostazione del problema](argomenti/composizionalita-transformer/frontiera-riuso-algoritmico.md) — la frontiera del riuso algoritmico
- [Disegno sperimentale](argomenti/composizionalita-transformer/disegno-sperimentale.md) — primitive, recupero, routing, memoria intermedia
- [Bibliografia](argomenti/composizionalita-transformer/bibliografia.md) — 21 voci, 12 marcate come portanti per il design
- → il ponte con il filo 2 è [Zeng, P., Griffiths, T. L. & Lake, B. M. (2026), *Nothing from Something: Can a Language Model Discover 0?*](argomenti/composizionalita-transformer/bibliografia.md#-zeng-griffiths--lake--un-modello-può-scoprire-lo-zero), l'unica voce che i due dossier si linkano a vicenda

### 5. Interpretability
- [Papers per livello di profondità](argomenti/interpretability/bibliografia.md) — dai framework concettuali (Lipton, Rudin) ai metodi meccanicistici
- [Aritmetica e mech interp](argomenti/interpretability/aritmetica-mech-int.md) — bibliografia operativa per gli esperimenti su addizione e moltiplicazione
- [CoT drift su EDOS + HateXplain](argomenti/interpretability/bibliografia-drift-mechint.md) — fedeltà della catena di ragionamento, disaccordo annotatoriale, probing e interventi direzionali

### 6. Fondamenti
- [P e NP — riassunto](argomenti/fondamenti/riassunto-p-np.md)
- [MDP, V e Q](argomenti/fondamenti/stanford-ai-mdp.md) — e il suo seguito: [Autonomous and Adaptive Systems](formazione/autonomous-adaptive-systems/) (UniBO, Musolesi), la sequenza RL completa da bandit a policy gradient
- [Dal campionamento dei token al watermarking](argomenti/fondamenti/watermarking-llm-sampling.md) — softmax, temperatura, top-p, seed, e il tournament sampling di SynthID
- [Risorse CS](argomenti/fondamenti/risorse-cs.md)

---

## Formazione

- [Corsi singoli e MOOC](formazione/corsi.md) — 8 corsi tra UniBO e UniFi, costi, calendari, vincoli di iscrizione, azioni
- [Computational Cognitive Modeling — NYU (Lake & Gureckis)](formazione/nyu-ccm-lake-gureckis.md) — corso pubblico, reading list canonica e mappatura ai fili; aggancio forte a composizionalità e program induction
- [Categories and Concepts — NYU (Lake)](formazione/nyu-categories-concepts-lake.md) — seminario sulla psicologia dei concetti; il dominio (contenuto) di cui il CCM dà i metodi, chiude sulla conceptual combination
- [Autonomous and Adaptive Systems — UniBO (Musolesi)](formazione/autonomous-adaptive-systems/) — slide pubbliche di tutto il corso; l'ossatura RL che manca all'archivio, più [9 paper della lezione *Intelligent Agents*](formazione/autonomous-adaptive-systems/pdf/)
- [Appunti Stanford — MDP](argomenti/fondamenti/stanford-ai-mdp.md)

**Prossime azioni** (dettaglio in [corsi.md §7](formazione/corsi.md)): mail a Garagnani · verifica che la carriera Master AI risulti chiusa · contatto con la Segreteria di Semiotica. Le ultime due maturano da sole, conviene avviarle subito.

---

## Lavori aperti

- [x] ~~Fondere le due bibliografie intensione/autonomia in un solo documento canonico~~
- [x] ~~Splittare `formazione-corsi-e-letture.md` e riconciliare i verdetti sui corsi UniBO~~
- [x] ~~Triare `inbox.md` verso i dossier tematici~~
- [x] ~~Progetto NEmo 2026: chiuso il 18 agosto 2026.~~ Le note bibliografiche sopravvissute sono in [scoperta-di-astrazioni-letteratura.md](argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md); il resto è recuperabile dalla storia di git
- [ ] Ruotare la password su nemo.semantic.review — è ancora nella storia di git
- [ ] Sostituire i redirect `lnkd.in` in [inbox.md](inbox.md) con gli URL reali
- [x] ~~Committare `topics/reasoning/` e `topics/content-drift/`~~
- [ ] Riscrivere [interpretability/papers.md](argomenti/interpretability/bibliografia.md) — porta residui di conversazione (riga 124), il livello 0 è in coda invece che in testa, l'indice annuncia voci che non esistono
- [ ] Fondere [neurosimbolico-nlp.md](argomenti/reasoning/neurosimbolico-nlp.md) (appunti grezzi) nel nucleo K della [bibliografia reasoning](argomenti/reasoning/bibliografia-ragionata.md), che copre la stessa area meglio
- [ ] Portare nella [bibliografia intensione/autonomia](argomenti/intensione-autonomia/bibliografia.md) la tensione fra le due definizioni di autonomia — quella ingegneristica di Stuart Russell e Peter Norvig (indipendenza dalla conoscenza a priori) e quella epistemica di Peter Cariani (costruirsi nuovi sensori). Emersa confrontando [AAS](formazione/autonomous-adaptive-systems/) con il filo 2, non è scritta da nessuna parte
- [ ] Scegliere **una** convenzione di verifica delle citazioni: oggi convivono `[V]`/`[M]`, `✔`/`⚠` e nessuna. È l'annotazione che serve davvero sei mesi dopo

---

## Contatti

pamaldi@gmail.com · licenza MIT
