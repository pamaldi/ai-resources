# Compressione, ripetizione e scoperta autonoma di astrazioni

**Sintesi di conversazione — 31 luglio 2026**
Note di lavoro collegate al Progetto NEmo 2026. Filo conduttore: come un sistema possa passare autonomamente da una descrizione di livello *n* a una di livello *n+1*, e cosa serve perché ciò accada.

---

## 1. Progetto NEmo — le opzioni sul tavolo

### 1.1 Le due strade per la partecipazione

| | Short paper con early results | Position paper argomentativo |
|---|---|---|
| Formato | ≤ 4 pagine, CFP non-archival | ≤ 4 pagine, stessa categoria |
| Contenuto | toy minimale funzionante + metriche | tesi + letteratura + posizionamento del gap |
| Rischio | poco tempo per implementare | l'assenza dell'esperimento è un segnale negativo |

**Decisione**: la prima, tenendo l'apparato argomentativo della seconda come cornice. Anche il *fallimento pulito* della condizione senza gate di verifica è un risultato pubblicabile.

### 1.2 I due approcci implementativi

Stessa tesi (*la compressione è la value function, vincolata dalla correttezza verificata simbolicamente*), due vie. Cambia **chi propone e nomina la macro-azione**; il gate resta in entrambe.

**A — Neuro-simbolico con ASP.** Percezione → fatti simbolici → pianificazione clingo → logging tracce → rilevatore ripetizioni → anti-unificazione che propone e nomina il template → verifica con `#minimize` → libreria. Proponente = compressione simbolica. ILP a valle (Popper per la predicate invention, ILASP per raffinare). Per la ricorsione aritmetica pura conviene Prolog (in clingo il grounding esplode).

**B — LLM ad hoc** (filone Voyager / LILO). Proponente = LLM, che genera e nomina le skill; l'ambiente o un verificatore simbolico fa da gate; libreria online.

**Trade-off**: A è più ispezionabile e sfrutta il vantaggio comparativo sull'implementazione simbolica; B è più mainstream e regge meglio il taglio "self-evolving agents", ma espone all'obiezione che la verità la fa comunque il verificatore esterno.

---

## 2. Perché la moltiplicazione è conoscenza "superiore" all'addizione

Tre sensi distinti, più un caveat che è il vero punto.

- **Strutturale** — l'addizione opera su *oggetti* (quantità); la moltiplicazione opera *sull'addizione stessa* (`a×b = a + a×(b−1)`). Salto di livello logico: dal dominio degli oggetti a quello delle procedure. In miniatura è un `fold` sull'addizione — motivo per cui il DSL deve contenere fold/ricorsione.
- **Compressivo** — `4+4+4+4+4+4` cresce linearmente in `b`; `6×4` è di lunghezza costante. Non è solo notazione più corta: **il numero di ripetizioni diventa un parametro manipolabile**, cioè cittadino di prima classe. L'addizione ripetuta *contiene* quell'informazione ma non la *rappresenta*.
- **Generativo** — divisibilità, fattorizzazione, primi, potenze non esistono senza la moltiplicazione come oggetto. Ogni astrazione verificata apre il livello successivo (scala delle iperoperazioni).

**Caveat decisivo**: in senso *estensionale* la moltiplicazione sui naturali non aggiunge nulla — ogni prodotto è calcolabile per addizione ripetuta, la funzione è la stessa. La superiorità è tutta **intensionale**: sta nella rappresentazione, non nel contenuto denotato.

> Conseguenza operativa: una funzione obiettivo che guarda solo *cosa produce* l'ipotesi non può preferire `mult` all'addizione ripetuta. La distinzione va messa esplicitamente nell'obiettivo (lunghezza di descrizione, o costo computazionale).

Formula da paper: *la moltiplicazione non è conoscenza in più rispetto all'addizione, è conoscenza **sulla** addizione.*

---

## 3. Ancoraggi esterni valutati

### 3.1 Aldo Gangemi (UniBO) — tangente, ma politicamente rilevante

- **Anna Sofia Lippolis**, organizzatrice NEmo, è del suo gruppo. Utile sapere quale sensibilità leggerà il paper.
- **Ontology Design Patterns**: astrazioni riusabili, parametriche, catalogate — concettualmente il tema della libreria. Ma sono *elicitate da esperti umani*: sono il **prodotto** del processo che si vuole automatizzare. Il progetto è, in un senso, "ODP discovery dalla ripetizione comportamentale, con verifica".
- Linea recente LLM → ontologie da competency question: stessa grammatica architetturale della via B (neurale propone, verifica valida).
- **Non tocca**: MDL, predicate invention, skill discovery, genesi autonoma di simboli da tracce.
- **Uso**: un paragrafo nella sezione shared semantics. Non di più.

### 3.2 Max Garagnani (Goldsmiths / Pulvermüller) — legittimazione teorica

- Reti **brain-constrained**: connettività neuroanatomica, apprendimento hebbiano, aree corticali simulate. Dall'apprendimento emergono **cell assembly** distribuite ma *discrete*.
- È la stessa domanda della sezione "simbolizzazione dentro gli LLM", affrontata dal lato neuroscientifico, con risposta più ottimista: unità discrete possono emergere da substrato distribuito **purché i vincoli architetturali siano quelli giusti**.
- Parallelo utile: da loro il vincolo è la biologia, nel progetto è la verifica logica. Due modi di rispondere allo stesso problema — *l'apprendimento da solo non basta, serve qualcosa che vincoli*.
- Lavoro su grounding visuo-motorio con iCub → embodiment reale.
- **Non c'è**: compressione/MDL, ricorsione, composizionalità parametrica. Le cell assembly sono concetti *ancorati*, non macro procedurali con argomenti.
- **Uso**: 1-2 frasi in intro o future work sull'internalizzazione.

---

## 4. Neuroscienze della ripetizione

La ripetizione *è* documentata come stimolo alla formazione di nuove rappresentazioni. Tre filoni.

### 4.1 Chunking nei gangli della base — l'analogo più letterale

- **Graybiel (1998)**: la ricodifica corticale nello striato "chunka" sequenze d'azione perché siano eseguite come unità di performance. Generalizza il chunking di Miller al controllo dell'azione. Motivata esplicitamente da **compressione dell'informazione** e da un vincolo di costo biologico. *La tesi del progetto, formulata nel 1998.*
- **Task bracketing** (Jog et al. 1999; Barnes et al. 2005): nei ratti in un labirinto a T, l'attività striatale inizialmente distribuita collassa dopo l'apprendimento in un burst all'inizio e uno alla fine, con quasi silenzio in mezzo. La sequenza è stata *imparentesizzata* in un'unità.
- **Jin & Costa (2010; 2014)**: neuroni che codificano intere sequenze come singole azioni, più neuroni di start/stop che segnalano il parsing. È letteralmente `inizio(macro) … fine(macro)`.

