# AI Resources

Archivio di lavoro personale: bibliografie ragionate, note di studio, lavori in corso.

**Dove va una cosa lo decide una sola domanda.**

```
argomenti/    "cosa so su X"            — sei argomenti, uno per cartella
lavori/       "cosa ho fatto"           — shared task, workshop, progetti sw
formazione/   "cosa sto studiando"      — corsi, valutazioni, appunti
libri/        le monografie, che sono trasversali per natura
inbox.md      "non ho ancora deciso"
conferenze.md conference e venue da tenere d'occhio

bibliografia-trasversale.md   lettura incrociata delle nove bibliografie
```

Tre corollari, che eliminano i casi ambigui: **un PDF sta in `pdf/` dentro l'argomento che lo cita** · **un argomento è una cartella sola** · **ogni cartella ha un `README.md` con la stessa intestazione**.

Il codice dei progetti software **non sta qui**: `lavori/` ne tiene la memoria e punta al repository vero.

---

## In corso

| Lavoro | Scadenza | Stato |
|---|---|---|
| [SemEval 2027 — DiCo-NLI, VAKRA, AgentRisk](lavori/2026-09_semeval-2027/) | training data 8 set 2026 · valutazione 10–31 gen 2027 | [sette task valutate](lavori/2026-09_semeval-2027/valutazione-task.md): Task 2 primaria, Task 11 cap. 4 opportunistica |

---

## Gli argomenti

Sei, e ognuno è una domanda. La scheda di ciascuno dice a che punto è, quali voci reggono, cosa ci ho fatto e cosa resta aperto.

> Per cosa gli argomenti hanno **in comune** — le voci che ricorrono in più bibliografie, le domande su cui convergono senza citarsi, e dove i criteri si contraddicono — vedi [bibliografia trasversale](bibliografia-trasversale.md).

### 1. Compressione → astrazione
*Perché predire è comprimere, e cosa serve perché un sistema passi da una descrizione di livello n a una di livello n+1.*
→ **[scheda](argomenti/compressione-astrazione/)** · [sintesi](argomenti/compressione-astrazione/sintesi-compressione-astrazione.md) · [scoperta di astrazioni — la letteratura](argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md) · [la mappa dei libri](argomenti/compressione-astrazione/mappa-dei-libri.md)

### 2. Intensione, autonomia e nuovi primitivi
*Un sistema può estendere il proprio alfabeto, o solo ricombinare i primitivi che ha ricevuto?*
→ **[scheda](argomenti/intensione-autonomia/)** · [bibliografia](argomenti/intensione-autonomia/bibliografia.md) — ~60 voci in 17 sezioni, le due tradizioni e il loro disaccordo

### 3. Reasoning e neuro-simbolico
*«Reasoning» è un omonimo: almeno dieci programmi di ricerca usano la parola per cose diverse, e non si citano.*
→ **[scheda](argomenti/reasoning/)** · [bibliografia ragionata](argomenti/reasoning/bibliografia-ragionata.md) — il documento più curato dell'archivio: undici nuclei, criteri espliciti, itinerario in 5 fasi
→ alimenta [SemEval 2027](lavori/2026-09_semeval-2027/)

### 4. Composizionalità e riuso algoritmico nei Transformer
*Dove finisce il riuso di primitive già apprese e dove inizia la costruzione di un algoritmo nuovo.*
→ **[scheda](argomenti/composizionalita-transformer/)** · [impostazione](argomenti/composizionalita-transformer/frontiera-riuso-algoritmico.md) · [disegno sperimentale](argomenti/composizionalita-transformer/disegno-sperimentale.md) · [bibliografia](argomenti/composizionalita-transformer/bibliografia.md)
→ il ponte con l'argomento 2 è [**P. Zeng, T. L. Griffiths e B. M. Lake — *Nothing from Something: Can a Language Model Discover 0?***](argomenti/composizionalita-transformer/bibliografia.md#-zeng-griffiths--lake--un-modello-può-scoprire-lo-zero), l'unica voce che i due si linkano a vicenda

### 5. Interpretability
*Cosa significa spiegare un modello, e quando una spiegazione è una scoperta invece che una proiezione.*
→ **[scheda](argomenti/interpretability/)** · [bibliografia per livelli](argomenti/interpretability/bibliografia.md) · [CoT drift su EDOS e HateXplain](argomenti/interpretability/bibliografia-drift-mechint.md) · [aritmetica e mech interp](argomenti/interpretability/aritmetica-mech-int.md)

