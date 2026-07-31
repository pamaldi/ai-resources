# P e NP — Riassunto delle slide

## 1. Dalla computabilità alla complessità

Il corso ha fin qui affrontato la **teoria della computabilità**, che si chiede: *quali problemi possono essere risolti da un computer?* La teoria della complessità sposta la domanda un gradino più su: *quali problemi possono essere risolti **efficientemente** da un computer?*

Il quadro delle classi di linguaggi visto finora si arricchisce quindi di una nuova regione: dentro l'universo dei linguaggi (che comprende anche gli indecidibili), stanno i linguaggi decidibili (R), e al loro interno i linguaggi regolari, i linguaggi context-free (CFL) e — trasversale a questi — la nuvola dei "linguaggi decidibili efficientemente", che è l'oggetto di studio da qui in avanti.

## 2. Cosa significa "algoritmo efficiente"?

L'intuizione si costruisce per confronto tra algoritmi ingenui e algoritmi furbi sullo stesso problema:

- **Sottosequenza crescente più lunga**: l'approccio ingenuo costa O(n · 2ⁿ), quello veloce O(n²).
- **Cammino minimo**: l'approccio ingenuo costa O(n² · n!), quello veloce O(n + m), con n nodi e m archi.

La linea di demarcazione proposta è tra **polinomi ed esponenziali**:

- Un algoritmo gira in **tempo polinomiale** se il suo tempo di esecuzione è O(nᵏ) per qualche costante k.
- Le funzioni polinomiali "scalano bene": piccole variazioni nella dimensione dell'input non producono variazioni enormi nel tempo totale.
- Le funzioni esponenziali "scalano malissimo": piccole variazioni dell'input producono variazioni gigantesche del tempo di esecuzione.

## 3. La tesi di Cobham-Edmonds

> Un linguaggio L può essere deciso *efficientemente* se e solo se esiste una macchina di Turing che lo decide in tempo polinomiale, cioè in tempo O(nᵏ) per qualche k ∈ ℕ.

Punti importanti sottolineati dalle slide:

- Come la tesi di Church-Turing, **non è un teorema**: è un'assunzione sulla natura del calcolo efficiente, e per certi versi controversa.
- La corrispondenza polinomiale = efficiente ha casi limite paradossali:
  - Tempi "efficienti" solo formalmente: n^1.000.000.000.000 oppure la costante 10⁵⁰⁰ sono polinomiali ma assurdi in pratica.
  - Tempi "inefficienti" solo formalmente: n^(0,0001 log n) o 1,000000001ⁿ sono superpolinomiali/esponenziali ma crescono in modo mitissimo.
- Esempi di tempi genuinamente efficienti: 4n + 13, n³ − 2n² + 4n, n log log n. Genuinamente inefficienti: 2ⁿ, n!, nⁿ.

## 4. La classe P

**Definizione.** P (polynomial time) è la classe di tutti i problemi risolvibili in tempo polinomiale:

```
P = { L | esiste un decisore in tempo polinomiale per L }
```

Assumendo la tesi di Cobham-Edmonds, un linguaggio sta in P se e solo se può essere deciso efficientemente.