### 4.2 Statistical learning e formazione di unità

- Esposizione ripetuta a co-occorrenze → gli elementi frequentemente co-occorrenti vengono trattati come **una singola unità**; evidenza di rappresentazione ippocampale.
- Dibattito rilevante: *modello statistico* (relazioni statistiche senza unità esplicite) vs *modelli a chunk* (unità discrete immagazzinate). È la versione neuroscientifica esatta di "la rete impara la tabella" vs "il sistema inventa l'operatore". Evidenza recente: rappresentazioni su più livelli simultaneamente.

### 4.3 Replay e gist abstraction — la ripetizione *offline*

- Modello **iOtA** (Lewis & Durrant 2011): il replay sovrapposto di memorie durante il sonno a onde lente produce astrazione delle componenti condivise (*gist*) e formazione di nuovi schemi.
- Le aree di sovrapposizione vengono rinforzate hebbianamente → si astraggono gli elementi invarianti (molte esperienze di "gatto" → il concetto di gatto). **Ed entrambe le forme di astrazione permettono compressione**, perché la codifica condivisa è più compatta.
- È DreamCoder in versione biologica; la fase *sleep* del wake-sleep non è metafora casuale.

### 4.4 Il caveat, che è anche il gap

Tutta questa letteratura documenta **chunk**: unità concatenate, eseguibili in blocco, più economiche. Nessuna mostra:

- **parametrizzazione** — il chunk striatale è una sequenza fissa, non `riempi_scatola(S, O, Q)`
- **verifica** — il chunking è irreversibile e non certificato: produce anche abitudini sbagliate, rituali, compulsioni. *È il fallimento della compressione senza gate.*

Il livello 1 (`a+a → double`) ha solido substrato neurale. Il livello 2 (astrazione del *numero di ripetizioni*) no.

---

## 5. La vespa Sphex — il controesempio perfetto

- **La storia** (Wooldridge 1963, ripresa da Hofstadter): la vespa trascina il grillo alla soglia, entra a ispezionare, esce, lo tira dentro. Se si sposta il grillo di qualche centimetro mentre è dentro, ricomincia l'intera procedura. In un'occasione ripetuta **quaranta volte**.
- **La diagnosi di Hofstadter in GEB**: nel cervello della vespa ci sono simboli rudimentali che si attivano a vicenda, ma manca la capacità di vedere più istanze *come istanze* di una classe non ancora formata. Da qui *sphexishness* / *antisphexishness*.
- **Perché serve**: la vespa esegue quaranta ripetizioni identiche e **non le vede come ripetizioni**. Non ha noia, non ha compressione. Ha simboli che si concatenano, non simboli su cui si può salire di livello.
- **Simmetria con Graybiel**: la vespa **è già un chunk** — macro-azione biologica compilata, con start/stop. Ha il livello 1 e nient'altro. *Il chunking non è sufficiente: la natura lo fa da centinaia di milioni di anni e produce vespe.*
- **Caveat prima di citarla**: Keijzer (2013) ricostruisce come l'aneddoto sia stato ripetuto acriticamente per decenni; Wooldridge non era un biologo; i dati entomologici mostrano più variabilità. Dennett stesso ha poi ammesso che il resoconto è semplificato.
- **Uso corretto**: presentarla come **parabola, non come dato empirico**. L'ironia (la comunità cognitiva ha ripetuto quaranta volte la storia della vespa che ripete quaranta volte) trasforma l'obiezione in ornamento.

---

## 6. Il trigger: perché "bassa entropia" non basta

L'ipotesi iniziale — *bassa entropia → scarsa informazione → scatta a livello più alto* — ha un difetto fatale:

- l'entropia **minima** è la traccia costante: non c'è niente da astrarre, ottieni una costante, non una funzione
- **una lookup table memorizzata ha entropia bassissima** → il criterio autorizza la memorizzazione

### Dove sta davvero il segnale

```
3+3+3+3+3      elemento=3, conteggio=5
4+4+4+4+4+4    elemento=4, conteggio=6
9+9            elemento=9, conteggio=2
```

L'entropia è bassa **lungo una dimensione** (l'operatore è sempre `+`, l'operando è costante dentro ogni traccia) e alta **lungo un'altra** (elemento e conteggio variano tra tracce). L'astrazione nasce sul confine:

- **invariante → struttura** (il `+`, la forma "somma di copie identiche")
- **variabile → parametro** (`a`, `b`)

> Il trigger non è "poca informazione", è **"molta struttura ripetuta con poche dimensioni di variazione"**.

### Formulazione operativa

```
gain(T) = Σ_episodi_coperti [ len(ep) − len(ep con T) ] − size(definizione di T)
```

Una lookup table fa esplodere `size(definizione)` linearmente → guadagno nullo. **L'MDL fatto bene contiene già la difesa contro la memorizzazione.** (Schmidhuber: la reward non è la compressione, è il *progresso* di compressione — una derivata.)

### Architettura a due stadi

1. **stadio economico** — proxy di comprimibilità su finestra scorrevole (entropy rate, o rapporto `zlib`). O(n), gira sempre.
2. **stadio costoso** — sopra soglia: suffix automaton / merging BPE-style, anti-unificazione, nome fresco, verifica.

> *L'entropia dice dove guardare, la compressione dice cosa proporre, la logica dice cosa tenere.*

---

## 7. MDL — Minimum Description Length

### 7.1 L'idea

La migliore ipotesi è quella che permette di descrivere i dati nel modo più breve possibile, **contando anche la lunghezza dell'ipotesi stessa**.

```
minimizza  L(H) + L(D | H)
```

Gioco del trasmettitore: mandi prima la regola, poi i dati codificati assumendo che il ricevitore la conosca. **Compressione lossless** — l'ipotesi non sostituisce i dati, li aiuta solo a comprimersi; i residui vanno pagati.

### 7.2 Il ponte codici ↔ probabilità

`L(x) = −log₂ P(x)` (Kraft, Shannon). Corrispondenza biunivoca: ogni codice definisce una distribuzione e viceversa. **"Più corto" e "più probabile" sono sinonimi.** MDL non è Occam per gusto estetico: è teoria dell'informazione.

### 7.3 Esempio numerico (10.000 lanci, 9.000 teste)