### 6. Fondamenti
*Il vocabolario che gli altri cinque usano senza definirlo.*
→ **[scheda](argomenti/fondamenti/)** · [P e NP](argomenti/fondamenti/riassunto-p-np.md) · [MDP, V e Q](argomenti/fondamenti/stanford-ai-mdp.md) · [dal campionamento dei token al watermarking](argomenti/fondamenti/watermarking-llm-sampling.md)

---

## Formazione

- [Corsi singoli e MOOC](formazione/corsi.md) — 8 corsi tra UniBO e UniFi, costi, calendari, vincoli di iscrizione, azioni
- [Autonomous and Adaptive Systems — UniBO (Musolesi)](formazione/autonomous-adaptive-systems/) — slide pubbliche di tutto il corso; l'ossatura RL che manca all'archivio, più [9 paper della lezione *Intelligent Agents*](formazione/autonomous-adaptive-systems/pdf/)
- [Computational Cognitive Modeling — NYU (Lake & Gureckis)](formazione/nyu-ccm-lake-gureckis.md) — corso pubblico, reading list canonica e mappatura agli argomenti; aggancio forte a composizionalità e program induction
- [Categories and Concepts — NYU (Lake)](formazione/nyu-categories-concepts-lake.md) — seminario sulla psicologia dei concetti; il dominio di cui il CCM dà i metodi, chiude sulla conceptual combination
- [Physical AI — mappa mondiale dei corsi](formazione/physical-ai-mappa-corsi.md)

**Prossime azioni** (dettaglio in [corsi.md §7](formazione/corsi.md)): mail a Garagnani · verifica che la carriera Master AI risulti chiusa · contatto con la Segreteria di Semiotica. Le ultime due maturano da sole, conviene avviarle subito.

---

## Lavori aperti

- [x] ~~Fondere le due bibliografie intensione/autonomia in un solo documento canonico~~
- [x] ~~Splittare `formazione-corsi-e-letture.md` e riconciliare i verdetti sui corsi UniBO~~
- [x] ~~Triare `inbox.md` verso i dossier tematici~~
- [x] ~~Progetto NEmo 2026: chiuso il 18 agosto 2026.~~ Le note bibliografiche sopravvissute sono in [scoperta-di-astrazioni-letteratura.md](argomenti/compressione-astrazione/scoperta-di-astrazioni-letteratura.md); il resto è recuperabile dalla storia di git
- [x] ~~Committare `topics/reasoning/` e `topics/content-drift/`~~
- [x] ~~Ristrutturare l'archivio: una domanda sola decide la cartella, i PDF stanno accanto alle note che li citano~~ — 3 settembre 2026
- [ ] **Riempire `lavori/`**: il Task 11 SemEval 2026 (NS-EDL) è citato come precedente in mezzo archivio e non ha una scheda; i workshop seguiti e i progetti software non ne hanno nessuna. È il buco più grande rimasto — [la convenzione è qui](lavori/README.md)
- [ ] Ruotare la password su nemo.semantic.review — è ancora nella storia di git
- [ ] Sostituire i redirect `lnkd.in` in [inbox.md](inbox.md) con gli URL reali
- [ ] Riscrivere [interpretability/bibliografia.md](argomenti/interpretability/bibliografia.md) — porta residui di conversazione (riga 124), il livello 0 è in coda invece che in testa, l'indice annuncia voci che non esistono
- [ ] Fondere [neurosimbolico-nlp.md](argomenti/reasoning/neurosimbolico-nlp.md) (appunti grezzi) nel nucleo K della [bibliografia reasoning](argomenti/reasoning/bibliografia-ragionata.md), che copre la stessa area meglio. Ora sono nella stessa cartella: manca solo il lavoro editoriale
- [ ] Portare nella [bibliografia intensione/autonomia](argomenti/intensione-autonomia/bibliografia.md) la tensione fra le due definizioni di autonomia — quella ingegneristica di Stuart Russell e Peter Norvig (indipendenza dalla conoscenza a priori) e quella epistemica di Peter Cariani (costruirsi nuovi sensori). Emersa confrontando [AAS](formazione/autonomous-adaptive-systems/) con l'argomento 2, non è scritta da nessuna parte
- [ ] Scegliere **una** convenzione di verifica delle citazioni: oggi convivono `[V]`/`[M]`, `✔`/`⚠` e nessuna. È l'annotazione che serve davvero sei mesi dopo

---

## Contatti

pamaldi@gmail.com · licenza MIT