**Posizione nel quadro generale:** tutti i linguaggi regolari sono in P (hanno TM in tempo lineare); tutti i CFL sono in P (serve un argomento più fine, tramite l'algoritmo CYK o quello di Earley). P vive dentro R, l'insieme dei decidibili.

**Esempi di problemi in P:**

- **Connettività di grafi**: dato un grafo G e due nodi s e t, esiste un cammino da s a t?
- **Test di primalità**: dato un numero p, p è primo? (La migliore TM nota citata nelle slide impiega tempo O(n³⁷).)
- **Matching massimo**: dato un insieme di compiti e lavoratori, se ogni lavoratore svolge esattamente un compito, si possono svolgere almeno n compiti?
- **Remoteness testing**: dato un grafo G, tutti i nodi sono a distanza al più k l'uno dall'altro?
- **Programmazione lineare**: dati vincoli lineari e una funzione obiettivo lineare, l'ottimo vale almeno n?
- **Edit distance**: date due stringhe, si possono trasformare l'una nell'altra con al più n modifiche a singolo carattere?

## 5. Cosa non si riesce a fare in tempo polinomiale

Le slide mostrano due esempi di **spazi di ricerca esponenziali**:

- Contare i cammini semplici da un nodo di partenza a uno di arrivo in un grafo: possono essere esponenzialmente tanti.
- Contare i sottoinsiemi di un insieme (l'esempio delle monete): un insieme di n elementi ha 2ⁿ sottoinsiemi.

**L'osservazione chiave:** di questi oggetti ce ne sono (almeno) esponenzialmente tanti, ma *ciascun oggetto preso da solo è piccolo*: un cammino semplice non è più lungo del numero di nodi del grafo; un sottoinsieme non ha più elementi dell'insieme di partenza. Lo spazio di ricerca è enorme, ma ogni candidato è compatto e controllabile. Questa osservazione motiva la classe NP.

## 6. Nondeterminismo: "e se potessi indovinare?"

L'idea guida: *e se si potesse magicamente indovinare quale elemento dello spazio di ricerca è quello giusto?*

Le slide presentano macchine di Turing nondeterministiche (NTM) che risolvono problemi con lo schema "indovina e verifica":

- **Sottosequenza crescente**: su input ⟨S, k⟩, indovina nondeterministicamente una sottosequenza di S; se è crescente e lunga almeno k, accetta; altrimenti rifiuta.
- **Cammino tra due nodi**: su input ⟨G, u, v, k⟩, indovina una permutazione di al più k nodi; se è un cammino da u a v, accetta; altrimenti rifiuta.

### Misurare l'efficienza di una NTM

- Il calcolo nondeterministico si visualizza come un **albero** di scelte (quello deterministico è una linea retta).
- La complessità temporale di una NTM è **l'altezza dell'albero**: la lunghezza del ramo più lungo. Intuizione: se si eseguissero tutti i rami in parallelo, quanto tempo servirebbe perché terminino tutti?

### Dal nondeterminismo al determinismo

**Teorema:** per ogni NTM con complessità f(n) esiste una TM deterministica con complessità 2^O(f(n)).

Non è noto se si possa fare meglio nel caso generale: le NTM esplorano più opzioni in parallelo, e questo "sembra" intrinsecamente più veloce del calcolo deterministico. La simulazione nota paga un prezzo esponenziale.

## 7. La classe NP

**Definizione (via NTM).** NP (nondeterministic polynomial time) è la classe dei problemi risolvibili in tempo polinomiale da una macchina di Turing nondeterministica:

```
NP = { L | esiste una NTM che decide L in tempo polinomiale nondeterministico }
```

**Esempi di problemi in NP:**

- **Sudoku generalizzato**: una griglia n² × n² ha soluzione? La NTM indovina come riempire tutte le celle e verifica deterministicamente. Analisi: la griglia ha n⁴ celle (tempo O(n⁴) per riempirla); righe, colonne e riquadri da controllare sono O(n²), ciascuno verificabile in O(n²); tempo totale O(n⁴) — polinomiale.
- **k-colorazione di grafi**: assegnare uno di k colori a ogni nodo in modo che nodi adiacenti abbiano colori diversi (applicazioni: compilatori, celle telefoniche). La NTM indovina la colorazione e ne verifica la legalità.
- **Subset sum**: dato un insieme S di naturali e un target n, esiste un sottoinsieme di S che somma a n?
- **Cammino più lungo**: esiste un cammino semplice da u a v di lunghezza almeno k?
- **Job scheduling**: k lavoratori in parallelo possono completare tutti i job entro il tempo t?

### Problemi come linguaggi

Le domande astratte vengono formalizzate come linguaggi:

```
SUDOKU = { ⟨S⟩ | S è una griglia di Sudoku risolvibile }
COLOR  = { ⟨G, k⟩ | G è un grafo non orientato, k ∈ ℕ, e G è k-colorabile }
```

Una griglia S è risolvibile se e solo se ⟨S⟩ ∈ SUDOKU; G è k-colorabile se e solo se ⟨G, k⟩ ∈ COLOR.

## 8. La definizione di NP tramite verificatori

**Intuizione:** un linguaggio L sta in NP se per ogni w ∈ L esiste un modo *efficiente* di dimostrare a qualcuno che w ∈ L. È l'analogo dell'intuizione del verificatore per la classe RE, con in più il requisito di efficienza.

**Richiamo (verificatori per RE).** Un verificatore per L è una TM deterministica V tale che: V si ferma su ogni input, e w ∈ L se e solo se esiste c ∈ Σ* tale che V accetta ⟨w, c⟩. Teorema: L ∈ RE se e solo se esiste un verificatore per L.

**Verificatore in tempo polinomiale.** È una TM deterministica V tale che:

1. V si ferma su ogni input;
2. w ∈ L ⟺ ∃c ∈ Σ*. V accetta ⟨w, c⟩;
3. il tempo di esecuzione di V è polinomiale in |w|.

La stringa c è il **certificato**: la prova compatta che accompagna l'input. Esempi: per il Sudoku, il certificato è la presunta soluzione A, e V controlla deterministicamente che A risolva S; per la colorazione, il certificato è la presunta colorazione C, e V controlla che sia una k-colorazione legale di G.

**Teorema (equivalenza delle due definizioni).** L ∈ NP se e solo se esiste un verificatore in tempo polinomiale per L.

- (⇐) Se esiste il verificatore V, si costruisce una NTM che indovina nondeterministicamente un certificato e poi esegue deterministicamente V per controllarlo; la NTM gira in tempo polinomiale nondeterministico.
- (⇒) Se L ∈ NP, si usa la costruzione generale che trasforma una NTM in un verificatore e si argomenta che gira in tempo polinomiale.

Le due definizioni — "indovina e verifica" e "certificato + verificatore" — sono due facce della stessa classe.

## 9. P ≟ NP: la domanda più importante dell'informatica teorica

Dalle definizioni segue subito che **P ⊆ NP**: un decisore deterministico polinomiale è un caso particolare di quello nondeterministico.

La domanda aperta è se valga l'uguaglianza. Con la definizione tramite verificatori, si può riformulare così:

> Se la soluzione di un problema può essere **controllata** efficientemente, il problema può anche essere **risolto** efficientemente?

Una risposta in qualunque direzione darebbe intuizioni fondamentali sulla natura del calcolo.

### Perché la questione è importante

Problemi efficientemente verificabili ma senza soluzione efficiente nota:

- **Steiner tree**: si può costruire una rete elettrica che colleghi certe case entro un certo costo?
- **Shortest common supersequence**: esiste un filamento di DNA semplice di cui più sequenze geniche possano far parte?
- **Allocazione ottima dei registri** in un compilatore.
- **Job scheduling**: distribuire i compiti a più lavoratori minimizzando il tempo di completamento.
- E molti altri.

Le conseguenze sono nette:

- **Se P = NP**: tutti questi problemi hanno soluzioni efficienti; un enorme numero di problemi apparentemente difficili diventerebbe trattabile, e la nostra capacità di risolvere problemi scalerebbe bene con la loro dimensione.
- **Se P ≠ NP**: nessuno di questi problemi ha soluzione efficiente; servirebbe una potenza di calcolo enorme per compiti apparentemente semplici, e la nostra capacità di risolvere problemi non terrebbe il passo della nostra curiosità.

### Lo stato dell'arte

- In 43 anni (al momento delle slide) non è stata trovata alcuna dimostrazione corretta in nessuna delle due direzioni.
- Molte *tecniche* di dimostrazione sono state dimostrate insufficienti a risolvere la questione.
- La maggioranza degli informatici crede che P ≠ NP, ma non è una maggioranza schiacciante.
- Il **Clay Mathematics Institute** offre un premio da **1.000.000 $** a chi dimostri o confuti P = NP.

## 10. Riducibilità: usare un problema per risolverne un altro

L'ultima parte introduce la tecnica della **riduzione** con un esempio completo: matching massimo e tiling di domino.

### Matching massimo

- Dato un grafo non orientato G, un **matching** è un insieme di archi tali che nessuna coppia di archi condivide un estremo.
- Un **matching massimo** è un matching col massimo numero di archi. I matching massimi non sono necessariamente unici.
- **Teorema (Edmonds)**: il paper "Paths, Trees, and Flowers" di Jack Edmonds (lo stesso della tesi di Cobham-Edmonds) fornisce un algoritmo in tempo polinomiale per il matching massimo. Formalizzando:

```
MATCHING = { ⟨G, k⟩ | G è un grafo non orientato con un matching di taglia ≥ k }
MATCHING ∈ P
```

### Domino tiling e la riduzione

```
DOMINO = { ⟨D, k⟩ | D è una griglia su cui si possono piazzare k domino non sovrapposti }
```

Si dimostra che DOMINO ∈ P *riducendolo* a MATCHING:

1. **Conversione**: si trasforma la griglia in un grafo — ogni cella vuota diventa un nodo, e due celle vuote adiacenti sono collegate da un arco.
2. **Interrogazione**: si chiede se quel grafo ha un matching di taglia almeno k.
3. **Risposta**: si restituisce la risposta ottenuta. (Ogni domino copre due celle adiacenti, cioè un arco; domino non sovrapposti = archi senza estremi comuni = matching.)

In pseudocodice:

```java
boolean canPlaceDominos(Grid G, int k) {
    return hasMatching(gridToGraph(G), k);
}
```

**Perché funziona ed è efficiente:** la conversione griglia → grafo richiede tempo polinomiale; il controllo del matching richiede tempo polinomiale (per il teorema di Edmonds); la composizione di due passi polinomiali è polinomiale. Quindi DOMINO ∈ P.

Questo è il prototipo del ragionamento per riduzione, che nelle lezioni successive diventerà lo strumento centrale per la teoria della NP-completezza: trasformare un problema in un altro preservando la risposta, per trasferire algoritmi (o difficoltà) dall'uno all'altro.

## 11. Perché ogni problema si può ridurre a un linguaggio riconosciuto da una macchina

Le slide fanno un passaggio veloce ("Problems and Languages") che in realtà è il fondamento invisibile di tutto il corso. Vale la pena rallentare e capire *perché* funziona sempre, perché a prima vista sembra un trucco: come può "il Sudoku ha soluzione?" essere la stessa cosa di "questa stringa appartiene a questo insieme di stringhe?"

### Passo 1 — Tutto è codificabile come stringa

Qualunque oggetto matematico discreto si può scrivere come sequenza finita di simboli su un alfabeto finito. Non è una metafora: è ciò che i computer fanno letteralmente ogni giorno.

- Un **numero** è la sua scrittura binaria: 13 → `1101`.
- Un **grafo** è la sua lista di archi: `{(1,2),(2,3),(1,3)}` → la stringa `"1,2;2,3;1,3"`. O la matrice di adiacenza riga per riga: `011101110`.
- Una **griglia di Sudoku** è la sequenza delle sue 81 celle lette per righe, con un simbolo per "vuoto".
- Una **formula booleana** è il suo testo: `(x1|~x2)&(x2|x3)`.
- Una **coppia** di oggetti ⟨G, k⟩ si codifica concatenando le due codifiche con un separatore.
- Perfino una **macchina di Turing** è codificabile come stringa (la lista delle sue transizioni) — è l'intuizione che rende possibile il problema della fermata: le macchine possono ricevere *altre macchine* come input.

La notazione ⟨·⟩ delle slide significa esattamente questo: ⟨G, k⟩ = "una codifica ragionevole di G e k come stringa". Il dettaglio della codifica è irrilevante — binario, JSON, quello che vuoi — purché sia decodificabile in tempo polinomiale. Le classi di complessità sono robuste rispetto alla scelta: passare da una codifica ragionevole a un'altra costa al più un fattore polinomiale, che P e NP assorbono per definizione. (Un solo avvertimento: la codifica *unaria* dei numeri — scrivere 1000 come mille aste — non è ragionevole, perché gonfia l'input esponenzialmente e falsa i conti. È il cuore della sottigliezza sul knapsack "pseudo-polinomiale".)

### Passo 2 — Ogni domanda sì/no è un insieme di stringhe

Un **problema decisionale** è una domanda con risposta sì o no su un input: "questo grafo è connesso?", "questa formula è soddisfacibile?", "questo numero è primo?".

Ora l'osservazione chiave, semplice e spiazzante: una domanda sì/no è *completamente determinata* dall'insieme degli input la cui risposta è sì. Non c'è nient'altro nella domanda. Quindi:

```
problema decisionale  ≡  insieme delle codifiche delle istanze-sì  ≡  linguaggio
```

È esattamente il passaggio delle slide:

```
SUDOKU = { ⟨S⟩ | S è una griglia risolvibile }
PRIMES = { ⟨p⟩ | p è primo }
COLOR  = { ⟨G, k⟩ | G è k-colorabile }
```

Chiedere "S è risolvibile?" e chiedere "⟨S⟩ ∈ SUDOKU?" è la *stessa domanda*, riscritta. Non abbiamo perso niente e non abbiamo aggiunto niente: abbiamo solo cambiato vocabolario, da "problemi" a "insiemi di stringhe". E "riconoscere un linguaggio" — decidere se una stringa sta in un insieme — è precisamente ciò che le macchine (DFA, PDA, TM) sanno fare. Il ponte è completo: **risolvere un problema = decidere l'appartenenza a un linguaggio = far girare una macchina**.

### Passo 3 — Ma i problemi veri non sono sì/no! (Sì che lo sono)

Obiezione naturale: nella pratica non si chiede "esiste un giro sotto i 1000 km?" — si chiede "trovami il giro *più corto*". I problemi reali sono di **ottimizzazione** o di **ricerca**, non decisionali. La teoria non sta studiando una versione giocattolo?

No, e i due argomenti sono i seguenti.

**Ottimizzazione → decisione, via soglia + ricerca binaria.** Dal problema di ottimizzazione "qual è la lunghezza del giro minimo?" si ricava la famiglia decisionale "esiste un giro di lunghezza ≤ k?". Se sai rispondere alla versione decisionale, trovi l'ottimo con ricerca binaria su k: "≤ 1000? sì. ≤ 500? no. ≤ 750? sì..." — il numero di domande è logaritmico nel range dei valori, cioè *polinomiale nella lunghezza in bit* dell'input. Quindi: ottimizzazione facile ⟺ decisione facile, a meno di fattori polinomiali. Studiare la versione decisionale non perde nulla della difficoltà.

**Ricerca → decisione, via autoriducibilità.** E se voglio la soluzione stessa, non solo sapere che esiste? Anche qui la decisione basta, con un trucco elegante. Prendi SAT: hai un oracolo che risponde solo "soddisfacibile sì/no" e vuoi *l'assegnazione*. Procedi così: chiedi se φ è soddisfacibile con x₁ = vero (cioè se φ[x₁:=vero] è soddisfacibile). Se sì, fissa x₁ = vero; se no, fissa x₁ = falso. Ripeti con x₂ sulla formula semplificata, poi x₃... Dopo n domande hai ricostruito un'intera assegnazione soddisfacente, un bit alla volta. La versione sì/no, interrogata con astuzia, *contiene* la versione costruttiva. Questa proprietà (autoriducibilità) vale per tutti i problemi NP-completi.

Morale: la restrizione ai problemi decisionali non è una semplificazione di comodo — è una **normalizzazione senza perdita**. Tutta la difficoltà di ottimizzare e costruire si conserva nella domanda sì/no.

### Passo 4 — Perché questa riduzione è così potente

Il guadagno di aver compresso "tutti i problemi" in "tutti i linguaggi" è enorme, e spiega la forma di tutto il corso:

- **Uniformità.** Sudoku, primalità, scheduling, la fermata di un programma: oggetti che sembrano vivere in mondi diversi diventano tutti punti dello *stesso spazio* — l'insieme dei linguaggi su un alfabeto. Diventa sensato chiedersi "quali linguaggi riconosce questa macchina?" e disegnare i cerchi concentrici delle slide.
- **Confrontabilità.** Due problemi qualunque ora si possono confrontare: L₁ si riduce a L₂ se esiste una funzione calcolabile (efficientemente) che trasforma istanze di L₁ in istanze di L₂ preservando la risposta. Le riduzioni — DOMINO → MATCHING, e poi tutto Cook-Levin e Karp — esistono *perché* tutto è un linguaggio: si tratta sempre e solo di trasformare stringhe in stringhe.
- **Limiti dimostrabili.** Sui linguaggi si può fare matematica vera: contare (i linguaggi sono più che numerabili, le macchine sono numerabili → *devono* esistere linguaggi non riconoscibili da nessuna macchina — un argomento di cardinalità puro), diagonalizzare (la fermata), pompare (i pumping lemma). Nessuno di questi argomenti sarebbe formulabile restando nel linguaggio vago dei "problemi".

C'è anche un confine onesto da dichiarare: questa riduzione cattura i problemi con input **discreti e finiti** e risposte **definite**. Problemi su oggetti genuinamente continui, o compiti senza criterio netto di correttezza ("scrivi una bella poesia"), non rientrano direttamente nello schema — vanno prima discretizzati o formalizzati, e qualcosa nella formalizzazione si può perdere. Ma per tutto ciò che un computer digitale può anche solo *ricevere in input*, la catena problema → stringa → linguaggio → macchina è completa. È il motivo per cui la tesi di Church-Turing e quella di Cobham-Edmonds si formulano sui linguaggi: sono il denominatore comune di ogni calcolo.

## 12. Panoramica: linguaggi regolari, CFL e R — la gerarchia sotto P

Le slide danno per scontata la gerarchia vista nella prima parte del corso (è il "Recap from Last Time"). Vale la pena richiamarla, perché P e NP si innestano esattamente lì sopra. L'idea unificante: ogni classe corrisponde a una **macchina con più o meno memoria**, e più memoria significa più linguaggi riconoscibili.

### Linguaggi regolari — memoria finita

**Macchina:** automa a stati finiti (DFA/NFA), oppure equivalentemente le **espressioni regolari**. Il teorema di Kleene dice che le tre formulazioni (DFA, NFA, regex) riconoscono esattamente gli stessi linguaggi.

**Intuizione:** la macchina ha solo un numero *fisso* di stati — può ricordare "in che situazione sono" ma non può *contare* quantità illimitate. Tutto ciò che si riconosce guardando l'input una volta, da sinistra a destra, con memoria costante.

**Esempi di linguaggi regolari:**

- Stringhe binarie con un numero pari di 1: `(0*10*10*)*0*` — bastano due stati, "pari" e "dispari".
- Stringhe che finiscono in `.csv`: è il pattern matching di ogni giorno.
- Numeri divisibili per 3 letti in binario: sorprendente ma vero — bastano 3 stati che tracciano il resto mod 3.
- Un indirizzo email "ragionevole", una targa italiana, un codice fiscale ben formato: tutta la validazione di formato quotidiana (i campi di un form, i pattern in NiFi, le regex in PostgreSQL con `~`) vive qui.
- Le keyword e i token di un linguaggio di programmazione: il **lexer** di ogni compilatore è un automa finito.

**Cosa NON è regolare — e come si dimostra:**

- `{ 0ⁿ1ⁿ | n ≥ 0 }` — tante 0 seguite da altrettante 1. Per riconoscerlo bisogna *contare* le 0, e n è illimitato: nessun numero finito di stati basta. Lo strumento formale è il **pumping lemma**: in ogni stringa abbastanza lunga di un linguaggio regolare c'è un pezzo "pompabile" (ripetibile a piacere restando nel linguaggio); in 0ⁿ1ⁿ pompare rompe il bilanciamento.
- Le parentesi bilanciate — stesso motivo: serve contare le aperte non ancora chiuse.
- Conseguenza pratica famosa: **non si può parsare l'HTML con le regex** (né il JSON, né l'XML). Ogni volta che qualcuno ci prova, sta cercando di far contare una macchina che non sa contare.