| Ipotesi | L(H) | L(D\|H) | Totale |
|---|---|---|---|
| A — moneta equa | ~1 bit | 10.000 | ~10.001 |
| B — moneta sbilanciata, `p` da specificare | ~7 bit | 4.690 | **~4.697** |
| C — memorizzazione della sequenza | 10.000 | 0 | 10.000 |

C fitta perfettamente e non guadagna nulla: ha solo spostato il costo di tasca. **MDL è immune alla memorizzazione per costruzione.** È questo che lo distingue dalla "compressione" intesa come "far diventare piccolo il secondo termine".

### 7.4 La curva a U

Sinistra = underfitting (`L(D|H)` enorme); destra = overfitting (`L(H)` esploso). Il minimo sta in mezzo. **L'overfitting emerge senza test set, senza cross-validation, senza teoria statistica della generalizzazione** — solo contando bit sui dati che già possiedi.

### 7.5 Kolmogorov, MDL raffinata, Bayes

- **Kolmogorov** `K(x)`: lunghezza del programma più corto che produce `x`. Ottimo assoluto, ma **incalcolabile**. MDL è la ritirata pragmatica: si sostituisce "tutti i programmi" con "una classe di modelli scelta da te".
- **Il problema di `L(H)`**: come codifichi l'ipotesi? Cambiando codifica cambia il vincitore → la versione a due parti è in parte convenzionale.
- **MDL raffinata** (Rissanen 1996): si abbandona la separazione in due pezzi. Codice **NML** / *stochastic complexity*: al fit migliore si somma la **complessità parametrica**, che misura quanto la classe è *capace di adattarsi a qualunque cosa* (somma su tutti i dataset). Proprietà minimax sul regret. Asintoticamente `≈ (k/2)·log n` → **è la penalità del BIC**, che risulta quindi un'approssimazione di MDL. (AIC no: altra logica, divergenza KL attesa.)
- **Bayes**: `min[−log P(H) − log P(D|H)]` ⟺ `max P(H)·P(D|H)`. È **esattamente il MAP**; il codice sull'ipotesi *è* il prior. Differenze filosofiche: MDL non richiede una "vera distribuzione" nella classe → più robusto sotto misspecification, ma non dà posterior né quantificazione dell'incertezza.

### 7.6 I limiti veri

1. **MDL non sceglie il linguaggio, lo eredita.** Trova la migliore ipotesi *esprimibile*. Se la struttura vera non è dicibile, seleziona serenamente il miglior modello sbagliato. È il no-free-lunch che rientra dalla finestra.
2. **Comprimere non è spiegare.** Un modello che comprime bene può essere causalmente assurdo.
3. **Il minimo non lo trovi**: NP-hard o peggio su classi ricche → euristiche greedy, garanzie evaporate.
4. **NML spesso non esiste**: la somma diverge per molte famiglie comuni (serve NML condizionale/ristretta).

---

## 8. Come si spendono davvero i bit

### 8.1 Il paradosso dei bit frazionari

Con `P(T)=0.9` il costo ottimale è `−log₂(0.9) = 0.152` bit per testa. Ma i bit sono interi e **Huffman su alfabeto binario non può scendere sotto 1 bit/simbolo**.

- **Raggruppamento**: coppie → 0.645 bit/simbolo; terne → 0.533; converge verso l'entropia 0.469 senza mai raggiungerla, e la tabella raddoppia a ogni passo.
- **Codifica aritmetica**: si smette di assegnare un codice a ciascun simbolo. Si assegna **un unico numero all'intero messaggio**, restringendo `[0,1)` un simbolo alla volta.

Esempio `TTCT` con `p=0.9`:

```
inizio    [0      , 1      )   ampiezza 1
T         [0      , 0.9    )   0.9
T         [0      , 0.81   )   0.81
C         [0.729  , 0.81   )   0.081
T         [0.729  , 0.8019 )   0.0729
```

**L'ampiezza finale è esattamente `P(messaggio)` = 0.9·0.9·0.1·0.9 = 0.0729.** Si trasmette un numero binario dentro l'intervallo: `0.75 = 0.11₂` → messaggio `11`, **2 bit**.

Da cui, in un colpo solo:

```
bit necessari = −log₂( P(messaggio) )
```

I bit frazionari **non esistono a livello di simbolo; esistono come costo marginale ammortizzato sull'intero messaggio**. Huffman deve chiudere il conto a ogni simbolo, l'aritmetica una volta sola.

> Chiusura del cerchio con MDL: il ricevitore deve *sapere* che `p = 0.9`. Quel costo è `L(H)`. **La codifica aritmetica quantifica il secondo termine; il primo è il prezzo del biglietto per poterla usare.**

### 8.2 Elias-Fano — l'altra famiglia

Cambio di paradigma: da **entropico** a **succinto/combinatorio**. (Da non confondere con i codici di Elias γ/δ, che sono per interi singoli.)

- **Problema**: `n` interi crescenti da `[0, u)` — posting list, indici invertiti.
- **Limite informativo**: `log₂ C(u,n) ≈ n·log₂(u/n) + 1.44n`. **È un conteggio, non un'entropia** — codice uniforme sulla classe combinatoria (stesso spirito della complessità parametrica NML).
- **Elias-Fano**: `n·⌈log₂(u/n)⌉ + 2n` bit → entro ~mezzo bit/elemento dall'ottimo ("quasi-succinto").
- **Meccanismo**: ogni intero si spezza in `ℓ = ⌊log₂(u/n)⌋` bit bassi (scritti in chiaro, incomprimibili) e bit alti (quasi ridondanti per monotonia, scritti in **unario per bucket**: tanti `1` quanti elementi, poi uno `0`). I `2^h ≈ n` bucket producono `n` zeri + `n` uni = `2n` bit, **indipendentemente da quanto è grande l'universo**.
- **La vera ragione d'essere**: `accedi(i)` in **O(1)** via `select₁`, e query di successore veloci — cioè intersezione di posting list. L'aritmetica è un flusso, Elias-Fano è una struttura dati.

| | Codifica aritmetica | Elias-Fano |
|---|---|---|
| Assume | modello probabilistico | solo monotonia |
| Ottimale rispetto a | entropia | conteggio `log C(u,n)` |
| Distanza dall'ottimo | ~0 | ~0.5 bit/elemento |
| Accesso a un elemento | O(n) sequenziale | O(1) |

> Il mezzo bit buttato via **è il prezzo della navigabilità**. Tema ricorrente nelle strutture succinte: si rinuncia all'ottimo entropico per interrogare i dati senza decomprimerli.

---

## 9. Automi cellulari — cosa c'è, e cosa manca

### 9.1 Computational mechanics (Crutchfield & Hanson)