**Costo computazionale:** decidere se una stringa appartiene a un linguaggio regolare è O(n) — tempo lineare, memoria costante. Per questo tutti i linguaggi regolari sono in P, ed è il motivo per cui le regex (quelle vere, senza backreference) sono così veloci.

### Linguaggi context-free (CFL) — memoria a pila

**Macchina:** automa a pila (PDA), oppure equivalentemente le **grammatiche context-free** (CFG): regole di riscrittura come `S → (S)S | ε`.

**Intuizione:** oltre agli stati finiti, la macchina ha una **pila** illimitata — può contare e può gestire strutture *annidate*: apri una parentesi, la impili; la chiudi, la spili. È esattamente la memoria che serve per la ricorsione.

**Esempi di CFL:**

- `{ 0ⁿ1ⁿ | n ≥ 0 }` — il non-regolare di prima: con la pila si impilano le 0 e si spilano leggendo le 1. Grammatica: `S → 0S1 | ε`.
- Parentesi bilanciate: `S → (S)S | ε`. È l'esempio archetipo.
- Palindromi: `S → 0S0 | 1S1 | 0 | 1 | ε` — la pila ricorda la prima metà e la confronta con la seconda.
- **La sintassi dei linguaggi di programmazione**: espressioni aritmetiche annidate, blocchi `{ ... }` dentro blocchi, `if` dentro `if`. Il **parser** di ogni compilatore lavora su una grammatica context-free — la divisione lexer (regolare) / parser (context-free) dei compilatori ricalca esattamente questa gerarchia teorica. Lo stesso vale per SQL, per JSON, per le espressioni matematiche.

**Cosa NON è context-free:**

- `{ aⁿbⁿcⁿ | n ≥ 0 }` — tre contatori da tenere allineati: una sola pila non basta (spilando le a per contare le b, si perde il conto per le c). Esiste un pumping lemma anche per i CFL che lo dimostra.
- `{ ww | w ∈ {0,1}* }` — una stringa ripetuta due volte. Curioso: i palindromi (ww *rovesciata*) sono CFL, la copia esatta no — la pila restituisce in ordine inverso, perfetto per gli specchi, pessimo per le copie.
- In pratica: i controlli *semantici* dei linguaggi ("questa variabile è stata dichiarata?", "i tipi combaciano?") non sono context-free — infatti i compilatori li fanno in una fase separata, dopo il parsing.

**Costo computazionale:** decidere l'appartenenza a un CFL costa O(n³) nel caso generale (algoritmo **CYK**, o Earley) — è l'argomento "più fine" a cui accennano le slide per dire che tutti i CFL sono in P. Le grammatiche deterministiche usate nei linguaggi reali (LL, LR) si parsano in O(n).

### R — i linguaggi decidibili: memoria illimitata

**Macchina:** la **macchina di Turing** — nastro infinito, testina che legge, scrive e si muove in entrambe le direzioni. Nessun vincolo di tempo: conta solo che la macchina *termini sempre* con una risposta sì/no.

**Intuizione:** R (recursive/decidable) è tutto ciò che è *algoritmicamente risolvibile*, senza alcun riguardo per l'efficienza. È il confine della computabilità, non della praticità.

**Esempi di linguaggi in R:**

- `{ aⁿbⁿcⁿ }` e `{ ww }` — i due che bucavano i CFL: con un nastro riscrivibile sono banali (fai avanti e indietro spuntando i simboli).
- Tutti i problemi in P e in NP: SAT, TSP, Sudoku — magari lentissimi, ma decidibili: in ultima istanza si può sempre enumerare tutte le possibilità.
- Problemi mostruosamente costosi ma decidibili: l'equivalenza di espressioni regolari con squaring richiede spazio esponenziale; l'aritmetica di Presburger richiede tempo doppiamente esponenziale — decidibili, ma fuori da ogni speranza pratica. R contiene molta roba che nessun computer finirà mai.

**Cosa sta FUORI da R — l'indecidibile:**

- Il **problema della fermata**: dato un programma e un input, il programma termina? Dimostrazione per diagonalizzazione (Turing, 1936): nessun algoritmo può deciderlo per tutti i programmi. È il "muro esterno" del diagramma delle slide.
- Il **teorema di Rice** generalizza: *ogni* proprietà semantica non banale dei programmi è indecidibile — "questo programma stampa mai X?", "queste due funzioni sono equivalenti?", "questo codice contiene malware?" (in senso esatto). È il motivo teorico per cui l'analisi statica del software è sempre approssimata: warning falsi positivi e bug non trovati non sono difetti degli strumenti, sono matematica.
- La verità nell'aritmetica (conseguenza di Gödel), il decimo problema di Hilbert (equazioni diofantee), il problema della corrispondenza di Post.

### La gerarchia completa, in un colpo d'occhio

| Classe | Macchina | Memoria | Esempio dentro | Esempio fuori | Costo appartenenza |
|---|---|---|---|---|---|
| Regolari | DFA / regex | finita | numero pari di 1 | 0ⁿ1ⁿ | O(n) |
| CFL | automa a pila | pila | parentesi bilanciate | aⁿbⁿcⁿ | O(n³) (CYK) |
| P | TM, tempo polinomiale | nastro, tempo O(nᵏ) | cammino minimo | (si congettura) SAT | polinomiale per def. |
| NP | NTM polinomiale / verificatore | certificato + verifica polinomiale | SAT, Sudoku | problemi EXPTIME-completi | verifica polinomiale |
| R | TM che termina sempre | nastro illimitato | tutto quanto sopra | problema della fermata | nessun limite |

Ogni inclusione andando verso il basso è **stretta e dimostrata** (regolari ⊊ CFL ⊊ ... ⊊ R), con una sola eccezione: P ⊆ NP, dove nessuno sa se l'inclusione sia stretta. È l'unico gradino incerto della scala — ed è esattamente il tema di queste slide.

Un'ultima osservazione che lega le due metà del corso: la gerarchia regolari/CFL/R risponde a "*che memoria serve*", quella P/NP a "*che tempo serve*". Sono due assi ortogonali di una stessa domanda — cosa può fare una macchina con risorse limitate — e il diagramma a cerchi concentrici delle slide li sovrappone: la nuvola dei "linguaggi efficientemente decidibili" taglia trasversalmente CFL e R proprio perché l'efficienza temporale non rispetta i confini della memoria.

## 13. SAT: il problema al centro di tutto

Se la teoria della complessità avesse un protagonista, sarebbe SAT. Le slide non lo trattano ancora (arriva con la NP-completezza), ma tutto ciò che segue nel corso vi orbita attorno. Vale la pena conoscerlo bene.

### Il problema

**Input:** una formula booleana — variabili che valgono vero o falso, connesse da AND (∧), OR (∨) e NOT (¬). Per esempio:

```
φ = (x ∨ ¬y) ∧ (y ∨ z) ∧ (¬x ∨ ¬z) ∧ (x ∨ y ∨ ¬z)
```

**Domanda:** esiste un'assegnazione di vero/falso alle variabili che rende vera l'intera formula? (Si dice che φ è **soddisfacibile**.)

Per la φ qui sopra la risposta è sì: prova x = vero, y = vero, z = falso. Sostituendo, ogni clausola (ogni pezzo tra parentesi) contiene almeno un letterale vero, quindi tutta la congiunzione è vera. Ecco il certificato in azione: dati i tre valori, la verifica è una sostituzione meccanica in tempo lineare. Trovarli, invece, nel caso generale richiede di esplorare uno spazio di 2ⁿ assegnazioni.

### La forma normale congiuntiva (CNF) e k-SAT

Per convenzione SAT si studia su formule in **CNF**: un AND di clausole, dove ogni clausola è un OR di letterali (variabili o loro negazioni) — esattamente la forma di φ sopra. Non è una restrizione: ogni formula booleana si converte in CNF equisoddisfacibile con crescita solo polinomiale (trasformazione di Tseitin).

Limitando la lunghezza delle clausole si ottiene la famiglia k-SAT, e qui si nasconde uno dei confini più netti della teoria:

- **1-SAT**: banale — ogni clausola è un singolo letterale, basta controllare che non compaiano x e ¬x insieme.
- **2-SAT**: in **P**, anzi lineare. Il trucco è elegante: una clausola (a ∨ b) equivale alle implicazioni ¬a → b e ¬b → a; si costruisce il "grafo delle implicazioni" e la formula è insoddisfacibile se e solo se qualche x e ¬x finiscono nella stessa componente fortemente connessa. La logica si trasforma in raggiungibilità su grafi — un problema facile.
- **3-SAT**: **NP-completo**. E con esso ogni k ≥ 3, perché clausole lunghe si spezzano in clausole da 3 con variabili ausiliarie.

Da 2 a 3 letterali la difficoltà non cresce: *scatta*. Il motivo intuitivo: con clausole da 2, ogni scelta forzata propaga in una catena lineare di conseguenze; con clausole da 3, soddisfare un letterale lascia *due* alternative aperte nell'altra parte, e le alternative si moltiplicano — l'albero delle scelte torna a ramificare.

### Perché SAT è il "problema universale": Cook-Levin

**Teorema (Cook 1971, Levin indipendentemente):** SAT è NP-completo. Cioè: (1) SAT ∈ NP, e (2) *ogni* linguaggio in NP si riduce a SAT in tempo polinomiale.

Il punto (1) l'abbiamo visto: il certificato è l'assegnazione. Il punto (2) è l'idea geniale, e vale la pena capirla almeno a grandi linee, perché è una delle dimostrazioni più importanti dell'informatica.

Prendi un qualunque L ∈ NP. Per definizione esiste un verificatore V che, dati input w e certificato c, decide in tempo polinomiale p(n). Ora, l'esecuzione di V è un oggetto finito e completamente meccanico: una griglia di al più p(n) × p(n) celle — a ogni riga un istante di tempo, a ogni colonna una cella del nastro — dove ogni cella contiene un simbolo, e la testina sta da qualche parte in un certo stato. L'osservazione chiave: **ogni riga della griglia è determinata localmente dalla riga precedente** — cosa c'è in una cella al tempo t+1 dipende solo da tre celle al tempo t.

Questa località si cattura con variabili booleane ("la cella (i,j) contiene il simbolo s", "al tempo t la macchina è nello stato q") e clausole che dicono: la prima riga codifica w e un certificato *qualsiasi*; ogni transizione tra righe rispetta le regole di V; l'ultima riga è in stato accettante. La formula risultante è grande ma polinomiale, ed è soddisfacibile **se e solo se** esiste un certificato che fa accettare V — cioè se e solo se w ∈ L.

Morale filosofica: una formula booleana può *simulare qualunque computazione verificabile*. SAT non è difficile per caso — è difficile perché è un linguaggio di programmazione universale travestito da problema di logica. Ogni problema in NP è "SAT con un vestito diverso": il Sudoku è SAT, la colorazione è SAT, lo scheduling è SAT.

### Le due facce pratiche di questa universalità

L'universalità di Cook-Levin ha una lettura negativa e una positiva, ed è la positiva ad aver cambiato l'industria.

**Lettura negativa (teorica):** se risolvi SAT in tempo polinomiale, hai risolto tutto NP → P = NP. Quindi, credendo P ≠ NP, SAT è intrattabile nel caso peggiore.

**Lettura positiva (ingegneristica):** se costruisci un *buon solver* per SAT, hai automaticamente un buon solver per tutto NP — basta ridurre il tuo problema a SAT e premere invio. È esattamente ciò che è successo: dagli anni 2000 i **solver CDCL** (Conflict-Driven Clause Learning) hanno trasformato SAT da spauracchio teorico a tecnologia industriale. Le idee chiave:

- **Propagazione unitaria**: se in una clausola resta un solo letterale non assegnato, il suo valore è forzato — si propaga a cascata.
- **Apprendimento dai conflitti**: quando un ramo di ricerca porta a contraddizione, il solver analizza *perché* ed estrae una nuova clausola ("no-good") che memorizza l'errore, evitando di rifarlo in tutte le altre parti dell'albero.
- **Backjumping non cronologico**: invece di tornare indietro di un passo, si salta direttamente alla decisione che ha causato il conflitto.
- **Euristiche di scelta** (VSIDS) e **restart**: quali variabili provare prima, e quando ripartire da capo tenendosi le clausole imparate.

Risultato: istanze industriali con **milioni di variabili** risolte in secondi. Non contraddice l'NP-completezza — esistono ancora istanze piccole e diaboliche che stendono qualsiasi solver — ma rivela che le istanze *reali* hanno struttura (simmetrie, modularità, backbone) che il caso peggiore non ha.

**Dove si usa oggi, concretamente:**

- **Verifica di hardware**: i processori vengono verificati traducendo circuiti e proprietà in SAT (bounded model checking) — dal bug del Pentium in poi, l'industria dei chip vive di SAT solver.
- **Verifica e analisi di software**: SMT solver come Z3 (SAT arricchito con teorie: aritmetica, array, bitvector) alimentano l'esecuzione simbolica e i verificatori di programmi.
- **Gestione di dipendenze**: risolvere le dipendenze di pacchetti (apt, Eclipse, Rust/Cargo usano solver SAT o simili) è letteralmente SAT: "installa A" ∧ (A richiede B ∨ C) ∧ ¬(B ∧ D)...
- **Planning e configurazione**: dalla pianificazione di azioni in robotica ai configuratori di prodotti industriali.
- **Matematica assistita**: dimostrazioni ottenute via SAT, come il problema delle terne pitagoriche booleane (2016) — un certificato di 200 TB, verificabile meccanicamente. Il divario risolvere/verificare, di nuovo: la dimostrazione è mostruosa da *trovare*, ma ogni passo è banale da *controllare*.

### SAT e i suoi cugini dichiarativi

Lo stesso schema "descrivi i vincoli, lascia cercare al solver" esiste a livelli di espressività crescenti, con complessità crescente:

| Formalismo | Cosa aggiunge | Complessità della decisione |
|---|---|---|
| SAT | — | NP-completo |
| SMT | teorie (aritmetica, array...) | da NP-completo a indecidibile, secondo la teoria |
| ASP (programmi normali) | regole, negazione per fallimento, ricorsione | NP-completo (esistenza di un answer set) |
| ASP disgiuntivo | disgiunzione in testa | Σ₂ᵖ-completo (un gradino sopra NP) |
| QBF | quantificatori ∀/∃ sulle variabili | PSPACE-completo |

Il messaggio: SAT è il pavimento di un intero edificio di *programmazione dichiarativa*. I solver ASP come clingo condividono con i SAT solver il motore CDCL — quando si scrivono vincoli logici su dati reali e il solver risponde in millisecondi, si sta cavalcando esattamente la lettura positiva di Cook-Levin: la difficoltà universale di SAT, domata dalla struttura delle istanze concrete.

### Curiosità: la transizione di fase