Esiste un campo intero che è la stessa domanda applicata ai CA.

- **Domini regolari**: regioni spaziotemporali che sono (i) linguaggio regolare e (ii) invarianti per traslazione spaziale e temporale. Sono ripetizione pura = informazione zero.
- **La mossa**: si costruisce un **filtro che cancella il dominio**. Ciò che resta sono le **particelle** — strutture localizzate che si propagano e collidono, e che sono il meccanismo primario di trasporto dell'informazione.
- Su ECA 54: dominio dominante, filtro, difetti classificati, particelle primarie, interazioni, fino all'**equazione del moto del comportamento filtrato**.
- *Comprimi via il ripetitivo e ciò che resta è il livello superiore* — ma qui il livello superiore è un'**ontologia di oggetti** con una loro dinamica.

### 9.2 ε-machine reconstruction

- La scoperta del dominio è **automatica**: ricostruzione dell'ε-machine, che raggruppa le storie passate in classi di equivalenza (due passati equivalenti se implicano la stessa distribuzione di futuri).
- **Tre teoremi di ottimalità**: l'ε-machine è il predittore ottimale, è minimale tra i predittori ottimali, ed è unica. **È MDL con garanzia** — non "il più corto nel mio DSL" ma *il* modello minimo sufficiente.
- **Complessità statistica `C_μ`** = dimensione del modello. Il rumore puro ha entropia massima e `C_μ` quasi nulla; l'ordine perfetto ha entrambe basse; la complessità pica in mezzo. **Separa casualità da struttura**, che l'entropia da sola confonde.
- Versione moderna: **stati causali locali** (coni di luce passati/futuri) → filtri non supervisionati che rivelano domini e particelle senza template forniti a mano.
- Risultato collaterale: limite superiore rigoroso al numero di prodotti delle interazioni tra particelle, controllato dalla **complessità strutturale** delle particelle.

### 9.3 Israeli & Goldenfeld — coarse-graining come salto di livello

- Coarse-graining di CA in **tutte** le classi di Wolfram: processi computazionalmente irriducibili possono essere **predicibili e riducibili a un livello di descrizione grossolano**.
- Metodo: gruppo di rinormalizzazione con condizione di autoconsistenza (coarse-grain + nuove leggi ≡ leggi micro + coarse-grain).
- **240 delle 256 regole ECA** sono state coarse-grained, molte su altre regole ECA; **la complessità non aumenta mai** sotto coarse-graining → ordinamento parziale tra regole.
- Caso spettacolare: **rule 110** (universale) diventa un sistema semplice e predicibile alla scala grossolana.
- *La dimostrazione più pulita che la scelta del livello di descrizione, non la potenza di calcolo, è ciò che rende un sistema comprensibile.*

### 9.4 Il contributo negativo — irriducibilità computazionale

- Wolfram: molte domande sull'evoluzione di un CA **non possono essere scorciate** senza seguire il calcolo nel dettaglio. **Per alcuni sistemi la macro non esiste.**
- **Rule 30**: `K` ridicolmente piccola (8 bit di regola), output che supera i test di casualità e che **nessun compressore reale comprime**. Divario tra Kolmogorov e compressione praticabile → *l'esistenza di una compressione non implica la trovabilità della compressione.*
- Limite attuale del campo: generare le classi di equivalenza a partire dalla **sola regola** resta un problema aperto; l'unico modo noto è simulare a forza bruta e ricostruire.

### 9.5 Compressione come classificatore

Zenil (2010): il semplice **rapporto di compressione del diagramma spaziotemporale** riproduce automaticamente la classificazione di Wolfram. Classi I-II comprimono, III no, IV in mezzo.

### 9.6 La critica: non è apprendimento

**Manca l'anello.** La computational mechanics è **analisi**, non apprendimento. Chi scopre le particelle è lo scienziato che guarda il CA; la regola 54 continua a girare identica, ignara. Tre assenze:

1. **il loop** — l'astrazione non modifica il comportamento futuro
2. **il costo sostenuto dallo scopritore** — l'osservatore ha un incentivo a comprimere, l'automa no
3. **la riusabilità come primitiva** — la particella α non diventa un mattone per il livello successivo

C'è *compressione*, non c'è *agente* né *value function*.

**Ma**: la ricostruzione dell'ε-machine (CSSR) **è** apprendimento non supervisionato di struttura, con teoremi di ottimalità. Formula esatta: **c'è apprendimento di rappresentazioni, non c'è apprendimento agentico.** Un osservatore impara; nessuno agisce.

Caso ibrido: *evolving cellular automata* (Crutchfield & Mitchell) — un GA evolve regole per un compito globale, e le soluzioni implementano la strategia via interazioni tra particelle. Ma il GA impara *la regola*, l'analista scopre *le particelle*: l'anello resta aperto.

**Cosa resta di trasferibile**:
- una definizione formale di "qui non c'è niente da imparare" (il dominio regolare: criterio decidibile, non una soglia scelta a mano)
- una nozione di minimalità *con garanzia* (l'ε-machine risolve l'arbitrarietà della classe di modelli, che è il limite principale di MDL)
- un limite superiore all'intera impresa (esistono processi dove il fallimento non è dell'algoritmo ma del mondo)

---

## 10. HashLife — l'unico posto dove il cerchio si chiude

Gosper (1984). Fa **due cose diverse** che spesso vengono confuse in una.

### 10.1 Compressione spaziale — quadtree con hash consing

Un nodo di livello `n` rappresenta un quadrato `2ⁿ × 2ⁿ` con quattro figli di livello `n−1`. I nodi sono **canonicalizzati via hash**: prima di crearne uno si cerca se esiste già con quegli stessi figli. Conseguenza: **due regioni identiche, ovunque si trovino, sono lo stesso oggetto in memoria.** L'albero diventa un DAG; il fattore di compressione può essere astronomico.

### 10.2 Compressione temporale — il risultato memoizzato

```
result(nodo livello n) → il quadrato centrale 2ⁿ⁻¹ × 2ⁿ⁻¹, avanzato di 2ⁿ⁻² generazioni
```

**Perché il centro e perché quel numero di generazioni**: cono di luce. L'informazione viaggia a 1 cella/generazione, quindi da un blocco `2ⁿ` si perde una cella di bordo per lato a ogni passo. Dopo `2ⁿ⁻²` passi resta esattamente il quadrante centrale: `2ⁿ − 2·2ⁿ⁻² = 2ⁿ⁻¹`. La definizione è costruita per far coincidere il **massimo salto temporale sicuro** con il quadrato centrale.

`result()` è **messo in cache sul nodo**. Siccome i nodi sono canonicalizzati, la stessa configurazione — altrove nello spazio, o mille generazioni dopo — è lo stesso nodo, e il risultato è già lì.

**Ricorsione**: dai 16 nipoti si ricavano 9 sotto-quadrati sovrapposti di livello `n−1`, se ne prende il `result` (avanzano `2ⁿ⁻³`), si riassemblano in 4 quadrati, altro `result` (altre `2ⁿ⁻³`). Totale `2ⁿ⁻²`. Caso base: livello 2 → centro `2×2` avanzato di 1, dalla regola di Life.

### 10.3 Il risultato

**Salendo di un livello, il passo temporale raddoppia.** Un nodo di livello 40 avanza di 2³⁸ generazioni in una chiamata. Il tempo di calcolo cresce **logaritmicamente** nel numero di generazioni: Golly porta pattern noti oltre la generazione 2¹⁰⁰ in secondi, con risultato **esatto**.

**Quando fallisce**: sul caos. Una soup casuale non riproduce mai lo stesso blocco → cache miss continui, memoria esplosa, più lento della simulazione ingenua. *HashLife è veloce esattamente sui pattern comprimibili: il suo profilo di prestazioni è una misura di regolarità.*

### 10.4 Perché conta per il progetto

| Requisito | HashLife |
|---|---|
| rileva ripetizione | ✅ hash consing |
| crea astrazione nominata | ✅ nodo canonico, hash come nome |
| verifica | ✅ gratuita e perfetta (identità strutturale) |
| riusa, e il riuso ripaga | ✅ speedup superlineare misurabile |
| gerarchia | ✅ nodi di nodi, portata raddoppiata a ogni livello |
| **parametrizzazione** | ❌ |

Il nodo `X` funziona solo per la configurazione esatta `X`. Nessun trasferimento a casi simili-ma-diversi. **È la lookup table perfetta** — quella che MDL punisce, e che qui non viene punita solo perché `L(H)` non conta (memoria trattata come gratuita).

> HashLife scopre `double`, `triple`, …, fino a `2⁶⁴-uple`, ognuno memorizzato separatamente. **Non scopre mai la moltiplicazione.** Ed è velocissimo proprio perché non ci prova.

Diagnosi generale: nei CA si trova il **criterio** di astrazione in forma matematicamente impeccabile, e il **loop** solo nella sua forma più degenerata. Le due metà del problema, mai nella stessa stanza.

---

## 11. Cosa serve davvero per scoprire la moltiplicazione

**Premessa che ribalta la domanda**: la funzione obiettivo è la parte facile. HashLife ha un obiettivo perfetto (minimizza il tempo, in modo esatto e misurabile) e non ci arriverà mai — perché nel suo linguaggio `mult` **non è dicibile**.

### 11.1 Il linguaggio (necessario, e decisivo)

Servono due cose:
- **variabili**, perché l'elemento ripetuto sia astraibile
- **un combinatore ricorsivo** (`fold`, `iterate`, ricorsione) perché sia astraibile **il numero di ripetizioni**

Il secondo è quello che tutti sottovalutano. Senza fold, `double/triple/quadruple` sono programmi separati e brevi, ma la famiglia infinita non ha nome.

> **Verità scomoda**: se dai il fold, `mult(a,b) = if b=0 then 0 else a + mult(a,b−1)` costa poche decine di bit e un sistema alla DreamCoder la trova senza fatica. **Il progettista che sceglie i primitivi sta facendo metà del lavoro induttivo** — e va dichiarato, non lasciato scoprire al revisore.

### 11.2 La funzione obiettivo

```
J(H) = ω·errori(H)                     ← vincolo duro
     + λ·|H|                           ← costo della libreria       L(H)
     + μ·Σ_task |codifica(task | H)|   ← costo dei dati             L(D|H)
     + ν·Σ_task log(passi(task | H))   ← costo computazionale
     − γ·copertura_su_holdout(H)       ← generalizzazione
```

**`λ·|H|` uccide la lookup table**:

| Ipotesi | `L(H)` | `L(D\|H)` per task | Copre |
|---|---|---|---|
| tabella memorizzata | O(N) | ~0 | solo il visto |
| famiglia `double, triple, …` | O(K) | costante | tutti gli `a`, solo i `b` visti |
| `mult` con fold | **O(1)** | costante | tutto |

**`ν·log(passi)` è il termine spesso mancante e più interessante.** Sui naturali `mult` e l'addizione ripetuta calcolano la stessa funzione: estensionalmente indistinguibili. La distinzione è intensionale → va messa nell'obiettivo esplicitamente (lunghezza di descrizione, o costo di esecuzione — *complessità di Levin* / *speed prior*).

*Sottigliezza*: `mult` ricorsiva **non è più veloce** dell'addizione ripetuta (gira comunque in O(b)). Il risparmio computazionale arriva solo se l'operazione viene poi **compilata in primitiva** (hardware, lookup, skill motoria appresa). In pianificazione è naturale — `mult(6,4)` è una azione contro 24 primitive. In aritmetica pura il guadagno è tutto descrittivo finché non c'è internalizzazione.

**`γ·copertura_su_holdout` è il gate.** MDL protegge dalla memorizzazione *sui dati visti*, non garantisce nulla su `b` mai incontrati. Serve un criterio esterno: holdout, prova simbolica, o un ambiente che punisce gli errori.

### 11.3 Le condizioni sui dati (la parte che nessuno menziona)

> **L'ambiente deve variare lungo la dimensione che si vuole astrarre.**

Se il sistema vede solo `3+3`, `7+7`, `11+11`, allora `double` è **l'ipotesi MDL ottimale** e `mult` è overfitting — paghi il fold per una generalità mai usata. Serve `3+3`, `4+4+4+4+4`, `9+9+9`. **È la variazione a rendere la dimensione visibile.**

Ragione strutturale del fallimento di HashLife: il suo mondo è pieno di ripetizione, ma **identica, mai parametrica**. Cache hit perfetti, zero variazione da astrarre.

### 11.4 Il salto tecnicamente più duro: dal livello 1 al livello 2

L'anti-unificazione classica (Plotkin) è del **primo ordine**: da `+(3,+(3,3))` e `+(4,+(4,4))` ottieni `+(X,+(X,X))` = `triple(X)`. Ma da `double` e `triple` **non ottieni `mult`**: hanno struttura sintattica e profondità diverse, e l'anti-unificazione del primo ordine generalizza sui *sottotermini*, non sulla *profondità*.