Un fenomeno empirico affascinante: generando formule 3-SAT casuali, la difficoltà dipende dal rapporto α = clausole/variabili. Con α basso (pochi vincoli) quasi tutte le formule sono soddisfacibili e facili; con α alto (troppi vincoli) quasi tutte insoddisfacibili e ancora facili (le contraddizioni si trovano presto). La zona letale è intorno ad **α ≈ 4,27**: lì la probabilità di soddisfacibilità crolla dal ~100% allo ~0% quasi di colpo, e proprio lì le istanze diventano brutalmente difficili per ogni solver noto. È una vera transizione di fase, studiata anche con strumenti della meccanica statistica — uno dei punti di contatto più belli tra informatica e fisica.

## 14. Esempi pratici, molti e spiegati

Questa sezione espande le slide con esempi concreti: dove questi problemi compaiono nel mondo reale, perché stanno nella classe in cui stanno, e cosa si fa in pratica quando la teoria dice "difficile".

### Problemi in P — cose che i computer fanno bene ogni giorno

**Cammino minimo (Dijkstra, O((n+m) log n))**
È il cuore di Google Maps e di ogni navigatore: dato il grafo stradale, trovare il percorso più veloce da A a B. Sta in P perché il problema ha *sottostruttura ottima*: il cammino minimo verso una città passa per cammini minimi verso le città intermedie, quindi si può costruire la soluzione incrementalmente senza mai tornare indietro. Lo stesso algoritmo instrada i pacchetti in Internet (protocollo OSPF).

**Ordinamento (merge sort, O(n log n))**
Ogni volta che ordini le email per data o i prodotti per prezzo. È il caso da manuale di divide et impera: spezza, risolvi le metà, fondi. La teoria dimostra anche un lower bound: nessun ordinamento per confronti può battere n log n — un raro caso in cui sappiamo esattamente quanto costa un problema.

**Matching massimo (Edmonds, polinomiale)**
Applicazioni reali: assegnare specializzandi agli ospedali, donatori di rene a riceventi compatibili (i "kidney exchange" usano proprio matching su grafi), studenti ai progetti. Sorprende che sia in P: lo spazio dei matching possibili è esponenziale, ma la struttura dei "cammini aumentanti" permette di migliorare la soluzione un passo alla volta senza esplorare tutto.

**Programmazione lineare (ellissoide/punto interno, polinomiale)**
Ottimizzare una funzione lineare sotto vincoli lineari: miscele di raffineria, dieta a costo minimo, portafogli finanziari. Curiosità storica: il simplesso, l'algoritmo usato in pratica dal 1947, è *esponenziale nel caso peggiore* ma velocissimo nella realtà; solo nel 1979 (Khachiyan) si dimostrò che il problema è davvero in P. Morale: "in P" e "veloce in pratica" sono assi indipendenti.

**Test di primalità (AKS, 2002)**
Fondamentale per la crittografia: per generare chiavi RSA servono primi enormi. Per decenni si usarono test probabilistici (Miller-Rabin); AKS dimostrò che la primalità è in P in senso deterministico. Attenzione al contrasto con la *fattorizzazione*: dire "è primo?" è facile, trovare *i fattori* no — ed è su questa asimmetria che si regge RSA.

**Edit distance (programmazione dinamica, O(n·m))**
Il correttore ortografico che ti suggerisce "macchina" quando scrivi "machina", il `diff` di git, l'allineamento di sequenze di DNA in bioinformatica (Needleman-Wunsch è la stessa idea). In P grazie alla programmazione dinamica: la distanza tra due prefissi dipende solo da tre sottoproblemi più piccoli, quindi basta riempire una tabella n×m.

**Connettività / raggiungibilità (BFS/DFS, O(n+m))**
"Questo utente può raggiungere questa pagina?", "questi due componenti del circuito sono collegati?", "il pacchetto può arrivare a destinazione?". Banale per un computer: una visita del grafo. È il tipo di problema che nella pratica dei dati (pipeline, grafi stradali, reti di trasporto) si dà per scontato — ed è giusto darlo per scontato, perché è in P con costante piccola.

**2-SAT (polinomiale, O(n+m))**
Caso speciale istruttivo: SAT con clausole di *due* letterali si risolve in tempo lineare (componenti fortemente connesse sul grafo delle implicazioni). Con *tre* letterali diventa NP-completo. Il salto da 2 a 3 è uno dei confini più netti e famosi di tutta la teoria: la difficoltà non cresce gradualmente, scatta.

### Problemi in NP (NP-completi) — verificare facile, risolvere duro

**SAT / 3-SAT — il capostipite**
Data una formula booleana, esiste un'assegnazione che la rende vera? È il problema NP-completo originale (Cook-Levin). In pratica è ovunque travestito: verifica formale di hardware (Intel verifica i circuiti dei processori con solver SAT), configurazione di software (le dipendenze dei pacchetti Linux si risolvono con SAT), pianificazione. Paradosso pratico: i solver CDCL macinano istanze industriali con milioni di variabili, perché le istanze reali hanno struttura sfruttabile.

**Commesso viaggiatore (TSP, versione decisionale)**
"Esiste un giro che visita tutte le città e torna a casa in meno di k km?" Verificare un giro proposto: sommi le distanze, fatto. Trovarlo: con 60 città i giri possibili superano il numero di atomi nell'universo. Applicazioni reali: logistica dei corrieri (UPS, Amazon), perforazione di circuiti stampati (il trapano è il "commesso", i fori le "città"), sequenziamento del genoma. In pratica si vive benissimo con euristiche (Lin-Kernighan) e solver esatti come Concorde che risolvono istanze con decine di migliaia di città — ottimizzati, non garantiti veloci su *ogni* input.

**Zaino (Knapsack)**
Hai uno zaino da 15 kg e oggetti con peso e valore: quale sottoinsieme massimizza il valore senza sforare? Versioni reali: selezione di progetti con budget limitato, caricamento di container, allocazione di banda. NP-completo, ma con una sfumatura elegante: esiste un algoritmo pseudo-polinomiale O(n·W) — efficiente se i pesi sono numeri piccoli, esponenziale nella *lunghezza in bit* dei pesi. Insegna che "dimensione dell'input" va misurata in bit, non in valore.

**Colorazione di grafi (k-coloring)**
Oltre agli usi delle slide (compilatori: i registri della CPU sono i colori, le variabili i nodi, due variabili vive contemporaneamente sono collegate), c'è l'assegnazione di frequenze alle antenne (celle vicine non possono usare la stessa frequenza) e la compilazione degli orari scolastici (due corsi con studenti in comune non possono avere lo stesso slot: gli slot sono i colori). Verificare una colorazione è banale; decidere se bastano 3 colori è NP-completo — mentre con 2 colori è in P (basta controllare che il grafo sia bipartito). Ancora un confine 2/3.

**Subset sum e partizione**
"Da questi importi bancari, un sottoinsieme somma esattamente a 10.000 €?" Usato in audit e anti-frode (riconciliare transazioni), ed è la base di alcuni crittosistemi storici. La variante "partizione" — dividere un insieme in due metà di somma uguale — è il problema NP-completo più semplice da enunciare: lo capisce un bambino, non lo risolve nessuno in tempo polinomiale garantito.

**Cammino/ciclo hamiltoniano**
Esiste un cammino che tocca ogni nodo *esattamente una volta*? Contrasto istruttivo col ciclo *euleriano* (toccare ogni *arco* una volta): quello è in P — Eulero lo risolse con un criterio sui gradi dei nodi nel 1736. Cambiare "archi" con "nodi" fa saltare il problema da P a NP-completo. Due problemi che sembrano gemelli, distanza abissale.

**Job scheduling / makespan**
Distribuire n job su k macchine minimizzando il tempo di completamento totale. È il pane quotidiano di ogni scheduler: Kubernetes che piazza i pod sui nodi, i job Spark sui worker, le catene di montaggio. NP-hard già con 2 macchine identiche. In pratica: euristiche greedy (longest processing time first) con garanzie di approssimazione — la soluzione trovata è al più 4/3 dell'ottimo, dimostrabilmente.

**Clique e independent set**
"In questo social network esiste un gruppo di 50 persone tutte amiche tra loro?" (clique) — usato in analisi di reti sociali, bioinformatica (trovare gruppi di proteine che interagiscono tutte), individuazione di comunità. Il duale, l'independent set (nessuno collegato a nessuno), modella la selezione di elementi mutuamente incompatibili. Entrambi NP-completi, e tra i più duri anche da *approssimare*.

**Vertex cover**
Piazzare il minimo numero di telecamere agli incroci in modo che ogni strada sia sorvegliata da almeno un estremo. NP-completo, ma con un'approssimazione facilissima: prendi gli archi uno a uno e copri entrambi gli estremi — ottieni al più il doppio dell'ottimo. Esempio perfetto di come si "convive" con l'NP-completezza: rinunci all'ottimo, ti tieni una garanzia.

**Bin packing**
Impacchettare oggetti di varie dimensioni nel minor numero di contenitori: container navali, allocazione di VM sui server fisici (il cloud è un gigantesco bin packing), taglio di barre d'acciaio minimizzando gli sprechi. NP-hard; l'euristica first-fit-decreasing usa al più ~22% di contenitori in più dell'ottimo.

**Steiner tree**
Dalle slide: collegare un insieme di case a una rete elettrica al costo minimo, potendo aggiungere snodi intermedi. È esattamente il problema del progetto di reti in fibra ottica e dei chip VLSI (collegare i pin minimizzando il rame). La libertà di aggiungere punti intermedi è ciò che lo rende NP-hard — il problema senza snodi extra (minimum spanning tree) è in P con un greedy banale.

**Sudoku, e i puzzle in generale**
Il Sudoku n²×n² è NP-completo, e lo stesso vale per Campo Minato (versione consistenza), Kakuro, e molti altri. Non è un caso: un puzzle è divertente proprio quando verificare è facile ma risolvere richiede ingegno — i giochi enigmistici vivono *dentro* il divario P/NP. Se P = NP, in un certo senso, i puzzle smetterebbero di essere interessanti.