Opzioni:
- **anti-unificazione di ordine superiore** (in generale indecidibile; le forme ristrette tipo pattern di Miller funzionano)
- **riconoscere che la famiglia è indicizzata da un intero** e proporre il fold come ipotesi strutturale — bias mirato, meno elegante ma pratico
- **e-graph / equality saturation**: le riscritture equivalenti si accumulano in una struttura condivisa e l'estrazione del programma minimo diventa ottimizzazione trattabile

Serve inoltre un **curriculum**: `double` scoperto prima e messo in libreria abbassa il costo di `mult` al giro successivo (ciclo wake-sleep di DreamCoder). Senza incrementalità lo spazio di ricerca è troppo grande perché il fold venga mai proposto.

### 11.5 Ordine di importanza

1. **il linguaggio** — senza fold non c'è niente da fare
2. **i dati** — se il conteggio non varia, la generalizzazione è ingiustificata (e correttamente rifiutata)
3. **l'obiettivo** — MDL + correttezza + costo computazionale + verifica su non visti
4. **la ricerca** — dove si consuma il 90% della fatica ingegneristica

---

## 12. Linguaggio e funzione obiettivo — il livello generale

### 12.1 La distinzione

**Il linguaggio non serve a esprimere la funzione obiettivo. Serve a definire lo spazio su cui la funzione obiettivo è definita.**

- il **DSL** stabilisce *cosa è pensabile*
- la **funzione obiettivo** è una funzione *su* quell'insieme, e vive un livello sopra (nel motore di ricerca, non nel DSL)

Metafora: il linguaggio è il terreno, l'obiettivo è la quota.

### 12.2 Il punto di contatto

`L(H) = lunghezza della descrizione di H nel linguaggio scelto`. Quindi il linguaggio non definisce solo *cosa* è esprimibile ma **quanto costa**. Stessa `J(H)`, due DSL:

- senza fold → il minimo è la famiglia `double, triple, …`
- con fold → il minimo si sposta su `mult`

L'obiettivo è identico: **è il terreno che si è deformato**. Il linguaggio è *metà* della funzione obiettivo, pur non contenendola.

### 12.3 Il minimo indispensabile, in generale

Per una funzione obiettivo servono solo:
1. **un insieme** di alternative distinguibili
2. **un ordinamento** (anche parziale, anche senza numeri)

Per l'apprendimento, aggiungi **un modo di spostarsi** (mutazione, gradiente, enumerazione). Il linguaggio è un'implementazione del primo elemento, non un requisito.

### 12.4 L'obiettivo può non essere espresso da nessuna parte

Può essere **implicito nella dinamica**. La fitness evolutiva non è scritta da nessuna parte: alcuni si riproducono e altri no, e la "ottimizzazione" è la nostra ricostruzione a posteriori. Stesso schema: la goccia sferica, il mercato, il bias implicito di SGD.

E l'evoluzione **scopre astrazioni** — modularità, piani corporei riusati, reti di regolazione gerarchiche, l'occhio inventato decine di volte — senza linguaggio, senza obiettivo esplicito, senza sapere cosa sta facendo.

> **Linguaggio: no. Preferenza differenziale su alternative: sì, sempre.**

### 12.5 Tre modi in cui un obiettivo può esistere

| | Dove sta | Esempi |
|---|---|---|
| **implicito** | nella dinamica; nessuno lo scrive | evoluzione, fisica, mercati |
| **esterno** | in un metalinguaggio che il sistema non conosce | quasi tutto il ML |
| **interno** | nello stesso linguaggio delle ipotesi → manipolabile | sistemi riflessivi, Gödel machine |

Solo nel terzo caso il sistema **può cambiare il proprio criterio** — e lì il linguaggio autoreferenziale diventa necessario. (La Gödel machine: teoricamente ottimale, praticamente inservibile, perché le dimostrazioni richieste sono fuori portata.)

### 12.6 Cosa compra il linguaggio

- **produttività** — infinite ipotesi da primitivi finiti
- **sistematicità** — se puoi pensare `aRb` puoi pensare `bRa`
- **sostituzione salva** — sostituisci una variabile con qualunque valore e la correttezza tiene; *è questo che rende un'astrazione trasferibile a casi mai visti*
- **compressione strutturale** — le parti condivise si nominano una volta
- **verificabilità** — puoi dimostrare qualcosa *sull'ipotesi*, non solo testarla
- **trasmissibilità** — un altro agente riceve l'astrazione senza rifare la scoperta
- **autoriferimento**

Prezzo: ricerca dura (niente gradienti), e primitivi scelti a mano.

### 12.7 Il principio invariante

> **Il bias induttivo non si elimina, si sposta.**

Tre contenitori intercambiabili:
- lo **spazio delle ipotesi** (certe cose non sono dicibili)
- l'**obiettivo** (dicibili ma costose)
- la **ricerca** (dicibili ed economiche, ma non le trovi mai)

CNN → architettura; bayesiano → prior; enumeratore → ordine di esplorazione. Puoi travasare, il volume resta. **Il linguaggio è semplicemente il contenitore più leggibile**: l'unico in cui puoi *guardare* il tuo bias e dichiararlo.

---

## 13. René Thom — la domanda sotto tutte le altre

### 13.1 Cosa dice

Medaglia Fields 1958 (trasversalità), poi *Stabilité structurelle et morphogenèse* (1972). La domanda: **da dove vengono le forme discrete in un mondo continuo?**

Un sistema è governato da un potenziale liscio dipendente da parametri di controllo. Al variare dei parametri il minimo si sposta con continuità finché non scompare; lì lo stato **salta**. La discontinuità è emergente da una dinamica continua.

**Teorema di classificazione**: per ≤ 4 parametri di controllo le biforcazioni possibili sono **sette** (piega, cuspide, coda di rondine, farfalla, ombelicali ellittico/iperbolico/parabolico). Non "in pratica": sette per ragioni topologiche, a meno di diffeomorfismi. Un catalogo chiuso dei modi in cui il continuo genera il discreto.

Ambizione semantica: le catastrofi come **archetipi morfologici** — morfogenesi, percezione, e (l'ultimo Thom) strutture predicative del linguaggio. Da lì la semantica cognitiva di Petitot e Zeeman.

### 13.2 Perché aggancia

Restava aperta la domanda: **da dove vengono le alternative?** Thom dà l'unica risposta di questa conversazione: le alternative discrete non si postulano — **emergono come regioni di stabilità strutturale di una dinamica continua**. Un simbolo è una zona dello spazio dei parametri dove il comportamento qualitativo è invariante sotto piccola perturbazione; il confine tra due simboli è una catastrofe.

**È la genesi dell'alfabeto** — il pezzo che manca sia a MDL (che riceve il DSL già fatto) sia alla computational mechanics (che riceve l'alfabeto del CA già discreto).

E la stabilità strutturale è un criterio di compressione: **una forma è quella che resiste alla perturbazione**. Non la configurazione più probabile, ma quella la cui *classe qualitativa* è robusta — un modo diverso, e più profondo, di dire "generalizza".

Antenato della "noia": la dinamica lenta e liscia non produce niente; l'evento è la **biforcazione**. Il salto di livello coincide con un cambio di regime.

### 13.3 Perché non lo usa nessuno

Boom negli anni '70 (soprattutto per la divulgazione di Zeeman: aggressione animale, rivolte carcerarie, anoressia, mercati), poi **crollo di reputazione**. L'attacco decisivo di **Sussmann & Zahler (1978)**: nelle applicazioni alle scienze umane il modello è essenzialmente non falsificabile (se osservi un salto dici "cuspide", se non lo osservi dici "parametri sbagliati").

Verdetto storico: **la matematica è impeccabile** (oggi materia standard di teoria delle biforcazioni e delle singolarità); **le applicazioni fuori da fisica e ottica erano metafora presentata come modello**. Thom stesso era abbastanza esplicito sul fare *intelligibilità* e non predizione.

**Non c'è algoritmo.** Da un ε-machine ricostruisci una macchina; da una catastrofe non ottieni nulla di eseguibile.

### 13.4 Come usarlo

- ✅ **La domanda**: "da dove viene l'alfabeto" resta la migliore eredità. Chi decide che le primitive sono `afferra, sposta, deposita`? MDL comincia a lavorare *dopo* che qualcuno ha risposto.
- ✅ **La discendenza tecnica viva**: teoria delle biforcazioni, e soprattutto la **teoria delle transizioni critiche** (Scheffer et al.) con gli *early warning signals* — rallentamento critico, aumento di varianza e autocorrelazione prima di un salto di regime. Testabile, quantitativa, usata in ecologia/clima/epidemiologia. **Thom depurato dalle pretese semantiche.** Se servisse un detector di cambio di regime, è lì che guardare.
- ❌ **Citarlo per profondità filosofica**: un revisore che conosce la storia lo legge come segnale negativo.

*Ironia*: Thom era ferocemente antiriduzionista e osteggiava l'approccio computazionale alla biologia. Avrebbe detestato l'intero programma di cui si è parlato.

---

## 14. Fili conduttori

1. **La compressione da sola trova gli shortcut sbagliati.** La lookup table è compressione. Serve un secondo criterio: MDL fatto bene (che conta `L(H)`), la verifica, o entrambi.
2. **Chunking ≠ astrazione.** Il chunking (biologico, HashLife, memoizzazione) produce unità fisse ed è ubiquo. L'astrazione richiede **parametrizzazione**, cioè una variabile dove prima c'era una costante. Nessun sistema arriva al secondo per il solo fatto di essere bravo al primo.
3. **L'astrazione vive sul confine invariante/variabile.** Ciò che non cambia diventa struttura, ciò che cambia diventa parametro. Da cui: **l'ambiente deve variare lungo la dimensione che si vuole astrarre**, o la generalizzazione è ingiustificata.
4. **La superiorità di un livello è intensionale, non estensionale.** Stessa funzione calcolata, rappresentazione diversa. L'obiettivo deve saper vedere la differenza, o non la vedrà.
5. **Il bias induttivo non si elimina, si sposta** — linguaggio, obiettivo, ricerca. Il linguaggio è il contenitore più onesto perché è ispezionabile.
6. **Esistono processi senza scorciatoia.** L'irriducibilità computazionale è un limite reale a qualunque programma di scoperta autonoma di astrazioni.
7. **La sostituzione salva è la proprietà che conta.** Non "il simbolo" come feticcio: la garanzia che sostituendo una variabile con qualunque valore il comportamento resti corretto. È l'unica cosa che rende un'astrazione trasferibile — e per ora il formalismo simbolico è l'unico modo noto di ottenerla insieme alla verificabilità.

---

## Riferimenti

### MDL, complessità, teoria dell'informazione

- Rissanen, J. (1978). *Modeling by shortest data description*. Automatica 14(5):465–471.
- Rissanen, J. (1996). *Fisher information and stochastic complexity*. IEEE Trans. Information Theory 42(1):40–47.
- Grünwald, P. (2007). *The Minimum Description Length Principle*. MIT Press. — **testo di riferimento**
- Li, M. & Vitányi, P. (2019). *An Introduction to Kolmogorov Complexity and Its Applications*. 4ª ed., Springer.
- Shannon, C.E. (1948). *A Mathematical Theory of Communication*. Bell System Technical Journal.
- Levin, L. (1973). *Universal sequential search problems*. — complessità di Levin.
- Schmidhuber, J. (2002). *The Speed Prior: A New Simplicity Measure Yielding Near-Optimal Computable Predictions*. COLT.

### Codifica

- Witten, I.H., Neal, R.M., Cleary, J.G. (1987). *Arithmetic coding for data compression*. CACM 30(6):520–540.
- Elias, P. (1974). *Efficient storage and retrieval by content and address of static files*. JACM 21(2).
- Vigna, S. (2013). *Quasi-succinct indices*. WSDM '13.
- Ottaviano, G. & Venturini, R. (2014). *Partitioned Elias-Fano indexes*. SIGIR '14.

### Library learning, program synthesis, ILP

- Ellis, K. et al. (2021). *DreamCoder: bootstrapping inductive program synthesis with wake-sleep library learning*. PLDI.
- Bowers, M. et al. (2023). *Top-down synthesis for library learning* (Stitch). POPL.
- Grand, G., Wong, L. et al. (2024). *LILO: Learning Interpretable Libraries by Compressing and Documenting Code*. ICLR.
- Wang, G. et al. (2023). *Voyager: An Open-Ended Embodied Agent with Large Language Models*. arXiv:2305.16291.
- Plotkin, G.D. (1970). *A note on inductive generalization*. Machine Intelligence 5. — anti-unificazione
- Cropper, A. & Morel, R. (2021). *Learning programs by learning from failures* (Popper). Machine Learning 110.
- Willsey, M. et al. (2021). *egg: Fast and extensible equality saturation*. POPL.
- Lee, N. et al. (2025). *Self-Improving Transformers Overcome Easy-to-Hard and Length Generalization Challenges*. arXiv:2502.01612, ICML.

### Motivazione intrinseca e sistemi riflessivi