**Fattorizzazione (menzione d'onore, con una precisazione)**
Dato un numero di 2048 bit, trovarne i fattori primi. Sta in NP (il certificato sono i fattori: moltiplichi e verifichi), ma *non è noto* essere NP-completo — probabilmente è un problema "intermedio". È il caso pratico più pesante di tutti: la sicurezza di RSA, cioè di gran parte del commercio elettronico, si fonda sulla scommessa che fattorizzare sia fuori da P. Se P = NP (con algoritmi praticabili), la crittografia a chiave pubblica classica crolla. Nota: gli algoritmi quantistici (Shor) fattorizzano in tempo polinomiale, ma questo non risolve P vs NP — è un modello di calcolo diverso.

### Il quadro pratico: come si convive con l'NP-completezza

Che un problema sia NP-completo non significa arrendersi. L'industria usa quattro strategie, spesso combinate:

1. **Solver esatti su istanze strutturate** — SAT/SMT/ASP/MIP solver (clingo, Z3, CPLEX, Gurobi): esponenziali nel caso peggiore, ma le istanze reali hanno simmetrie e struttura che il solver sfrutta. È la via dei sistemi di verifica, configurazione, pianificazione.
2. **Approssimazione con garanzie** — accetti una soluzione entro un fattore dimostrato dall'ottimo (vertex cover ×2, makespan ×4/3, bin packing +22%).
3. **Euristiche e ricerca locale** — simulated annealing, algoritmi genetici, Lin-Kernighan: nessuna garanzia, ottimi risultati empirici. È la via della logistica reale.
4. **Casi speciali e parametri** — molti problemi NP-completi diventano polinomiali su input ristretti (colorazione su grafi bipartiti, TSP su punti allineati) o trattabili quando un parametro è piccolo (complessità parametrizzata: vertex cover con k piccolo si risolve in O(2ᵏ·n)).

La teoria dice *dove* è il muro; l'ingegneria decide *come aggirarlo*.

## 15. La prospettiva storica e divulgativa (dall'articolo "I limiti dell'elaborazione computerizzata")

Il secondo documento integra le slide con la storia della questione, esempi di sapore quotidiano e una riflessione sulle conseguenze. Ne vale la pena, perché aggiunge tre cose che nelle slide mancano: le origini, un esempio di problema *dimostrato* esponenziale, e la chiusa sulle euristiche.

### Le origini: la lettera di Gödel a von Neumann (1956)

La prima formulazione della questione P=NP non è di Cook: è in una **lettera del 1956 di Kurt Gödel a John von Neumann**, riscoperta solo decenni dopo. Gödel — il logico dell'incompletezza — vi descriveva in sostanza il problema: se un procedimento di verifica è veloce, quanto può costare la ricerca della soluzione? Il fatto che l'idea sia germogliata nella corrispondenza tra i due giganti della logica del Novecento non è un caso: P vs NP è l'erede computazionale delle domande sulla dimostrabilità.

La questione entrò ufficialmente nella comunità scientifica nel **1971 con Stephen Cook** e subito dopo con **Dick Karp**, e fu chiaro fin dall'inizio che la soluzione richiedeva strumenti matematici superiori a quelli dell'epoca — i pessimisti ci videro giusto. Nel **2000 l'Istituto Matematico Clay** l'ha inserita tra i sette *problemi del millennio*, un milione di dollari ciascuno. Dei sette, solo la congettura di Poincaré è stata risolta (Perel'man, 2002, che peraltro rifiutò il premio); gli altri sei, P=NP incluso, restano aperti.

### L'algoritmo conta più dell'hardware: il residente più anziano

L'articolo costruisce la nozione di efficienza con un esempio d'anagrafe: trovare il residente più longevo tra n abitanti di un Comune. Due ditte propongono due algoritmi, entrambi corretti:

1. **Quadratico** — confronta r₁ con tutti gli altri (n−1 confronti); se non è lui il più anziano, passa a r₂ e riconfronta con tutti, e così via. Nel caso peggiore: n×(n−1) confronti.
2. **Lineare** — mantiene il "più anziano corrente": scorre i residenti una volta sola, confrontando ciascuno solo col campione in carica. Totale: n−1 confronti.

Su un Comune di 1000 abitanti: circa **un milione di confronti contro mille**. E la preferenza per il secondo vale *indipendentemente dalla potenza del computer* — è questa l'idea che l'accezione comune di "informatica" si perde: la disciplina non studia solo *come* risolvere i problemi, ma il **modo più efficiente possibile** di risolverli. La qualità è nell'algoritmo, non nel ferro.

L'articolo introduce poi il "lettore malizioso": ma che importa, se i computer fanno milioni di operazioni al secondo? Su n = 1000, in effetti, anche n³ resterebbe praticabile. È proprio questa osservazione a giustificare la definizione larga di P: tutte le complessità nᵏ, per qualunque costante k, vengono raggruppate come "trattabili". La distinzione che *non* perdona è quella con l'esponenziale — come mostra il prossimo esempio.

### Un problema dimostrato esponenziale: la sezione aurea generalizzata

Qui l'articolo aggiunge il tassello che alle slide manca: un problema **provatamente fuori da P**. Si parte dai pitagorici e dalla proporzione divina: esiste una lunghezza L con L² = 1 + L? (Sì: φ ≈ 1,618, la sezione aurea.) Generalizzando: date n incognite reali e un sistema di equazioni con somme e prodotti, con domande annidate del tipo "*esiste* L₁ tale che *per tutti* i valori di L₂ *esiste* L₃ tale che...", si può decidere automaticamente la risposta?

Sorprendentemente **sì** — questa teoria (l'aritmetica dei numeri reali con quantificatori, resa decidibile da Tarski) è algoritmicamente risolvibile. Ma i ricercatori hanno dimostrato un **limite invalicabile**: qualunque algoritmo risolutivo richiede almeno 2ⁿ operazioni, dove n conta incognite e operatori. Non "il miglior algoritmo noto è esponenziale": *ogni possibile* algoritmo lo è, per dimostrazione. Problemi così si dicono **intrinsecamente esponenziali** — e la sezione 12 del nostro riassunto li colloca: decidibili (stanno in R), ma dimostratamente fuori da P.

Sulla scala del disastro, l'articolo dà i numeri: 2¹⁰ ≈ mille, 2²⁰ ≈ un milione, 2³⁰ ≈ un miliardo — e con **n = 100, 2ⁿ supera la stima degli atomi che compongono la Terra**. Un computer che dovesse eseguire quel numero di operazioni impiegherebbe miliardi di miliardi di anni, per un input che in termini informatici è un'inezia. Soluzione teoricamente possibile, praticamente irraggiungibile.

### La "zona grigia": Number Partitioning e le squadre di calcio

Tra il bianco (polinomiale) e il nero (dimostrato esponenziale) c'è la **zona grigia**, ed è lì che vive la questione. L'esempio dell'articolo è delizioso: organizzare una partita di calcio tra n giocatori formando **due squadre perfettamente equilibrate** — a ogni giocatore un valore, e le due somme devono coincidere. (Con valori 9, 7, 3, 1: le squadre {9,1} e {7,3} pareggiano a 10.)

È il **Number Partitioning** — lo stesso problema "partizione" della nostra sezione 14, il più semplice da enunciare tra gli NP-completi. La soluzione naïve enumera le 2ⁿ divisioni possibili. E qui il limbo: nessuno ha mai trovato un algoritmo polinomiale, *ma nessuno ha mai dimostrato che non possa esistere*. A differenza della sezione aurea generalizzata, dove il muro esponenziale è un teorema, qui il muro potrebbe essere solo la nostra ignoranza. Questo limbo — problemi con verifica facile, risoluzione dallo status ignoto — è NP, ed è abitato da moltissimi problemi quotidiani: logistica, allocazione di risorse, protocolli crittografici.

*(Precisazione da tenere a mente rispetto al linguaggio dell'articolo: a rigore NP non è definito come "il limbo tra P ed esponenziale" — è definito dalla verificabilità polinomiale, e P ⊆ NP: i problemi facili stanno anch'essi in NP. Il "limbo" descrive bene i problemi NP-completi, la parte dura della classe. L'articolo divulga, le slide definiscono: le due letture combaciano tenendo presente questa sfumatura.)*

### I due comuni denominatori dei problemi in NP

L'articolo distilla ciò che accomuna gli abitanti del limbo, ed è la migliore formulazione intuitiva della definizione tramite certificati:

1. **Le soluzioni non sono mai oggetti "complicati"**: si rappresentano efficientemente in un calcolatore (una divisione in squadre, un'assegnazione, un giro di città — tutte cose compatte). È l'osservazione delle slide sugli spazi esponenziali fatti di oggetti piccoli.
2. **Se magicamente qualcuno ci porgesse una soluzione, sapremmo verificarla in tempo polinomiale**: per le squadre basta sommare i valori delle due formazioni e confrontare.

E il contrasto con gli intrinsecamente esponenziali diventa illuminante: per quelli, al crescere di n *la soluzione stessa* può diventare così complessa che perfino rappresentarla può essere irrealizzabile. In NP il collo di bottiglia è solo la *ricerca*; negli esponenziali veri può esserlo perfino la *risposta*.

### Cosa cambierebbe: i due mondi

- **Se P ≠ NP** (l'esito atteso): nella vita quotidiana cambierebbe poco — vivremmo nel mondo in cui già crediamo di vivere, con in più la certezza.
- **Se P = NP**: il mondo sarebbe sensibilmente diverso. Da un lato **la crittografia crollerebbe**: i protocolli che proteggono gli acquisti in rete si fondano sul fatto che forzarli richieda ~2ⁿ passi — basta una password lunga per trasformare l'attacco in miliardi di anni; con P = NP quella garanzia evapora. Dall'altro, moltissimi problemi oggi intrattabili diventerebbero facili quanto cercare il residente più anziano: un balzo di automazione con ripercussioni straordinarie. Computer "più intelligenti" non in potenza di calcolo, ma **nella qualità intrinseca di ciò che sanno calcolare**. Per questo, chiosa l'articolo, la risposta vale ben più del milione di dollari del Clay.

L'articolo registra anche un fatto sociologico interessante: l'intuizione "creare è più difficile che verificare" spinge quasi tutti verso P ≠ NP, ma i tentativi di formalizzarla si schiantano su questioni tecniche durissime — al punto che alcuni ricercatori autorevoli cominciano ad argomentare che la direzione giusta da esplorare potrebbe essere quella, contro-intuitiva, di un mondo in cui P = NP.

### La chiusa: i bambini e i capisquadra

Il finale dell'articolo è il più bello. Dividere i giocatori in squadre equilibrate è NP-completo — ma nessuno l'ha detto ai bambini, che lo risolvono da sempre: **due capisquadra scelgono a turno**, e il risultato è quasi sempre soddisfacente. Hanno scoperto una via pratica per aggirare il limbo?

In un certo senso sì: quella dei bambini è un'**euristica greedy** (è parente stretta del "longest processing time first" della nostra sezione 14 sullo scheduling) — niente garanzia di ottimo esatto, ottimo comportamento tipico. È la sintesi perfetta del rapporto tra teoria e pratica che attraversa tutto questo documento: l'NP-completezza parla del caso peggiore e della soluzione *esatta*; la vita reale si accontenta spesso di soluzioni ottime-quasi-sempre o quasi-ottime-sempre, e lì le euristiche prosperano. "Ma questa," come dice l'articolo, "è un'altra storia" — è la storia degli algoritmi di approssimazione e della ricerca locale, il modo in cui l'umanità convive ogni giorno con un muro che non sa se esista.



## 16. NP-completezza e NP-hardness, spiegate nello stile dell'articolo

L'articolo si ferma sulla soglia del limbo: ci mostra che Number Partitioning ci vive, insieme a moltissimi problemi di logistica, allocazione e crittografia, ma non ci dice la cosa più sorprendente su quel limbo — che i suoi abitanti più difficili sono, in un senso preciso, *tutti lo stesso problema travestito*. È l'idea di NP-completezza, e si costruisce in tre passi.

### Passo 1 — La riduzione: "il tuo problema è il mio problema"

Riprendiamo le squadre di calcio. Supponiamo che una ditta ci venda una scatola nera che risolve *un altro* problema, per esempio Subset Sum: "dato un insieme di numeri e un obiettivo t, esiste un sottoinsieme che somma esattamente a t?". Possiamo usarla per le nostre squadre?

Sì, con un travestimento: se i valori dei giocatori sommano complessivamente a S, allora due squadre equilibrate esistono *se e solo se* esiste un sottoinsieme che somma a S/2 (una squadra fa S/2, l'altra prende il resto, che vale anch'esso S/2). Coi giocatori 9, 7, 3, 1: la somma è 20, chiediamo alla scatola "c'è un sottoinsieme che fa 10?" — risponde sì ({9,1} o {7,3}), e abbiamo le formazioni.

Questo travestimento si chiama **riduzione** (polinomiale): una traduzione veloce che trasforma ogni istanza del problema A in un'istanza del problema B *preservando la risposta*. Se so risolvere B, so risolvere A: mi basta tradurre e interrogare. È lo stesso schema visto nella sezione 10 con DOMINO → MATCHING, e la freccia va letta come una **graduatoria di difficoltà**: se A si riduce a B, allora B è *almeno altrettanto difficile* di A — perché dentro B c'è A, sotto mentite spoglie.

### Passo 2 — NP-hard: il problema che li contiene tutti

Ora l'idea audace. E se esistesse un problema B a cui si riduce *non uno, ma ogni* problema del limbo — anzi, ogni problema di tutta NP, facili compresi? Un problema del genere sarebbe una specie di ricettacolo universale: risolvi lui, hai risolto tutto.

Un problema con questa proprietà si dice **NP-hard** (NP-arduo): *ogni* problema in NP si riduce a lui in tempo polinomiale. Attenzione al significato del nome, perché inganna: NP-hard non descrive quanto tempo richiede il problema — descrive la sua *posizione* nella graduatoria delle riduzioni. Dice: "questo problema sta sopra (o alla pari di) tutti quelli di NP". Sopra quanto? Anche molto sopra: la definizione non richiede che un problema NP-hard stia *dentro* NP. Il problema della fermata è NP-hard — ogni problema di NP vi si riduce — pur essendo addirittura indecidibile. E le versioni di *ottimizzazione* dei problemi del limbo ("trova il giro più corto", non "esiste un giro sotto k?") sono tipicamente NP-hard senza essere, formalmente, in NP (non sono nemmeno domande sì/no).

### Passo 3 — NP-completo: dentro il limbo, e in cima al limbo

Un problema **NP-completo** soddisfa entrambe le condizioni:

1. sta **in NP** — le sue soluzioni sono oggetti semplici, verificabili in tempo polinomiale (i due denominatori comuni dell'articolo);
2. è **NP-hard** — ogni problema di NP si riduce a lui.

In una riga: **NP-completo = NP ∩ NP-hard** — il più difficile *tra* i problemi del limbo, ma ancora *dentro* il limbo. Sono i vertici della classe: più su di loro, dentro NP, non si può andare.

Che problemi del genere *esistano* non è ovvio per niente — è il **teorema di Cook-Levin** (1971, lo stesso Cook dell'articolo): SAT è NP-completo. La dimostrazione, raccontata nella sezione 13, codifica in clausole booleane la computazione di un qualunque verificatore: è il momento in cui si scopre che una formula logica può simulare *qualsiasi* verifica efficiente. Subito dopo (1972), **Karp** mostrò che la proprietà è contagiosa: ridusse SAT a 21 problemi concreti — tra cui partizione, clique, colorazione, cammino hamiltoniano — dimostrandoli tutti NP-completi. Il trucco è che la riduzione è *transitiva*: se tutto NP si riduce a SAT, e SAT si riduce a Number Partitioning, allora tutto NP si riduce a Number Partitioning. Per dimostrare che un nuovo problema è NP-completo non serve rifare la fatica di Cook: basta (a) mostrare che sta in NP e (b) ridurgli *un* problema già noto come NP-completo. Da 21 il catalogo è cresciuto a migliaia — le squadre di calcio dell'articolo, il Sudoku delle slide, il TSP, lo scheduling: tutti lì dentro.

### Cosa cambia, concretamente

**L'effetto domino.** L'intera classe NP-completa vive o muore insieme. Se domani qualcuno trovasse un algoritmo polinomiale anche per uno solo di questi problemi — uno qualunque, magari il più innocuo — le riduzioni lo propagherebbero istantaneamente a tutti gli altri e a tutta NP: P = NP, la crittografia crolla, il limbo si svuota. Viceversa, se si dimostrasse che uno solo richiede tempo superpolinomiale, P ≠ NP e il limbo è reale per tutti. La questione del millennio non è mille domande: è *una* domanda con mille facce.

**Il senso pratico della cattiva notizia.** Nell'articolo, di Number Partitioning si dice: "nessuno ha trovato un algoritmo polinomiale, né ha dimostrato che non esista". Detta così, potrebbe sembrare che il *tuo* problema sia semplicemente poco studiato — magari l'algoritmo furbo c'è e nessuno l'ha cercato abbastanza. La NP-completezza cambia radicalmente il peso di questa ignoranza: dimostrare che il tuo problema è NP-completo significa dimostrare che un tuo eventuale algoritmo polinomiale risolverebbe *anche* SAT, il TSP, la colorazione, e ogni altro problema su cui migliaia di ricercatori si sono rotti i denti per mezzo secolo. Non è una prova d'impossibilità — quella varrebbe il milione del Clay — ma è la più forte evidenza di difficoltà che l'informatica sappia offrire. È anche un'informazione *operativa*: appurato che il problema è NP-completo, si smette di cercare l'algoritmo esatto veloce che quasi certamente non c'è, e si passa con la coscienza pulita alle strategie della sezione 14 — solver su istanze strutturate, approssimazioni con garanzia, euristiche come i capisquadra dei bambini.

**La lettura positiva.** L'universalità taglia anche nell'altro verso, ed è il segreto industriale della sezione 13: se ogni problema di NP si riduce a SAT, allora un *buon solver* per SAT è automaticamente una macchina universale per tutto il limbo. Le riduzioni, nate come strumento per dimostrare difficoltà, sono diventate il canale con cui i problemi reali vengono convogliati verso i motori CDCL. La stessa freccia, percorsa da teorici e ingegneri in direzioni opposte.

### La mappa finale del limbo

Mettendo insieme articolo e slide, la geografia (nell'ipotesi P ≠ NP, quella creduta) è questa:

| Zona | Chi ci abita | Status |
|---|---|---|
| **P** | residente più anziano, cammino minimo (il navigatore), matching | facili, dimostrato |
| **NP ∖ P, non completi** | fattorizzazione (probabilmente), isomorfismo di grafi | i "sospetti intermedi": in NP, non si sa se facili, non dimostrati completi |
| **NP-completi** | SAT, Number Partitioning/le squadre, Sudoku, TSP decisionale, colorazione | i vertici del limbo: tutti equivalenti tra loro, tutti duri se uno lo è |
| **NP-hard fuori da NP** | TSP di ottimizzazione, QBF/PSPACE, fino al problema della fermata | più difficili dell'intero limbo, alcuni perfino indecidibili |

Nota il piano intermedio, spesso dimenticato: se P ≠ NP, un teorema di Ladner garantisce che esistono problemi in NP *né* facili *né* NP-completi. La fattorizzazione — proprio quella su cui poggia RSA — è la principale indiziata: sta in NP, nessuno sa risolverla in fretta, ma nessuno è mai riuscito a dimostrarla NP-completa. Il limbo dell'articolo, a guardarlo da vicino, ha una sua stratigrafia interna — ed è su uno di questi strati incerti, non sul pavimento né sui vertici, che è appoggiata la sicurezza dei nostri acquisti online.



## 17. NP-hard sotto la lente: quale "polinomiale" conta?

Nella definizione di NP-hard si annidano due possibili "polinomiale", e confonderli è l'errore più comune di tutta la materia. Mettiamoli a fuoco.

**Definizione esatta:** B è NP-hard se ogni problema A in NP si riduce a B **tramite una riduzione calcolabile in tempo polinomiale**.

Il polinomiale della definizione riguarda la **riduzione** — cioè la traduzione da A a B — e *non* la verifica delle soluzioni di B:

1. **La traduzione dev'essere polinomiale.** Questo requisito non è pignoleria: se la traduzione potesse costare tempo esponenziale, la definizione si svuoterebbe — si potrebbe "ridurre" qualunque cosa a qualunque cosa risolvendo A per forza bruta *durante* la traduzione e producendo un'istanza banale di B. La riduzione dev'essere così economica da non poter nascondere lavoro al suo interno: deve solo *tradurre*, mai *risolvere*.
2. **La verifica polinomiale non c'entra con l'hardness.** È la condizione separata "B ∈ NP". Ed è per questo che il problema della fermata può essere NP-hard pur essendo indecidibile: le riduzioni *verso* di lui sono polinomiali, ma lui non ha alcuna verifica.

La mappa dei "polinomiale" nelle tre nozioni:

| Nozione | Cosa deve essere polinomiale |
|---|---|
| B ∈ **NP** | la **verifica** di una soluzione di B, dato il certificato |
| B è **NP-hard** | le **riduzioni** da ogni problema di NP verso B |
| B è **NP-completo** | entrambe |

Un criterio per non confonderle mai più: la verifica è una proprietà **interna** di B (parla di come sono fatte le sue soluzioni); la riducibilità è una proprietà **relazionale** (parla della posizione di B rispetto agli altri problemi). NP guarda *dentro* il problema; NP-hard guarda le *frecce* che gli arrivano addosso.

I due polinomiali giocano poi di squadra, ed è il motore di tutta la teoria: se B fosse risolvibile in tempo polinomiale, ogni A ∈ NP si risolverebbe con traduzione polinomiale + soluzione polinomiale di B — e polinomio composto con polinomio resta polinomio, quindi P = NP. La catena regge proprio perché la riduzione è economica: è il suo essere polinomiale a garantire che tutta la difficoltà stia in B e non si sia annidata nella traduzione. In questo senso preciso si dice che B "contiene" la difficoltà di NP.

## 18. Come si dimostra che un problema è NP-hard

A prima vista sembra impossibile: la definizione quantifica su *infiniti* problemi ("ogni A in NP..."), compresi quelli non ancora inventati. Le strade sono esattamente due, e la storia le ha percorse in quest'ordine.

### Strada 1 — Da zero, attaccando lo stampo (fatta una volta sola: Cook, 1971)

Non conosci tutti i problemi di NP, ma conosci la loro **forma comune**: ogni A ∈ NP ha, per definizione, un verificatore V che gira in tempo polinomiale p(n). E una macchina che gira per p(n) passi è un oggetto finito e meccanico — una griglia p(n) × p(n) (tempo × nastro) in cui ogni riga discende dalla precedente per regole *locali*. Cook mostrò come scrivere clausole booleane che affermano "questa griglia è una computazione valida di V che accetta": la formula è soddisfacibile se e solo se esiste un certificato accettante, cioè se e solo se l'istanza è un sì.

Il punto cruciale: la costruzione non usa *nulla* dello specifico problema A — usa solo il fatto che A ha un verificatore, cioè la definizione stessa di NP. È una riduzione-schema che funziona per ogni membro presente e futuro della classe: appena dimostri che un problema nuovo sta in NP, gli hai dato un verificatore, e la macchina di Cook lo tritura in SAT. Ecco come si quantifica sull'infinito: non problema per problema, ma colpendo lo stampo da cui tutti escono.

### Strada 2 — Per contagio, via transitività (tutte le altre migliaia di volte)

Fatto il lavoro sporco una volta, nessuno lo rifà. Per dimostrare che il tuo problema B è NP-hard basta:

> prendere **un** problema già noto NP-hard (tipicamente 3-SAT) e costruire **una** riduzione polinomiale **dal problema noto verso B**.

La logica: ogni A ∈ NP → (Cook) si riduce a 3-SAT → (la tua riduzione) si riduce a B; due traduzioni polinomiali in fila restano polinomiali, quindi tutto NP arriva a B. Un solo anello nuovo aggancia il tuo problema all'intera catena.

**La direzione — l'errore classico.** Per dimostrare B difficile devi ridurre *noto-difficile → B*: mostrare che B sa "ospitare" 3-SAT travestito. La riduzione opposta B → 3-SAT non dimostra nulla sulla difficoltà di B (direbbe solo che B non è *più* difficile di 3-SAT — cosa vera anche per i problemi facili, visto che a un completo si riduce tutta NP). Mnemonico: **la difficoltà scorre lungo la freccia** — se il duro entra in B, B è duro.

### Il mestiere: i gadget (esempio completo, 3-SAT → Independent Set)

In pratica le riduzioni si costruiscono coi **gadget**: componenti del problema di destinazione che simulano i meccanismi del problema sorgente. Esempio classico e verificabile a mente — Independent Set chiede: "esistono k nodi a due a due non collegati?"

- Per ogni clausola (x ∨ ¬y ∨ z) si crea un **triangolo** di 3 nodi etichettati coi letterali. Dentro un triangolo si può scegliere al più un nodo → gadget "scegli quale letterale rende vera questa clausola".
- Si collega con un arco ogni coppia di nodi **contraddittori** (uno etichettato x, l'altro ¬x) tra triangoli diversi → gadget "non puoi rendere vero un letterale e il suo opposto".
- Si chiede un independent set di taglia k = numero di clausole.

Le due direzioni della correttezza: se φ è soddisfacibile, prendendo da ogni triangolo un letterale vero si ottengono k nodi senza archi tra loro; viceversa, un independent set di taglia k tocca ogni triangolo esattamente una volta e non contiene coppie contraddittorie, quindi vi si legge un'assegnazione che soddisfa φ. La traduzione è evidentemente polinomiale (3m nodi, archi in numero quadratico). Conclusione: Independent Set è NP-hard; poiché sta anche in NP (certificato: i k nodi), è NP-completo.

Tutte le migliaia di dimostrazioni di NP-hardness sono variazioni di questo artigianato: si sceglie il problema sorgente più affine al proprio (subset sum per i problemi numerici, hamiltoniano per quelli di percorso, 3-SAT per quasi tutto il resto) e si inventano gadget che ne simulino scelte e vincoli. I 21 problemi di Karp (1972) furono la prima ondata di questo contagio; da allora ogni problema NP-completo del catalogo ha un pedigree di riduzioni che risale, anello dopo anello, fino a Cook e alla macchina di Turing codificata in clausole.

## Idee chiave da portare a casa

1. **Efficiente = polinomiale** per convenzione (tesi di Cobham-Edmonds), pur con casi limite formalmente paradossali.
2. **P** = risolvere in fretta; **NP** = verificare in fretta un certificato (equivalentemente: risolvere in fretta con nondeterminismo).
3. Gli spazi di ricerca esponenziali con candidati piccoli e verificabili sono la firma tipica dei problemi in NP.
4. **P ⊆ NP** è un fatto; **P = NP?** è la domanda aperta più importante dell'informatica teorica.
5. Le **riduzioni** permettono di riciclare algoritmi polinomiali tra problemi diversi — e prepareranno il terreno per la NP-completezza.
6. **L'efficienza è una proprietà dell'algoritmo, non dell'hardware**: n(n−1) contro n−1 confronti resta un abisso su qualunque macchina (l'esempio del residente più anziano).
7. Esistono problemi **dimostrati** intrinsecamente esponenziali (come la teoria dei reali con quantificatori): per quelli non c'è speranza; per quelli in NP il muro potrebbe essere solo ignoranza — è tutta qui la differenza tra un teorema e una congettura.
8. Se P = NP: crolla la crittografia, ma i computer diventano qualitativamente più capaci; se P ≠ NP: il mondo resta com'è, con una certezza in più.
9. Le **euristiche** (i bambini coi capisquadra) convivono felicemente con l'NP-completezza: la teoria parla del caso peggiore esatto, la pratica si accontenta del quasi-ottimo quasi-sempre.
10. **NP-hard** = posizione, non velocità: "sopra tutto NP" nella graduatoria delle riduzioni. **NP-completo** = NP-hard *e* dentro NP: i vertici del limbo, tutti equivalenti tra loro — ne cade uno, cadono tutti (e P = NP).
11. In NP-hard il "polinomiale" è quello della **riduzione** (proprietà relazionale: le frecce in arrivo), non della verifica (proprietà interna, che definisce NP). La riduzione dev'essere economica proprio perché non possa nascondere lavoro: solo tradurre, mai risolvere.
12. L'NP-hardness si dimostra **una volta da zero** (Cook: codificare il verificatore generico in clausole — si attacca lo stampo, non i singoli problemi) e **poi per contagio**: riduzione da un problema noto-difficile *verso* il tuo, costruita a gadget. La difficoltà scorre lungo la freccia.