- Schmidhuber, J. (2010). *Formal Theory of Creativity, Fun, and Intrinsic Motivation (1990–2010)*. IEEE Trans. Autonomous Mental Development 2(3):230–247.
- Schmidhuber, J. (2007). *Gödel Machines: Fully Self-Referential Optimal Universal Self-Improvers*. In *Artificial General Intelligence*, Springer.

### Neuroscienze — chunking, replay, cell assembly

- Miller, G.A. (1956). *The magical number seven, plus or minus two*. Psychological Review 63(2).
- Graybiel, A.M. (1998). *The basal ganglia and chunking of action repertoires*. Neurobiology of Learning and Memory 70(1-2):119–136.
- Jog, M.S. et al. (1999). *Building neural representations of habits*. Science 286:1745–1749.
- Barnes, T.D. et al. (2005). *Activity of striatal neurons reflects dynamic encoding and recoding of procedural memories*. Nature 437:1158–1161.
- Jin, X. & Costa, R.M. (2010). *Start/stop signals emerge in nigrostriatal circuits during sequence learning*. Nature 466:457–462.
- Jin, X., Tecuapetla, F., Costa, R.M. (2014). *Basal ganglia subcircuits distinctively encode the parsing and concatenation of action sequences*. Nature Neuroscience 17:423–430.
- Saffran, J.R., Aslin, R.N., Newport, E.L. (1996). *Statistical learning by 8-month-old infants*. Science 274:1926–1928.
- Lewis, P.A. & Durrant, S.J. (2011). *Overlapping memory replay during sleep builds cognitive schemata*. Trends in Cognitive Sciences 15(8):343–351.
- Tse, D. et al. (2007). *Schemas and memory consolidation*. Science 316:76–82.
- Garagnani, M., Wennekers, T., Pulvermüller, F. (2008). *A neuroanatomically grounded Hebbian-learning model of attention-language interactions in the human brain*. European Journal of Neuroscience 27(2).
- Tomasello, R., Garagnani, M., Wennekers, T., Pulvermüller, F. (2017). *Brain connections of words, perceptions and actions: a neurobiological model of spatio-temporal semantic activation*. Neuropsychologia 98.

### Sphex

- Wooldridge, D.E. (1963). *The Machinery of the Brain*. McGraw-Hill. — fonte originale
- Hofstadter, D.R. (1979). *Gödel, Escher, Bach: An Eternal Golden Braid*. Basic Books.
- Hofstadter, D.R. (1985). *Metamagical Themas*. Basic Books. — *sphexishness*
- Dennett, D.C. (1984). *Elbow Room*. MIT Press.
- Keijzer, F. (2013). *The Sphex story: How the cognitive sciences kept repeating an old and questionable anecdote*. Philosophical Psychology 26(4):502–519. — **la critica**

### Automi cellulari e computational mechanics

- Crutchfield, J.P. & Young, K. (1989). *Inferring statistical complexity*. Physical Review Letters 63:105–108.
- Hanson, J.E. & Crutchfield, J.P. (1992). *The attractor–basin portrait of a cellular automaton*. Journal of Statistical Physics 66:1415–1462.
- Crutchfield, J.P. & Hanson, J.E. (1993). *Turbulent pattern bases for cellular automata*. Physica D 69:279–301.
- Hanson, J.E. & Crutchfield, J.P. (1997). *Computational mechanics of cellular automata: An example*. Physica D 103:169–189.
- Crutchfield, J.P. & Mitchell, M. (1995). *The evolution of emergent computation*. PNAS 92:10742–10746.
- Shalizi, C.R. & Crutchfield, J.P. (2001). *Computational mechanics: pattern and prediction, structure and simplicity*. Journal of Statistical Physics 104:817–879.
- Shalizi, C.R. & Klinkner, K.L. (2004). *Blind construction of optimal nonlinear recursive predictors for discrete sequences* (CSSR). UAI.
- Shalizi, C.R. et al. (2006). *Automatic filters for the detection of coherent structure in spatiotemporal systems*. Physical Review E 73:036104.
- Hordijk, W., Shalizi, C.R., Crutchfield, J.P. (2001). *Upper bound on the products of particle interactions in cellular automata*. Physica D 154:240–258.
- Wolfram, S. (2002). *A New Kind of Science*. Wolfram Media. — irriducibilità computazionale
- Israeli, N. & Goldenfeld, N. (2004). *Computational irreducibility and the predictability of complex physical systems*. Physical Review Letters 92:074105.
- Israeli, N. & Goldenfeld, N. (2006). *Coarse-graining of cellular automata, emergence, and the predictability of complex systems*. Physical Review E 73:026203.
- Zenil, H. (2010). *Compression-based investigation of the dynamical properties of cellular automata and other systems*. Complex Systems 19(1):1–28.
- Gosper, R.W. (1984). *Exploiting regularities in large cellular spaces*. Physica D 10(1-2):75–80. — **HashLife**
- Rokicki, T. (2006). *An Algorithm for Compressing Space and Time*. Dr. Dobb's Journal. — esposizione divulgativa di HashLife
- Golly — implementazione di riferimento: `https://golly.sourceforge.io/`
- Catagolue — censimento distribuito di pattern in Life: `https://catagolue.hatsya.com/`

### Simbolizzazione interna (mech interp)

- Nanda, N. et al. (2023). *Progress measures for grokking via mechanistic interpretability*. ICLR.
- Todd, E. et al. (2024). *Function vectors in large language models*. ICLR.
- *Emergent Symbolic Mechanisms Support Abstract Reasoning in Large Language Models*. ICML 2025.

### Knowledge representation

- Gangemi, A. (2005). *Ontology Design Patterns for Semantic Web Content*. ISWC.
- Gangemi, A. & Presutti, V. (2009). *Ontology Design Patterns*. In *Handbook on Ontologies*, Springer.

### Thom e dintorni

- Thom, R. (1972). *Stabilité structurelle et morphogenèse*. Benjamin. — trad. ingl. *Structural Stability and Morphogenesis*, 1975.
- Zeeman, E.C. (1977). *Catastrophe Theory: Selected Papers 1972–1977*. Addison-Wesley.
- Sussmann, H.J. & Zahler, R.S. (1978). *Catastrophe theory as applied to the social and biological sciences: a critique*. Synthese 37(2):117–216. — **la stroncatura**
- Petitot, J. (2011). *Cognitive Morphodynamics*. Peter Lang.
- Scheffer, M. et al. (2009). *Early-warning signals for critical transitions*. Nature 461:53–59. — la discendenza viva

---

*Nota: alcuni riferimenti sono citati a memoria e andrebbero verificati su Scholar/DBLP prima di finire in bibliografia formale — in particolare anno ed edizione dei lavori più recenti (2024–2026).*
