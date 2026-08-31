# Reasoning — bibliografia ragionata

*Documento di riferimento unico. Tre campi (filosofia, scienze cognitive, AI) organizzati per domande condivise, non per disciplina.*

---

## 0. Come è costruito questo documento

### Il criterio di inclusione

Un lavoro entra se soddisfa almeno uno di questi:

1. **introduce una distinzione** che, una volta vista, non si può più non vedere;
2. **falsifica** qualcosa che si sarebbe altrimenti dato per scontato;
3. **è un ponte** tra due campi che si citano poco.

Non entra un lavoro solo perché è famoso, o perché "copre" un'area. Una bibliografia sul reasoning senza criterio di esclusione arriva a 400 voci in due settimane e diventa inutilizzabile. Questo criterio è restrittivo di proposito.

### Lo schema di annotazione

Per i lavori portanti:

- **Claim** — la tesi centrale in una frase.
- **Tipo di evidenza** — teorica / comportamentale / correlazionale / causale.
- **Autorizza a dire** —
- **Non autorizza a dire** — *il campo che tutti saltano ed è l'unico che serve davvero sei mesi dopo.*
- **Perché è qui** — quale distinzione porta.

Per i lavori di contorno, una riga.

### Portanti vs. stato dell'arte

Distinguo due strati:

- **Strato portante** (per lo più pre-2024): stabile. Si legge una volta, si rilegge dopo anni, non decade.
- **Strato di stato dell'arte** (2024–2026): decade in 12–18 mesi. Va rivisto periodicamente, e va letto sapendo che sta rispondendo a una configurazione contingente di modelli.

Il rapporto sano è circa 70/30 a favore del portante. La tentazione è l'inverso.

---

## 1. Il problema preliminare: "reasoning" è un omonimo

Almeno dieci programmi di ricerca usano la parola per riferirsi a cose diverse. Non si citano quasi mai a vicenda. Prima di leggere qualsiasi cosa, conviene sapere in quale senso è usata.

| Senso | Domanda | Metro di successo | Campo | Nucleo |
|---|---|---|---|---|
| **Normativo** | Cosa *conta* come inferenza valida | Correttezza rispetto a una semantica | Logica, filosofia | A |
| **Descrittivo** | Come ragionano *di fatto* gli umani | Fit con i dati sperimentali | Psicologia cognitiva | B |
| **Culturale** | Il formato esplicito è pensiero o pratica appresa? | Variazione fra popolazioni e specie | Antropologia, cognizione comparata | C |
| **Strutturale** | Le combinazioni nuove sono gestite? | Split compositivi | Ling. formale, cog sci, ML | D |
| **Computazionale** | Quale classe di funzioni è esprimibile? | Teoremi | Teoria della complessità | E |
| **Intrinseco al problema** | Quanto è lunga la dimostrazione più corta? | Lower bound | Proof complexity | F |
| **Comportamentale** | Un sistema risolve il task? | Accuracy su benchmark | ML applicato | G |
| **Riportato** | La spiegazione verbalizzata corrisponde al processo? | Faithfulness | Interpretabilità / cog sci | H |
| **Meccanicistico** | Quale algoritmo è implementato? | Interventi causali | Mech interp | I |
| **Implementativo** | Quale sostrato fisico realizza l'inferenza? | Correlati e interventi neurali | Comp. neuroscience | J |
| **Procedurale** | Ricerca nello spazio degli stati | Ottimalità del piano | GOFAI, planning | (fuori) |

Quasi tutti i disaccordi pubblici su "gli LLM ragionano?" sono disaccordi su quale riga guardare. Chi dice sì guarda la riga comportamentale; chi dice no guarda quella computazionale o quella meccanicistica. Il dibattito non si risolve perché non è lo stesso dibattito.

**L'ordinamento sottostante è marriano.** Le righe non sono una lista piatta: si dispongono sui tre livelli di Marr (1982) — computazionale (cosa viene risolto e perché: normativo, intrinseco al problema, computazionale), algoritmico (con quale procedura e quale rappresentazione: descrittivo, strutturale, comportamentale, meccanicistico), implementativo (in quale sostrato: implementativo). Le righe *culturale* e *riportato* sono trasversali, perché riguardano il rapporto fra il sistema e la sua descrizione pubblica anziché il sistema. Vedi J.1: è la distinzione singola più utile del documento, ed è collocata in fondo solo per ragioni di provenienza disciplinare.

**Corollario pratico:** ogni volta che leggi un claim su "reasoning", chiediti quale riga e quale livello. È un esercizio che dopo un mese diventa automatico e cambia radicalmente cosa riesci a estrarre dai paper.

---

## 2. Nucleo A — Il metro normativo

> **Domanda:** cosa rende un'inferenza buona? E la logica è la risposta?

Questo nucleo serve a possedere un metro. Senza, non si può dire che un sistema *sbaglia*: si può solo dire che diverge da qualcosa.

### A.1 — Il lavoro che smonta l'assunzione di partenza

**Gilbert Harman, *Change in View: Principles of Reasoning* (1986).**

- **Claim:** la logica deduttiva non è, e non può essere, una teoria del ragionamento. La logica è una teoria della relazione di implicazione tra proposizioni; il ragionamento è un processo di revisione delle credenze nel tempo, sotto vincoli di risorse. Sono due oggetti diversi.
- **Tipo di evidenza:** argomentativa/concettuale.
- **Autorizza a dire:** che "il sistema non segue le regole della logica classica" non è di per sé un'accusa di irrazionalità.
- **Non autorizza a dire:** che le norme logiche siano irrilevanti — Harman non è un relativista sulla validità.
- **Perché è qui:** è il correttivo alla tentazione più forte del campo, cioè trattare la logica come specifica del comportamento desiderato. Se lo leggi per primo, tutto il resto si legge meglio. È anche il testo meno letto in proporzione alla sua importanza.

**L'argomento chiave, in breve:** se credi P e P implica Q, la logica dice che P→Q. Non dice che *devi* credere Q. Forse la cosa razionale è abbandonare P. La logica non ha risorse per dirti quale delle due. Il ragionamento sì. E la chiusura deduttiva è intrattabile: nessun agente reale può credere tutte le conseguenze delle sue credenze.

### A.2 — Non-monotonicità

Il ragionamento reale ritratta conclusioni quando arrivano nuove premesse. La logica classica no. Da qui un intero campo.

- **McCarthy (1980), *Circumscription*.** Minimizzare le anomalie.
- **Reiter (1980), *A Logic for Default Reasoning*.** Le default rules e il problema delle estensioni multiple.
- **Gelfond & Lifschitz (1988), *The Stable Model Semantics for Logic Programming*.** La base di ASP.
- **Kraus, Lehmann & Magidor (1990), *Nonmonotonic Reasoning, Preferential Models and Cumulative Logics*.** La caratterizzazione assiomatica: quali proprietà strutturali *deve* avere una relazione di conseguenza non-monotona. Sistema P.

**Perché conta qui:** KLM dà una risposta di forma insolita — non "ecco il sistema giusto" ma "ecco i vincoli che qualunque sistema ragionevole deve rispettare". È il tipo di risultato che manca completamente nella letteratura sul reasoning nei LLM, dove non esiste una caratterizzazione assiomatica di cosa dovrebbe fare un sistema che ragiona in modo defeasible.

**Non autorizza a dire:** che i sistemi non-monotoni siano modelli psicologici. Sono normativi. La confusione tra i due usi è frequente.

### A.3 — Abduzione e induzione

- **C. S. Peirce**, sull'abduzione come terza forma inferenziale (le *Collected Papers*; per un ingresso, la voce SEP su abduction). L'abduzione genera ipotesi, non le giustifica.
- **Peter Lipton, *Inference to the Best Explanation* (1991, 2ª ed. 2004).** Cosa rende una spiegazione "migliore"? La risposta di Lipton — *loveliness* vs. *likeliness* — è direttamente rilevante alla faithfulness: una traccia di ragionamento può essere *lovely* (spiega bene) senza essere *likely* (è ciò che è successo).
- **Nelson Goodman, *Fact, Fiction, and Forecast* (1955).** Il nuovo enigma dell'induzione, "grue".

**Su Goodman, con enfasi:** il problema *grue* è esattamente il problema della generalizzazione OOD, formulato trent'anni prima che diventasse un problema ingegneristico. Ogni insieme finito di dati è compatibile con infinite generalizzazioni; ciò che seleziona quella "giusta" non è nei dati. Nel ML questo si chiama inductive bias. Chi lavora sulla generalizzazione compositiva e non ha letto Goodman continuerà a formulare come scoperta empirica una cosa che è un vincolo strutturale.

### A.4 — Causalità

- **Judea Pearl, *Probabilistic Reasoning in Intelligent Systems* (1988)** — le reti bayesiane.
- **Judea Pearl, *Causality* (2000, 2ª ed. 2009)** — do-calculus, gerarchia associazione/intervento/controfattuale.
- **Pearl & Mackenzie, *The Book of Why* (2018)** — versione divulgativa, utile per fissare la gerarchia.

**Perché conta qui, in modo non ovvio:** la ladder di Pearl è la stessa distinzione che struttura la mech interp. Un probe lineare vive al primo gradino (associazione). L'activation patching vive al secondo (intervento). Il ragionamento su "cosa sarebbe successo se il circuito non ci fosse stato" vive al terzo. Il fatto che l'interpretabilità meccanicistica sia, formalmente, scienza causale applicata alle attivazioni è stato reso esplicito solo tardi (vedi Geiger, nucleo I).

### A.5 — Il frame problem

- **Daniel Dennett (1984), *Cognitive Wheels: The Frame Problem of AI*.**
- **Jerry Fodor, *The Mind Doesn't Work That Way* (2000).**

**Claim (Fodor):** i processi centrali del pensiero sono *isotropi* e *quineani* — qualunque credenza può essere rilevante per qualunque altra, e la conferma è olistica. Nessuna teoria computazionale locale può catturarli.

**Non autorizza a dire:** che sia impossibile. Fodor argomenta l'impossibilità *per una certa architettura* (computazione simbolica su rappresentazioni locali). I sistemi ad apprendimento profondo hanno una risposta diversa alla rilevanza — l'attenzione appresa — e se sia una soluzione o un aggiramento è genuinamente aperto. Ma il problema che risolvono è quello che Fodor ha nominato.

### A.6 — Norme argomentative

Se il ragionamento è, per funzione, produzione e valutazione di argomenti (vedi B.5), allora la deduzione è la norma sbagliata e ne serve un'altra.

- **Toulmin, *The Uses of Argument* (1958).** La struttura informale dell'argomento: claim, dati, warrant, backing, qualificatori, condizioni di rebuttal. La mossa importante è il *warrant* — la regola-ponte che autorizza il passaggio dai dati al claim, e che negli argomenti reali resta quasi sempre implicita.
- **Dung (1995), *On the Acceptability of Arguments and Its Fundamental Role in Nonmonotonic Reasoning, Logic Programming and n-Person Games*, AIJ.** Gli abstract argumentation frameworks: un grafo di attacchi fra argomenti, e semantiche (grounded, preferred, stable) che selezionano insiemi ammissibili.

**Perché è qui:** la semantica stable di Dung e la semantica dei modelli stabili di Gelfond & Lifschitz (A.2) sono formalmente imparentate — la corrispondenza è esplicita nel paper stesso. Se conosci ASP, hai già metà dell'apparato per una teoria formale dell'argomentazione, e questo è il modo di rendere non-vago il claim di Mercier & Sperber. La differenza importante rispetto alla deduzione: qui la conclusione è *accettabile* rispetto a un insieme di attacchi, non *vera* rispetto a un modello.

---

## 3. Nucleo B — Il ragionamento reale

> **Domanda:** cosa fanno effettivamente gli umani quando ragionano? E perché diverge sistematicamente dal metro?

Questo è il nucleo che la letteratura AI cita meno e da cui avrebbe più da guadagnare.

### B.1 — L'effetto contenuto

- **Wason (1966/1968), il selection task.** Meno del 10% risolve la versione astratta.
- **Cheng & Holyoak (1985), *Pragmatic Reasoning Schemas*.** La performance salta se il problema è inquadrato come permesso/obbligo.
- **Cosmides (1989), la versione contratto sociale / cheater detection.**
- **Griggs & Cox (1982)**, l'effetto del materiale familiare.

**La lezione, che è più profonda della singola task:** la performance inferenziale umana dipende dal *contenuto*, non solo dalla *forma*. Questo è precisamente ciò che una teoria formale del ragionamento dice non dovrebbe accadere.

**Ponte:** **Dasgupta et al. (2022), *Language Models Show Human-like Content Effects on Reasoning*.** Gli stessi pattern nei LLM. Se leggi questo paper senza aver letto Wason e Cheng & Holyoak, sembra un risultato carino. Se li hai letti, è un risultato sul *tipo* di sistema che gli LLM sono.

### B.2 — Il dibattito modelli vs. regole

- **Johnson-Laird, *Mental Models* (1983)** e **Johnson-Laird & Byrne, *Deduction* (1991).** Si ragiona costruendo e manipolando modelli semantici, non applicando regole sintattiche. La difficoltà predice il numero di modelli da tenere in memoria.
- **Rips, *The Psychology of Proof* (1994)** e **Braine & O'Brien** sulla mental logic. La replica: esiste un sistema di regole inferenziali naturali.

**Perché conta per te, specificamente:** questa è *strutturalmente la stessa domanda* di "il transformer implementa un algoritmo simbolico o simula un modello?". Il dibattito è durato vent'anni ed è utile sapere come è finito — non con una vittoria, ma con la constatazione che le due ipotesi erano meno distinguibili comportamentalmente di quanto sembrasse, e che servivano vincoli di implementazione per separarle. È l'argomento a favore dell'approccio meccanicistico, formulato prima che esistesse.

### B.3 — Euristiche, bias, e la loro riabilitazione

- **Tversky & Kahneman (1974), *Judgment under Uncertainty: Heuristics and Biases*, Science.**
- **Kahneman, *Thinking, Fast and Slow* (2011)** — utile come sintesi, da leggere sapendo che la letteratura sul priming al suo interno ha subito la replication crisis.
- **Evans & Stanovich (2013), *Dual-Process Theories of Higher Cognition: Advancing the Debate*.** La versione difendibile del dual-process, dopo le critiche.
- **Simon (1955/1956)** sulla razionalità limitata; **Gigerenzer & Todd (1999), *Simple Heuristics That Make Us Smart*.**
- **Oaksford & Chater, *Bayesian Rationality* (2007).**

**Su Oaksford & Chater, con enfasi:** la mossa è la più elegante del campo. Riformulano il selection task come problema di selezione ottimale dell'informazione (valore atteso dell'informazione) invece che come test di logica condizionale. Sotto questa funzione obiettivo, il comportamento "sbagliato" dei soggetti diventa ottimale.

- **Autorizza a dire:** che un pattern di errore rispetto a una norma può indicare che il sistema sta ottimizzando *un'altra* funzione obiettivo.
- **Non autorizza a dire:** che qualunque comportamento può essere razionalizzato scegliendo l'obiettivo giusto — questa è la critica standard (non-falsificabilità), e va tenuta presente.
- **Perché è qui:** è il template concettuale per ragionare sul comportamento dei LLM. "Il modello sbaglia la moltiplicazione" e "il modello ottimizza la next-token prediction, sotto la quale il suo comportamento è sensato" sono due descrizioni dello stesso fatto, e la seconda è più informativa.

### B.4 — Il testo che nessuno legge e che dovrebbe essere obbligatorio

**Stenning & van Lambalgen, *Human Reasoning and Cognitive Science* (2008).**

- **Claim:** ogni compito di ragionamento richiede due fasi distinte — *reasoning to an interpretation* (decidere cosa significa il problema, quale logica si applica, quali assunzioni di chiusura valgono) e *reasoning from an interpretation* (eseguire l'inferenza). Quasi tutti gli "errori" documentati dalla tradizione heuristics-and-biases sono errori attribuiti alla seconda fase che in realtà appartengono alla prima: i soggetti stanno risolvendo correttamente un problema diverso da quello che lo sperimentatore crede di aver posto.
- **Tipo di evidenza:** reinterpretazione formale (usano la logica non-monotona, in particolare la closed-world reasoning, come modello della fase interpretativa) più evidenza sperimentale.
- **Autorizza a dire:** che una discrepanza fra risposta e norma è ambigua fra fallimento di esecuzione e divergenza interpretativa, e che le due vanno separate sperimentalmente.
- **Non autorizza a dire:** che i soggetti non commettano mai errori esecutivi.
- **Perché è qui:** è il ponte più diretto e meno sfruttato verso il prompting e la valutazione dei LLM. Metà dei disaccordi su "il modello ha fallito il task" sono disaccordi su quale task il modello ha creduto di risolvere. Nel tuo caso specifico, la distinzione fra *format generalization* e *fallimento compositivo* è un'istanza di questa distinzione, riscoperta indipendentemente.

### B.5 — Introspezione e confabulazione

Questo sotto-nucleo è la radice concettuale diretta della letteratura sulla CoT unfaithfulness, e la seconda quasi non lo cita.

**Nisbett & Wilson (1977), *Telling More Than We Can Know: Verbal Reports on Mental Processes*, Psychological Review.**

- **Claim:** i report verbali sui propri processi cognitivi non derivano da accesso introspettivo ai processi, ma da teorie causali a priori su cosa plausibilmente li ha determinati. I soggetti riportano fluentemente ragioni per scelte determinate da fattori che dimostrabilmente non hanno rilevato (l'esperimento sull'effetto posizione nella scelta di collant è l'esempio canonico).
- **Tipo di evidenza:** comportamentale sperimentale, con manipolazione della causa reale.
- **Autorizza a dire:** che un report fluente e plausibile non costituisce evidenza di accesso al processo.
- **Non autorizza a dire:** che nessun report sia mai accurato — Nisbett e Wilson distinguono l'accesso al *contenuto* mentale (spesso disponibile) dall'accesso ai *processi* (tipicamente no).
- **Perché è qui:** è, parola per parola, la tesi di Turpin et al. (2023) trentasei anni prima, con un design sperimentale migliore. Il parallelo strutturale — manipolo la causa reale, verifico che il report non la menzioni — è identico.

**Michael Gazzaniga**, sull'*interpreter* dell'emisfero sinistro nei pazienti split-brain (vari lavori dagli anni '70; per una sintesi, *The Ethical Brain* o le rassegne). Il caso limite: un modulo che genera spiegazioni causali coerenti per azioni le cui cause reali gli sono fisicamente inaccessibili.

**Mercier & Sperber (2011), *Why Do Humans Reason? Arguments for an Argumentative Theory*, BBS** — e il libro, ***The Enigma of Reason*** (2017).

- **Claim:** il ragionamento esplicito non è evoluto per migliorare la cognizione individuale ma per produrre e valutare argomenti in contesti sociali. I bias documentati (confirmation bias in primis) sono funzionali sotto questo obiettivo, non difetti.
- **Perché è qui:** offre una spiegazione *funzionale* dell'unfaithfulness invece che una constatazione. Se il ragionamento verbalizzato è per default una produzione argomentativa post-hoc, la domanda interessante non è "perché la CoT è infedele?" ma "in quali condizioni diventa fedele?". Riformulazione utile.

### B.6 — Analogia e trasferimento

- **Gentner (1983), *Structure-Mapping: A Theoretical Framework for Analogy*.** L'analogia è allineamento di struttura relazionale, non di attributi superficiali.
- **Gick & Holyoak (1980, 1983)** sul transfer analogico: i soggetti non trasferiscono una soluzione a un problema strutturalmente identico se la copertura di superficie cambia, a meno di un hint esplicito.
- **Hofstadter & Sander, *Surfaces and Essences* (2013).**

**Perché conta:** Gick & Holyoak è il risultato umano più vicino alla domanda "una primitiva appresa in un contesto viene riusata in un contesto strutturalmente nuovo?". La risposta, negli umani, è: raramente e spontaneamente quasi mai, ma quasi sempre con uno scaffold minimo. La struttura del risultato — fallimento spontaneo, successo con hint — è esattamente la struttura di un design A/B/C.

**Il base rate, dalle learning sciences:**

- **Detterman & Sternberg (a cura di), *Transfer on Trial* (1993).** Il capitolo introduttivo di Detterman è la rassegna più pessimista e più onesta: il transfer lontano, in condizioni sperimentali controllate, quasi non si osserva.
- **Barnett & Ceci (2002), *When and Where Do We Apply What We Learn? A Taxonomy for Far Transfer*, Psychological Bulletin.** Nove dimensioni lungo cui il contesto può variare, il che rende "lontano" una nozione graduata invece che binaria.

**Uso corretto di questo sotto-nucleo:** come base rate, prima di formulare aspettative. La sorpresa che un transformer non trasferisca da addizione a moltiplicazione va calibrata sul fatto che gli umani trasferiscono molto meno di quanto l'intuizione suggerisca, e che la letteratura ha impiegato vent'anni a smettere di trattarlo come un'anomalia. La domanda produttiva non è "perché non trasferisce?" ma "quali sono le condizioni al contorno in cui il transfer avviene?", che è la stessa riformulazione di D.3 in Lake & Baroni 2023.

---

## 4. Nucleo C — Linguaggio, cultura e ragionamento

> **Domanda:** quanto del ragionamento è ragionamento, e quanto è verbalizzazione? Il formato linguistico esplicito è il pensiero, o una tecnologia per esporlo?

Due letterature che non si parlano fra loro rispondono alla stessa domanda da due lati opposti: organismi senza linguaggio che inferiscono, e umani con linguaggio ma senza scolarizzazione che rifiutano di inferire. Insieme costituiscono il controllo più forte sull'assunzione implicita di tutta la letteratura CoT, cioè che il ragionamento *sia* una catena di enunciati.

### C.1 — Inferenza senza linguaggio

- **von Fersen, Wynne, Delius & Staddon (1991), *Transitive Inference Formation in Pigeons*.** Piccioni che, addestrati su coppie adiacenti di una serie ordinata, rispondono correttamente su coppie non addestrate. Il fenomeno è replicato in molte specie, inclusi corvidi e primati non umani.
- **Taylor, Miller & Gray (2012), *New Caledonian Crows Reason About Hidden Causal Agents*, PNAS.**
- **Penn, Holyoak & Povinelli (2008), *Darwin's Mistake: Explaining the Discontinuity Between Human and Nonhuman Minds*, Behavioral and Brain Sciences.**

**Su Penn, Holyoak & Povinelli, che è il lavoro portante del sotto-nucleo:**

- **Claim:** la discontinuità fra menti umane e non umane non riguarda l'intelligenza in generale ma una capacità specifica — rappresentare e manipolare *relazioni di ordine superiore*, cioè relazioni fra relazioni. Gli animali non umani apprendono relazioni di primo ordine con grande efficacia; la reinterpretazione relazionale è ciò che manca.
- **Tipo di evidenza:** rassegna critica comparativa, con reinterpretazione sistematica di esperimenti esistenti.
- **Autorizza a dire:** che l'inferenza relazionale di primo ordine non richiede linguaggio, e che il candidato per ciò che il linguaggio abilita è specificamente l'ordine superiore.
- **Non autorizza a dire:** che il linguaggio sia la *causa* di quella capacità. Gli autori sono espliciti sul fatto che la correlazione non stabilisce la direzione.
- **Perché è qui:** dà una formulazione precisa e verificabile della domanda "cosa serve per comporre". La composizionalità nel senso di Fodor (D.1) è, letta attraverso PHP, esattamente la capacità di rappresentare relazioni di ordine superiore. E la moltiplicazione posizionale è un caso di ordine superiore: la relazione fra la posizione di un prodotto parziale e la colonna di destinazione è una relazione fra relazioni.

**La conseguenza per la CoT:** se l'inferenza transitiva non richiede sintassi, il ragionamento in spazio latente (I.5) non è una versione degradata della CoT. È la modalità più antica, e la CoT è il caso speciale.

### C.2 — Il ragionamento formale come tecnologia culturale

- **Luria (1976), *Cognitive Development: Its Cultural and Social Foundations*.** Le spedizioni in Uzbekistan e Kirghizistan degli anni Trenta. Soggetti non scolarizzati, posti di fronte a sillogismi con premesse fuori dalla loro esperienza diretta ("nel nord tutti gli orsi sono bianchi; Novaja Zemlja è nel nord; di che colore sono gli orsi lì?"), rifiutano di rispondere — non perché non sappiano inferire, ma perché non accettano la convenzione secondo cui si ragiona su premesse che non si è in grado di verificare. La risposta tipica è: non l'ho visto, chiedi a chi c'è stato.
- **Scribner & Cole (1981), *The Psychology of Literacy*.** Il disegno che separa scolarizzazione e literacy sfruttando i Vai della Liberia, che hanno una scrittura appresa fuori dalla scuola. Gli effetti cognitivi generalizzati risultano attribuibili alla scolarizzazione, non alla scrittura in sé; la literacy produce effetti specifici e circoscritti alle pratiche in cui è impiegata.
- **Olson (1994), *The World on Paper*.** La scrittura come tecnologia che rende gli enunciati oggetti ispezionabili, e quindi rende possibile il ragionamento sulla forma anziché sul contenuto.
- **Henrich, Heine & Norenzayan (2010), *The Weirdest People in the World?*, BBS.** Il campione su cui è costruita la psicologia cognitiva è atipico rispetto alla popolazione umana su quasi ogni dimensione misurata.

**Autorizza a dire:** che il ragionamento formale decontestualizzato — accettare premesse ipotetiche, sospendere la conoscenza del mondo, operare sulla forma — è una pratica trasmessa, non un universale cognitivo che la scolarizzazione si limita a raffinare.

**Non autorizza a dire:** che i soggetti di Luria fossero incapaci di inferenza. È il punto in cui il lavoro è stato più frequentemente frainteso, anche in senso apertamente razzista. La lettura corretta è quella di Scribner & Cole e di Stenning & van Lambalgen (B.4): il rifiuto è una scelta interpretativa, e la fase interpretativa è ciò che la scuola modifica.

**Perché è qui, e perché il ponte non è mai stato fatto:** un modello linguistico apprende il ragionamento formale esplicito da un corpus prodotto in larghissima parte da individui scolarizzati, cioè da una popolazione WEIRD nel senso di Henrich. La CoT non è quindi il formato naturale del ragionamento che il modello scopre, ma un genere testuale che assorbe. Questo predice esattamente ciò che si osserva: la CoT è imitabile in superficie senza corrispondenza col processo (nucleo H), perché è stata appresa come genere. Nessuno, a mia conoscenza, ha formulato l'ipotesi in questi termini.

---

## 5. Nucleo D — Composizionalità e sistematicità

> **Domanda:** un sistema che gestisce X e Y gestisce automaticamente le loro combinazioni? E se no, cosa manca?

Questo nucleo è il ponte fra i tre campi ed è il punto in cui il dibattito filosofico e quello empirico si toccano davvero.

### D.0 — Preliminare: da dove viene il principio

La nozione di composizionalità che circola nel ML è una versione impoverita di quella semantica, e vale la pena avere l'originale.

- **Frege**, il principio nella sua forma canonica: il significato di un'espressione complessa è funzione del significato delle parti e del modo in cui sono combinate. (L'attribuzione testuale è discussa; per la storia, Janssen.)
- **Montague (1970), *Universal Grammar*.** L'omomorfismo fra algebra sintattica e algebra semantica: la composizionalità non è una proprietà vaga ma una condizione algebrica precisa.
- **Partee**, sui limiti e sulla vacuità potenziale del principio — se si è liberi di scegliere sintassi e significati, quasi ogni linguaggio può essere reso composizionale. Il principio ha contenuto solo sotto vincoli indipendenti sulle due algebre.
- **MacCartney & Manning (2009), *An Extended Model of Natural Logic*.** L'inferenza per monotonicità, senza traduzione in forma logica: si opera direttamente sulle stringhe, sfruttando le proprietà di monotonia dei contesti.

**Perché conta:** l'osservazione di Partee è il correttivo più utile del sotto-nucleo. "Il modello è composizionale?" è sottodeterminata finché non si fissano vincoli su cosa conta come parte e come combinazione. Nei test di generalizzazione compositiva quei vincoli sono imposti dallo split del dataset, non dalla teoria — il che significa che lo split *è* la definizione operativa, e va scelto sapendolo.

### D.1 — La sfida originale

**Fodor & Pylyshyn (1988), *Connectionism and Cognitive Architecture: A Critical Analysis*, Cognition.**

- **Claim:** la cognizione è *sistematica* (chi capisce "John loves Mary" capisce necessariamente "Mary loves John") e *produttiva*. La sistematicità richiede rappresentazioni con struttura costituente e processi sensibili a quella struttura. Le reti connessioniste, se non implementano una tale architettura, non spiegano la sistematicità; se la implementano, sono implementazioni di architetture simboliche e non un'alternativa.
- **Tipo di evidenza:** argomentativa, con premessa empirica (che la cognizione *sia* sistematica).
- **Autorizza a dire:** che la sistematicità richiede una spiegazione architetturale, non solo statistica.
- **Non autorizza a dire:** che le reti non possano acquisirla — l'argomento riguarda cosa la *spiega*, e la premessa empirica sulla sistematicità umana è essa stessa contestabile (vedi B.6 e nucleo C: gli umani sono meno sistematici di quanto Fodor assuma).
- **Perché è qui:** è la formulazione originale della domanda che stai facendo. Trentacinque anni dopo, il dilemma "o non lo fa, o lo fa implementando un algoritmo" è ancora la forma della disputa — solo che ora si può guardare dentro e vedere quale corno vale.

Repliche essenziali: **Smolensky (1990)** sulle tensor product representations (struttura costituente distribuita — il primo corno del dilemma preso sul serio); **Fodor & McLaughlin (1990)** che replicano; **Marcus, *The Algebraic Mind* (2001)**.

### D.2 — L'operazionalizzazione empirica

- **Lake & Baroni (2018), SCAN.** Il primo benchmark che rende la sistematicità misurabile; i seq2seq falliscono sugli split compositivi.
- **Hupkes, Dankers, Mul & Bruni (2020), *Compositionality Decomposed: How Do Neural Networks Generalise?*, JAIR.** Scompone la composizionalità in cinque test distinti (systematicity, productivity, substitutivity, localism, overgeneralisation).
- **Kim & Linzen (2020), COGS.**
- **Keysers et al. (2020), CFQ / compositional generalization measurement.**

**Su Hupkes et al., con enfasi:** è il lavoro che rende inutilizzabile la domanda "il modello è composizionale?" e la sostituisce con cinque domande separabili. Da leggere prima di scrivere qualsiasi cosa che usi la parola. Nel tuo caso serve a nominare con precisione quale delle cinque il tuo design testa (productivity e systematicity; non le altre tre).

### D.3 — Il rovescio

**Lake & Baroni (2023), *Human-like Systematic Generalization Through a Meta-Learning Neural Network*, Nature.**

- **Claim:** con meta-learning su un curriculum di compiti compositivi, una rete standard raggiunge — e in alcuni casi supera — la generalizzazione sistematica umana.
- **Autorizza a dire:** che l'architettura non è di per sé il vincolo; il regime di training lo è.
- **Non autorizza a dire:** che il problema sia risolto in generale — il dominio è ristretto e il curriculum è progettato.
- **Perché è qui:** è la risposta più forte a Fodor & Pylyshyn e il precedente concettuale per qualunque condizione di tipo "scaffold". Se uno scaffold minimo trasforma il fallimento in successo, la domanda si sposta da "può?" a "quale bias serve?", che è una domanda quantitativa e molto più produttiva.

### D.4 — Il caso aritmetico

**Dziri et al. (2023), *Faith and Fate: Limits of Transformers on Compositionality*, NeurIPS.**

- **Claim:** riducendo compiti compositivi (moltiplicazione multi-cifra, puzzle di Einstein, programmazione dinamica) a grafi di computazione, si mostra che i transformer risolvono il task per *matching di sottografi memorizzati* e degradano bruscamente al crescere della profondità del grafo. La performance predetta dalla frequenza dei sottografi nel training, non dalla struttura.
- **Tipo di evidenza:** comportamentale, con analisi strutturale del task (non causale sulle attivazioni).
- **Autorizza a dire:** che il successo su compiti compositivi può essere spiegato senza postulare un algoritmo composizionale.
- **Non autorizza a dire:** *dove* dentro il modello la composizione fallisce. È un risultato comportamentale con una teoria del task, non una localizzazione meccanicistica.
- **Perché è qui:** è il precedente comportamentale più vicino alla domanda "moltiplicazione multi-cifra da primitive". La sua lacuna — nessuna analisi causale interna — è esattamente lo spazio che un lavoro meccanicistico occupa.

### D.5 — Il contrasto: induzione di programmi

Se il transformer non costruisce una procedura composizionale, vale la pena avere davanti un modello formale di un sistema che lo fa, per sapere esattamente cosa manca.

- **Spelke & Kinzler (2007), *Core Knowledge*.** I sistemi di conoscenza precoce (oggetti, agenti, numero, geometria) come primitive non apprese.
- **Carey, *The Origin of Concepts* (2009).** Il cambiamento concettuale: come si acquisiscono concetti non esprimibili nel vocabolario precedente. Il caso del numero naturale è trattato in dettaglio ed è direttamente pertinente.
- **Gopnik & Meltzoff**, la *theory theory*: il bambino come costruttore di teorie causali sottoposte a revisione.
- **Tenenbaum, Kemp, Griffiths & Goodman (2011), *How to Grow a Mind*, Science.** Il programma bayesiano-strutturato: priors gerarchici su spazi di ipotesi strutturate.
- **Lake, Salakhutdinov & Tenenbaum (2015), *Human-Level Concept Learning Through Probabilistic Program Induction*, Science.** Il modello canonico: un concetto è un programma probabilistico composto da primitive esplicite secondo una grammatica di composizione, appreso da un singolo esempio.

**Perché è qui:** BPL è il modello formale di ciò che il tuo esperimento chiede se il transformer faccia. Le primitive sono esplicite, la grammatica di composizione è esplicita, e il transfer a combinazioni nuove è una conseguenza dell'architettura anziché una scoperta empirica. Averlo come contrasto rende preciso il claim negativo: non "il modello non compone" ma "il modello non ha la separazione fra inventario di primitive e regola di composizione che rende il transfer automatico".

**Non autorizza a dire:** che BPL sia la spiegazione della cognizione umana. Il dominio è ristretto (caratteri manoscritti) e le primitive sono progettate, non apprese — che è precisamente l'obiezione simmetrica a quella mossa ai transformer.

---

## 6. Nucleo E — La classe computazionale

> **Domanda:** quali funzioni un transformer a profondità costante *può* esprimere, indipendentemente dal training?

Questo nucleo è quello che risparmia mesi. Serve a sapere quando una frontiera empirica sta ricalcando un teorema.

- **Hahn (2020), *Theoretical Limitations of Self-Attention in Neural Sequence Models*, TACL.** Hard attention non può riconoscere PARITY o linguaggi Dyck; soft attention degrada con la lunghezza.
- **Merrill & Sabharwal (2023), *The Parallelism Tradeoff: Limitations of Log-Precision Transformers*, TACL.** I transformer a precisione logaritmica e profondità costante sono in uniform TC⁰. Non possono risolvere problemi P-completi (sotto le assunzioni standard di separazione).
- **Merrill & Sabharwal (2024), *The Expressive Power of Transformers with Chain of Thought*, ICLR.** La CoT come computazione seriale che estende la classe: con un numero sufficiente di passi intermedi si esce da TC⁰.
- **Feng et al. (2023), *Towards Revealing the Mystery behind Chain of Thought: A Theoretical Perspective*, NeurIPS.** Costruzione esplicita: per l'aritmetica e la programmazione dinamica, la CoT permette a un transformer di profondità costante ciò che senza richiederebbe profondità crescente.
- **Zhou et al. (2023/2024), *What Algorithms Can Transformers Learn? A Study in Length Generalization*.** L'ipotesi RASP-L: un transformer generalizza in lunghezza sui task il cui algoritmo è esprimibile come programma RASP corto e "semplice".
- **Delétang et al. (2023), *Neural Networks and the Chomsky Hierarchy*, ICLR.** Mappatura empirica sistematica delle architetture sulla gerarchia.
- **Pérez, Barceló & Marinkovic (2021)**, sulla Turing-completezza dei transformer con precisione arbitraria — il risultato di segno opposto, utile per capire quanto le assunzioni sulla precisione determinano la conclusione.
- **Sanford, Hsu & Telgarsky (2023)**, sui limiti rappresentazionali dell'attenzione per compiti che richiedono aggregazione su triple.

**Come leggere questo nucleo, in modo non ingenuo:** i risultati di impossibilità dipendono in modo critico dalle assunzioni (precisione numerica, uniformità, profondità in funzione della lunghezza dell'input). Un teorema che dice "profondità costante non può fare X" non dice niente su cosa fa un modello di profondità 32 su input di lunghezza 20. La tentazione è usarli come clave; l'uso corretto è come vincolo di forma sulle ipotesi. La domanda giusta è: *la mia frontiera empirica ha la forma che questi teoremi predicono, oppure no?* Entrambe le risposte sono informative.

---

## 7. Nucleo F — La difficoltà indipendente dall'agente

> **Domanda:** quanto è difficile un'inferenza, a prescindere da chi la esegue?

Il nucleo E limita l'agente. Questo limita il *problema*. È l'unica nozione di difficoltà del ragionamento che non dipende dal ragionatore, ed è quasi del tutto assente dalla letteratura ML sul reasoning nonostante il parallelo con la CoT sia immediato.

### F.1 — Sistemi di prova e lower bound

- **Cook & Reckhow (1979), *The Relative Efficiency of Propositional Proof Systems*, JSL.** Definiscono cosa sia un sistema di prova e stabiliscono il legame di fondo: esiste un sistema di prova con dimostrazioni di lunghezza polinomiale per tutte le tautologie se e solo se NP = coNP. Il programma di ricerca che ne segue — dimostrare lower bound superpolinomiali per sistemi via via più forti — è un attacco graduale a quella separazione.
- **Haken (1985), *The Intractability of Resolution*, TCS.** Il primo lower bound esponenziale: ogni refutazione per risoluzione del principio della piccionaia richiede lunghezza esponenziale.
- **Ben-Sasson & Wigderson (2001), *Short Proofs Are Narrow — Resolution Made Simple*, JACM.** Il trade-off dimensione/ampiezza, che rende quasi meccanica la derivazione di lower bound per risoluzione.

**Claim complessivo:** esistono enunciati veri, brevi e concettualmente semplici la cui dimostrazione più corta, in un dato sistema, è necessariamente di lunghezza esponenziale. Nessun agente, per quanto capace, può accorciarla restando in quel sistema.

- **Autorizza a dire:** che la lunghezza minima di una traccia di ragionamento è un oggetto matematico con teoremi già dimostrati, non una proprietà del modello.
- **Non autorizza a dire:** che un enunciato sia "difficile" in assoluto. **Ogni lower bound è relativo al sistema di prova.** La piccionaia è esponenziale per risoluzione e polinomiale per sistemi più forti (Frege esteso, o risoluzione con estensione). Questa relatività è il punto interessante, non un dettaglio tecnico.
- **Perché è qui:** il sistema di prova è l'analogo formale del *formato* di ragionamento. Cambiare formato — scratchpad, decomposizione, notazione intermedia, chiamata a un tool — è cambiare sistema di prova, e la teoria dice che questo può cambiare la lunghezza minima di un fattore esponenziale. È la giustificazione teorica più solida dell'esistenza di scaffold efficaci, e spiega perché la ricerca del "prompt giusto" non è cargo cult: alcuni formati sono genuinamente più espressivi per certe famiglie di problemi.

### F.2 — Ricerca di dimostrazioni in pratica

- **Davis, Putnam, Logemann & Loveland**, la procedura DPLL.
- **Marques-Silva & Sakallah (1996/1999), GRASP**, e la linea CDCL — conflict-driven clause learning. Il fatto che i SAT solver moderni risolvano istanze industriali con milioni di variabili, a fronte di lower bound esponenziali nel caso peggiore, è esso stesso un risultato sul rapporto fra difficoltà nel caso peggiore e difficoltà nei casi che interessano.
- **Trinh et al. (2024), AlphaGeometry**, Nature; e la linea successiva su Lean e mathlib, con benchmark come miniF2F.

**La distinzione da non perdere:** *trovare* una dimostrazione e *verificarla* sono problemi di difficoltà radicalmente diversa. Questa asimmetria è la ragione per cui l'architettura generatore-neurale più verificatore-simbolico funziona, ed è esattamente la struttura del nucleo K. La versione informale che circola nel ML — "il modello genera, il solver controlla" — è un'istanza di un fatto complessologico.

**Il collegamento non fatto, che vale la pena tenere in mente:** una traccia di CoT è una dimostrazione in un sistema di prova non specificato e non sano. Le domande naturali — qual è il sistema? quali regole di inferenza sono ammesse? esiste un lower bound sulla lunghezza della traccia per una famiglia di problemi? — non hanno, a mia conoscenza, ricevuto una formulazione seria. È uno spazio aperto e non affollato.

---

## 8. Nucleo G — Il comportamento nei sistemi attuali

> **Domanda:** cosa migliora la performance su compiti che chiamiamo di ragionamento, e cosa significa quel miglioramento?

**Strato instabile.** Da rivedere ogni 12–18 mesi.

### G.1 — Le tecniche

- **Nye et al. (2021), *Show Your Work: Scratchpads for Intermediate Computation*.** Il precursore.
- **Wei et al. (2022), *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*, NeurIPS.**
- **Kojima et al. (2022), *Large Language Models are Zero-Shot Reasoners*.**
- **Wang et al. (2023), *Self-Consistency Improves Chain of Thought Reasoning*, ICLR.**
- **Zhou et al. (2023), *Least-to-Most Prompting*.**
- **Gao et al. (2023), PAL: *Program-aided Language Models*.**
- **Yao et al. (2023), *ReAct*** e ***Tree of Thoughts***.

### G.2 — La critica

- **Mirzadeh et al. (2024), *GSM-Symbolic*.** Variazioni templatiche di GSM8K fanno crollare la performance; clausole irrilevanti aggiunte al testo degradano drasticamente.
- **McCoy et al. (2023/2024), *Embers of Autoregression*.** La performance è predetta dalla probabilità del task, dell'input e dell'output sotto la distribuzione di training. Riformulazione teleologica: il modello fa ciò per cui è stato ottimizzato.
- **Razeghi et al. (2022), *Impact of Pretraining Term Frequencies on Few-Shot Numerical Reasoning*.** Correlazione diretta fra frequenza dei numeri nel corpus e accuratezza aritmetica.
- **Ullman (2023)**, sul crollo della theory of mind sotto variazioni triviali.
- **Valmeekam / Kambhampati et al., PlanBench** e i lavori successivi sul planning. Da leggere con un filtro sulla retorica, ma i risultati sui domini mascherati sono solidi.

**La tesi trasversale di questo nucleo:** ogni miglioramento riportato su un benchmark è ambiguo fra acquisizione di capacità e riduzione della distanza distribuzionale fra test e training. Separare le due richiede o controlli distribuzionali (McCoy, Razeghi) o accesso al meccanismo (nucleo I).

### G.3 — Il regime attuale

- **DeepSeek-AI (2025), *DeepSeek-R1*.** RL su reward verificabile che induce tracce di ragionamento lunghe, con comportamenti emergenti di auto-verifica.
- La letteratura sul test-time compute scaling (2024–2026). Questo sotto-strato è il più volatile del documento; verificare prima di citare.

### G.4 — Il retaggio psicometrico

I benchmark hanno ereditato assunzioni da una disciplina che le ha esaminate per un secolo, senza importarne l'apparato critico.

- **Spearman (1904)**, il fattore *g* e l'analisi fattoriale; **Cattell**, la distinzione fluida/cristallizzata; **le matrici di Raven** come test paradigmatico di ragionamento non verbale.
- **Chollet (2019), *On the Measure of Intelligence*.** La definizione di intelligenza come efficienza di acquisizione di skill a parità di priors ed esperienza, e ARC come tentativo di operazionalizzarla. Discende direttamente dalla tradizione delle matrici.

**Perché è qui, e non per il contenuto:** la psicometria ha cent'anni di riflessione su *validità di costrutto* — sotto quali condizioni un test misura la capacità che dichiara di misurare, anziché una strategia specifica al formato. Ha nomi per i modi di fallire (validità convergente e discriminante, invarianza di misura fra gruppi, contaminazione del criterio) che descrivono con precisione i problemi attuali dei benchmark, riscoperti sotto altri nomi. Un modello e un umano che ottengono lo stesso punteggio su Raven non hanno, in senso psicometrico, punteggi confrontabili, perché l'invarianza di misura fra le due popolazioni non è stata stabilita e quasi certamente non vale. Questo è un vocabolario disponibile e inutilizzato.

---

## 9. Nucleo H — La traccia è il processo?

> **Domanda:** la spiegazione verbalizzata corrisponde alla computazione che ha prodotto la risposta?

Questo nucleo va letto **subito dopo B.5**, non separatamente. È la stessa domanda su un sostrato diverso.

- **Turpin et al. (2023), *Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting*, NeurIPS.** Bias iniettati nel prompt (es. riordinamento sistematico delle opzioni) cambiano la risposta senza comparire mai nella traccia. Il design è Nisbett & Wilson con un soggetto diverso.
- **Lanham et al. (2023), *Measuring Faithfulness in Chain-of-Thought Reasoning*.** Le metriche di perturbazione: early answering, adding mistakes, filler tokens, paraphrasing.
- **Arcuschin et al. (2025)**, sull'unfaithfulness in condizioni naturali, senza bias iniettati.
- **Korbak et al. (2025), *Chain of Thought Monitorability: A New and Fragile Opportunity for AI Safety*.** Position paper multi-lab: la leggibilità della CoT è una proprietà contingente del regime di training attuale e può degradare.
- **Baker et al. (2025)**, su monitoring della CoT e reward hacking, e sull'effetto perverso dell'ottimizzare direttamente la CoT monitorata.
- **BONAFIDE (Gur-Arieh et al., 2026).** Ground truth reale sulla faithfulness invece di proxy; le metriche standard di perturbazione risultano vicine al caso.

**La distinzione da tenere separata, sempre:**

- **Plausibilità** — la spiegazione convince un umano.
- **Importanza** — il testo della traccia influenza causalmente l'output (rimuoverlo cambia la risposta).
- **Faithfulness** — la traccia descrive il processo che ha effettivamente prodotto la risposta.

Le tre sono logicamente indipendenti. Una traccia può essere causalmente necessaria (il modello *usa* quei token come memoria di lavoro) e comunque non essere una descrizione del processo: sta computando *attraverso* il testo, non *riportando* una computazione. Gran parte della confusione nel campo nasce dal collassare importanza e faithfulness.

---

## 10. Nucleo I — Il meccanismo

> **Domanda:** quale algoritmo è implementato, e come si dimostra?

### I.1 — Il framework

- **Elhage et al. (2021), *A Mathematical Framework for Transformer Circuits*.** Residual stream, circuiti QK/OV, composizione fra teste.
- **Olsson et al. (2022), *In-context Learning and Induction Heads*.**
- **Wang et al. (2023), *Interpretability in the Wild* (IOI).** Il template metodologico per l'identificazione di un circuito.
- **Conmy et al. (2023), ACDC.** Automazione della scoperta di circuiti.

### I.2 — Il fondamento causale

- **Vig et al. (2020)**, causal mediation analysis applicata ai modelli linguistici.
- **Geiger et al. (2021, 2023–2024)**, causal abstraction, interchange interventions, DAS (distributed alignment search).

**Perché I.2 è il collo di bottiglia concettuale del campo:** dà le condizioni sotto cui si può legittimamente dire che una rete *implementa* un algoritmo simbolico — una relazione di astrazione causale fra il grafo di basso livello e quello di alto livello, verificata da interventi allineati. Senza questo apparato, "il modello implementa l'algoritmo X" è una metafora. Con esso, è un claim verificabile. È anche il punto in cui il nucleo A.4 (Pearl) e il nucleo I si saldano.

### I.3 — Aritmetica

- **Nanda et al. (2023), *Progress Measures for Grokking via Mechanistic Interpretability*, ICLR.** L'algoritmo trigonometrico per l'addizione modulare, reverse-engineered completamente.
- **Zhong et al. (2023), *The Clock and the Pizza*.** Lo stesso task, due algoritmi diversi a seconda del seed e degli iperparametri. Risultato importante e sottovalutato: l'universalità dei circuiti non è garantita.
- **Quirke & Barez (2024), *Understanding Addition in Transformers*** (e i lavori successivi con Neo). Circuiti ST/SV/TriAdd nell'addizione multi-cifra.
- **Bai et al. (2025), *Why Can't Transformers Learn Multiplication?*** L'attenzione costruisce un DAG per cachare e recuperare prodotti parziali; il segnale ausiliario sui running sums rende apprendibile ciò che il training standard non trova.
- **Lindsey et al. (2025), *On the Biology of a Large Language Model*.** Circuiti aritmetici ibridi in un modello di frontiera: strategie multiple in parallelo, diverse da quelle dei modelli piccoli.

**Il vincolo che questi cinque lavori insieme impongono:** Zhong e Lindsey rendono illegittimo il passaggio *circuito trovato in un modello piccolo → meccanismo generale*. La piccola scala compra identificabilità causale, non universalità. Va detto esplicitamente in qualunque cosa si scriva, non come cautela retorica ma perché è il punto in cui un revisore attacca.

### I.4 — Riuso e trasferimento

- **Todd et al. (2024), *Function Vectors in Large Language Models*, ICLR.**
- **Hendel, Geva & Globerson (2023), *In-Context Learning Creates Task Vectors*.**
- **Merullo, Eickhoff & Pavlick (2024), *Circuit Component Reuse Across Tasks in Transformer Language Models*, ICLR.**

**Su Merullo et al.:** è la formulazione più vicina alla domanda "una primitiva appresa viene riusata in un contesto strutturalmente nuovo?", con evidenza positiva (il circuito IOI riusato su un task diverso). È il precedente da confrontare direttamente: se il riuso avviene fra task linguistici ma non fra operazioni aritmetiche, la differenza fra i due casi è essa stessa il risultato.

### I.5 — Ragionamento latente

- **Hao et al. (2024), *Training Large Language Models to Reason in a Continuous Latent Space* (Coconut).**
- **Deng et al. (2023/2024)**, sull'internalizzazione della CoT (implicit chain of thought).
- **Giannou et al. (2023)**, looped transformers come computatori programmabili.

**Perché sta qui e non nel nucleo G:** è la controparte empirica dei risultati di espressività (nucleo E). Se la CoT funziona perché fornisce computazione seriale, allora il ragionamento in spazio latente dovrebbe fornire lo stesso beneficio senza il testo — e la sua efficacia o inefficacia discrimina fra "la CoT aiuta perché è computazione" e "la CoT aiuta perché è testo".

---

## 11. Nucleo J — Il sostrato biologico

> **Domanda:** come si stabilisce che un sistema fisico implementa un'inferenza? E che forma hanno le rappresentazioni che generalizzano?

Il valore di questo nucleo non sta principalmente nei risultati. Sta nel fatto che la neuroscienza computazionale ha sviluppato, trent'anni prima e su un sostrato molto più ostile, la metodologia che la mech interp sta reinventando. Ha convissuto a lungo con l'ambiguità correlazione/causa e ha costruito un apparato per gestirla; è per questo che il vocabolario di lesione, inattivazione reversibile e decoding mappa così bene su ablation e patching.

### J.1 — I livelli di analisi

**Marr (1982), *Vision*, capitolo 1.**

- **Claim:** ogni sistema che elabora informazione ammette tre descrizioni indipendenti e non riducibili l'una all'altra — computazionale (quale problema è risolto, e perché quello), algoritmica (quale procedura e quale rappresentazione), implementativa (in quale sostrato).
- **Autorizza a dire:** che un disaccordo può essere apparente perché i due interlocutori descrivono livelli diversi, e che una spiegazione a un livello non sostituisce quella a un altro.
- **Non autorizza a dire:** che i livelli siano davvero indipendenti. La critica standard, poi accolta anche da chi lavorava nella tradizione, è che i vincoli implementativi determinano fortemente quali algoritmi sono plausibili — il che è precisamente ciò che la mech interp mostra sui transformer.
- **Perché è qui, ma appartiene all'inizio:** questa è la distinzione più utile dell'intero documento e andrebbe letta insieme alla sezione 1. Sette degli otto sensi di "reasoning" elencati lì si dispongono su tre livelli marriani, e il fatto che i dibattiti pubblici non progrediscano dipende in larga parte da questo.

### J.2 — Decisione come accumulo di evidenza

- **Ratcliff (1978)**, il drift-diffusion model; e la letteratura successiva sui modelli di accumulo.
- **Gold & Shadlen (2007), *The Neural Basis of Decision Making*, Annual Review of Neuroscience.** La rassegna canonica sull'integrazione temporale di evidenza rumorosa fino a una soglia, con correlati identificati a livello di singola cellula nell'area LIP.

**Perché è il caso migliore che il campo abbia:** un modello matematico che predice congiuntamente accuratezza e distribuzione dei tempi di reazione, con parametri interpretabili, e un correlato neurale i cui pattern di scarica seguono la variabile decisionale postulata dal modello. Il legame fra livello algoritmico e livello implementativo è più stretto qui che in qualunque risultato di mech interp esistente. Vale come termine di paragone su cosa significhi "spiegare un comportamento inferenziale".

### J.3 — Controllo, regole, astrazione gerarchica

- **Miller & Cohen (2001), *An Integrative Theory of Prefrontal Cortex Function*, Annual Review of Neuroscience.** La PFC come mantenimento attivo di rappresentazioni di goal che modulano l'elaborazione altrove — bias top-down anziché computazione.
- **O'Reilly & Frank (2006)**, PBWM: il gating della working memory appreso per reinforcement, con i gangli della base come meccanismo di gate.
- **Badre & D'Esposito (2009)**, sul gradiente rostro-caudale nel lobo frontale: regole più astratte rappresentate più anteriormente.
- **Duncan**, sul *multiple demand system* e la sua relazione con l'intelligenza fluida.

**Il ponte concettuale:** "mantenere una rappresentazione che modula l'elaborazione altrove senza fare la computazione" è la descrizione funzionale di ciò che i function vector (I.4) fanno in un transformer. La letteratura sulla PFC ha una teoria di quando quel meccanismo funziona e quando fallisce — sovraccarico, interferenza, costo dello switch — che nel caso dei transformer non esiste ancora.

### J.4 — Geometria dell'astrazione

Il sotto-nucleo più direttamente utile.

- **Rigotti et al. (2013), *The Importance of Mixed Selectivity in Complex Cognitive Tasks*, Nature.** I neuroni con selettività mista non lineare espandono la dimensionalità della rappresentazione, rendendo linearmente separabile un numero molto maggiore di partizioni del task. La dimensionalità misurata predice la performance comportamentale.
- **Bernardi et al. (2020), *The Geometry of Abstraction in the Hippocampus and Prefrontal Cortex*, Cell.**
- **Kriegeskorte, Mur & Bandettini (2008)**, representational similarity analysis.
- **Chung, Lee & Sompolinsky (2018)**, la teoria della capacità dei manifold rappresentazionali.

**Su Bernardi et al., che è il lavoro portante:**

- **Claim:** introducono la **CCGP** (cross-condition generalization performance) — si addestra un decoder lineare su un sottoinsieme di condizioni e lo si testa su condizioni *diverse* e non viste. Una variabile è rappresentata in forma astratta solo se il decoder generalizza. Mostrano che nella PFC e nell'ippocampo alcune variabili hanno geometria astratta e altre no, pur essendo tutte decodificabili nel senso ordinario.
- **Tipo di evidenza:** correlazionale (decoding da registrazioni), ma con un controllo geometrico che esclude le spiegazioni banali.
- **Autorizza a dire:** che la decodificabilità semplice e la rappresentazione astratta sono proprietà distinte e separabili sperimentalmente.
- **Non autorizza a dire:** che la geometria astratta sia causalmente usata dal sistema a valle. È il limite dichiarato del metodo, e la ragione per cui serve comunque l'intervento.
- **Perché è qui:** **è la tua domanda, con una metrica già costruita.** "L'informazione è presente" contro "è presente in una forma che generalizza a combinazioni non viste" è la distinzione fra probe ordinario e CCGP. La neuroscienza ha dovuto inventarla perché la decodificabilità semplice si era rivelata quasi priva di contenuto — un probe che funziona non dice quasi nulla, dato che con dimensionalità sufficiente qualunque partizione è separabile (è il risultato di Rigotti). L'interpretabilità dei transformer non ha ancora assorbito del tutto questa lezione, e importare la CCGP in un contesto aritmetico — un probe sui prodotti parziali addestrato su alcune coppie di cifre e testato su altre — è una mossa disponibile e non ovvia.

### J.5 — Mappe cognitive e riuso di struttura

- **Behrens et al. (2018), *What Is a Cognitive Map? Organizing Knowledge for Flexible Behavior*, Neuron.** Le rappresentazioni di tipo grid generalizzano a spazi relazionali non spaziali: la stessa struttura appresa in un dominio, riusata in un altro.
- **Whittington et al. (2020), la Tolman-Eichenbaum Machine**, Cell. Un modello che separa esplicitamente la struttura astratta dal contenuto sensoriale e ricombina le due, riproducendo le proprietà delle cellule ippocampali.
- **Whittington, Warren & Behrens (2022), *Relating Transformers to Models and Neural Representations of the Hippocampal Formation*, ICLR.** La corrispondenza formale fra TEM e l'architettura transformer.

**Perché chiude il nucleo:** è letteratura sul riuso di struttura appresa in domini nuovi, cioè sulla tua domanda, scritta da persone che non pubblicano a NeurIPS e che non vengono citate nella letteratura sulla composizionalità. La separazione struttura/contenuto della TEM è anche l'architettura che Fodor avrebbe chiesto (D.1), ottenuta per apprendimento.

### Il caveat, che è serio

La neuroscienza ha un vantaggio metodologico e uno svantaggio epistemico. Il vantaggio è l'apparato causale. Lo svantaggio è che i suoi compiti sono poverissimi rispetto all'aritmetica multi-cifra: un'inferenza transitiva a cinque item non ha una catena di riporto, e la maggior parte dei paradigmi è progettata per essere eseguibile da un primate in una sessione di registrazione. **Da questo nucleo vanno presi i metodi e le distinzioni, non i risultati.** Il transfer dei risultati in senso stretto è quasi sempre un errore, e la letteratura NeuroAI che lo pratica è la parte meno solida del campo.

---

## 12. Nucleo K — Neuro-simbolico

> **Domanda:** si può ottenere la garanzia simbolica senza rinunciare all'apprendimento?

Nucleo compatto, per completezza dell'asse.

- **Manhaeve et al. (2018), DeepProbLog.**
- **Badreddine et al. (2022), Logic Tensor Networks.**
- **Xu et al. (2018), *A Semantic Loss Function for Deep Learning with Symbolic Knowledge*.**
- **Garcez & Lamb (2020/2023), *Neurosymbolic AI: The 3rd Wave*.** Rassegna programmatica.
- **Pan et al. (2023), Logic-LM**; **Olausson et al. (2023), LINC**; **Ye et al. (2023), SatLM.** Il filone LLM-come-estrattore + solver esterno.

**La distinzione strutturale da tenere ferma:** integrazione *a livello di loss* (DeepProbLog, semantic loss — il vincolo simbolico modella i pesi) contro integrazione *a livello di pipeline* (Logic-LM, LINC — il simbolico valida un output neurale a runtime). Sono risposte a domande diverse: la prima chiede se la conoscenza simbolica possa essere appresa, la seconda si accontenta di garantire la correttezza dell'output. La seconda è quella che funziona oggi; la prima è quella teoricamente interessante.

---

## 13. Itinerario di lettura

Trentasette voci in cinque fasi, in ordine di lettura. L'ordine è vincolante all'interno di ogni fase: ogni voce è collocata dove è perché prepara la successiva, e leggerle in ordine sparso costa più di quanto sembri.

Ogni fase ha un esito verificabile. Se al termine non riesci a formulare l'esito a voce, la fase non è servita e va rifatta la lettura, non aggiunta una voce.

Le liste di autori lunghe sono troncate con *et al.* dove non sono sicuro dell'ordine completo; il primo autore e l'anno sono sufficienti per il recupero.

---

### Fase 1 — I metri (4–6 settimane, 8 voci)

*Serve a costruire il vocabolario con cui giudicare tutto il resto. È la fase che più frequentemente viene saltata e che più frequentemente andrebbe fatta due volte.*

1. **Marr, D. (1982).** *Vision: A Computational Investigation into the Human Representation and Processing of Visual Information.* W. H. Freeman.
   → Solo il capitolo 1. Fuori sequenza rispetto al documento (sta in J.1) ma va per primo: dà i tre livelli di analisi.

2. **Harman, G. (1986).** *Change in View: Principles of Reasoning.* MIT Press.
   → Il libro intero è breve. Smonta l'identificazione fra logica e teoria del ragionamento.

3. **Goodman, N. (1955).** *Fact, Fiction, and Forecast.* Harvard University Press.
   → Capitolo 3, *The New Riddle of Induction*. Il problema *grue* è la generalizzazione OOD trent'anni prima.

4. **Wason, P. C. (1968).** «Reasoning about a Rule». *Quarterly Journal of Experimental Psychology*, 20(3).
   → Il selection task nella sua formulazione canonica. Breve.

5. **Cheng, P. W., & Holyoak, K. J. (1985).** «Pragmatic Reasoning Schemas». *Cognitive Psychology*, 17(4).
   → Da leggere subito dopo Wason: la performance dipende dal contenuto, non dalla forma.

6. **Stenning, K., & van Lambalgen, M. (2008).** *Human Reasoning and Cognitive Science.* MIT Press.
   → La voce più impegnativa della fase. *Reasoning to* contro *reasoning from an interpretation*.

7. **Nisbett, R. E., & Wilson, T. D. (1977).** «Telling More Than We Can Know: Verbal Reports on Mental Processes». *Psychological Review*, 84(3).
   → La tesi di Turpin et al. trentasei anni prima, con un design migliore.

8. **Mercier, H., & Sperber, D. (2011).** «Why Do Humans Reason? Arguments for an Argumentative Theory». *Behavioral and Brain Sciences*, 34(2).
   → Il target article; le repliche pubblicate nello stesso numero valgono la lettura. Versione estesa: *The Enigma of Reason*, Harvard University Press, 2017.

**Esito:** saper distinguere, davanti a qualunque claim su reasoning, fra divergenza normativa, divergenza interpretativa e fallimento esecutivo; e saper collocare un disaccordo su uno dei tre livelli di Marr.

---

### Fase 2 — Cosa è ragionamento e cosa è verbalizzazione (2–3 settimane, 4 voci)

*Fase breve e ad alto rendimento. Serve a non dare per scontato che il ragionamento sia una catena di enunciati.*

9. **Penn, D. C., Holyoak, K. J., & Povinelli, D. J. (2008).** «Darwin's Mistake: Explaining the Discontinuity Between Human and Nonhuman Minds». *Behavioral and Brain Sciences*, 31(2).
   → Target article. La discontinuità è nelle relazioni di ordine superiore, non nell'inferenza in sé.

10. **Luria, A. R. (1976).** *Cognitive Development: Its Cultural and Social Foundations.* Harvard University Press. (Ed. M. Cole.)
    → I capitoli sui sillogismi. Da leggere con l'avvertenza di C.2 sui fraintendimenti storici.

11. **Scribner, S., & Cole, M. (1981).** *The Psychology of Literacy.* Harvard University Press.
    → Il correttivo empirico a Luria: separa scolarizzazione da literacy.

12. **Henrich, J., Heine, S. J., & Norenzayan (2010).** «The Weirdest People in the World?». *Behavioral and Brain Sciences*, 33(2–3).
    → Il campione su cui è costruita la psicologia cognitiva, e quindi anche il corpus.

**Esito:** saper argomentare, in entrambe le direzioni, la tesi che la CoT sia un genere testuale appreso anziché il formato nativo dell'inferenza.

---

### Fase 3 — La sfida strutturale (3–4 settimane, 9 voci)

*Il ponte fra filosofia della mente ed evidenza empirica. È la fase più vicina alla tua domanda di ricerca.*

13. **Montague, R. (1970).** «Universal Grammar». *Theoria*, 36(3).
    → Difficile e non indispensabile per intero: serve l'omomorfismo fra algebra sintattica e semantica.

14. **Partee, B. H. (1984).** «Compositionality». In F. Landman & F. Veltman (a cura di), *Varieties of Formal Semantics.*
    → Il correttivo: il principio è vacuo senza vincoli indipendenti sulle due algebre.

15. **Fodor, J. A., & Pylyshyn, Z. W. (1988).** «Connectionism and Cognitive Architecture: A Critical Analysis». *Cognition*, 28(1–2).
    → La sfida originale. Lunga; la sezione sulla sistematicità è quella che conta.

16. **Smolensky, P. (1990).** «Tensor Product Variable Binding and the Representation of Symbolic Structures in Connectionist Systems». *Artificial Intelligence*, 46(1–2).
    → La replica tecnica: struttura costituente in forma distribuita.

17. **Marcus, G. F. (2001).** *The Algebraic Mind: Integrating Connectionism and Cognitive Science.* MIT Press.
    → La versione argomentata e leggibile della posizione simbolista.

18. **Hupkes, D., Dankers, V., Mul, M., & Bruni, E. (2020).** «Compositionality Decomposed: How Do Neural Networks Generalise?». *Journal of Artificial Intelligence Research*, 67.
    → Le cinque nozioni separabili. Da tenere aperto quando si progetta uno split.

19. **Lake, B. M., & Baroni, M. (2018).** «Generalization Without Systematicity: On the Compositional Skills of Sequence-to-Sequence Recurrent Networks». *ICML*.
    → SCAN. Il benchmark che ha reso misurabile la sfida di Fodor.

20. **Lake, B. M., & Baroni, M. (2023).** «Human-like Systematic Generalization Through a Meta-Learning Neural Network». *Nature*, 623.
    → Il rovescio, dagli stessi autori. Il regime di training, non l'architettura.

21. **Lake, B. M., Salakhutdinov, R., & Tenenbaum, J. B. (2015).** «Human-Level Concept Learning Through Probabilistic Program Induction». *Science*, 350(6266).
    → Il contrasto formale: come si comporta un sistema che ha davvero primitive e grammatica di composizione.

22. **Dziri, N., et al. (2023).** «Faith and Fate: Limits of Transformers on Compositionality». *NeurIPS*.
    → Chiude la fase riportando tutto sul caso aritmetico.

**Esito:** saper nominare quale delle cinque nozioni di composizionalità è in gioco in un dato esperimento, e saper dire cosa mancava a Fodor per rendere la sua tesi verificabile.

---

### Fase 4 — Il vincolo e il meccanismo (6–10 settimane, 15 voci)

*La fase più lunga e la più tecnica. Sotto-sequenza obbligata: difficoltà del problema → limite dell'architettura → apparato causale → geometria → casi aritmetici.*

**Difficoltà intrinseca**

23. **Cook, S. A., & Reckhow, R. A. (1979).** «The Relative Efficiency of Propositional Proof Systems». *Journal of Symbolic Logic*, 44(1).
    → Cosa sia un sistema di prova, e il legame con NP vs coNP.

24. **Haken, A. (1985).** «The Intractability of Resolution». *Theoretical Computer Science*, 39.
    → Il primo lower bound esponenziale. Basta capirne la struttura, non ogni passaggio.

**Limite dell'architettura**

25. **Merrill, W., & Sabharwal, A. (2023).** «The Parallelism Tradeoff: Limitations of Log-Precision Transformers». *TACL*, 11.
    → Profondità costante e precisione logaritmica ⊆ uniform TC⁰.

26. **Merrill, W., & Sabharwal, A. (2024).** «The Expressive Power of Transformers with Chain of Thought». *ICLR*.
    → Come la CoT estende la classe. Da leggere di seguito al precedente.

27. **Feng, G., Zhang, B., Gu, Y., Ye, H., He, D., & Wang, L. (2023).** «Towards Revealing the Mystery Behind Chain of Thought: A Theoretical Perspective». *NeurIPS*.
    → Le costruzioni esplicite per aritmetica e programmazione dinamica.

28. **Zhou, H., et al. (2024).** «What Algorithms Can Transformers Learn? A Study in Length Generalization». *ICLR*.
    → L'ipotesi RASP-L. Il ponte fra espressività e apprendibilità.

**Apparato causale**

29. **Elhage, N., et al. (2021).** «A Mathematical Framework for Transformer Circuits». *Transformer Circuits Thread*, Anthropic.
    → Il vocabolario: residual stream, circuiti QK/OV, composizione fra teste.

30. **Geiger, A., Lu, H., Icard, T., & Potts, C. (2021).** «Causal Abstractions of Neural Networks». *NeurIPS*.
    → Le condizioni sotto cui "la rete implementa l'algoritmo X" è un claim verificabile. Da integrare con i lavori successivi dello stesso gruppo su DAS.

**Geometria delle rappresentazioni**

31. **Rigotti, M., Barak, O., Warden, M. R., Wang, X.-J., Daw, N. D., Miller, E. K., & Fusi, S. (2013).** «The Importance of Mixed Selectivity in Complex Cognitive Tasks». *Nature*, 497.
    → Perché un probe che funziona dice quasi nulla.

32. **Bernardi, S., Benna, M. K., Rigotti, M., Munuera, J., Fusi, S., & Salzman, C. D. (2020).** «The Geometry of Abstraction in the Hippocampus and Prefrontal Cortex». *Cell*, 183(4).
    → La CCGP. La voce singola più direttamente importabile nel tuo lavoro.

**Casi aritmetici**

33. **Nanda, N., Chan, L., Lieberum, T., Smith, J., & Steinhardt, J. (2023).** «Progress Measures for Grokking via Mechanistic Interpretability». *ICLR*.
    → Un algoritmo aritmetico interamente reverse-engineered.

34. **Zhong, Z., Liu, Z., Tegmark, M., & Andreas, J. (2023).** «The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks». *NeurIPS*.
    → Stesso task, due algoritmi. Il limite dell'assunzione di universalità.

35. **Quirke, P., & Barez, F. (2024).** «Understanding Addition in Transformers». *ICLR*.
    → I circuiti dell'addizione multi-cifra. Verificare la sede esatta.

36. **Bai, X., Pres, I., Deng, Y., Tan, C., Shieber, S., Viégas, F., Wattenberg, M., & Lee, A. (2025).** «Why Can't Transformers Learn Multiplication? Reverse-Engineering Reveals Long-Range Dependency Pitfalls». arXiv:2510.00184.
    → Il DAG di cache e retrieval dei prodotti parziali.

37. **Merullo, J., Eickhoff, C., & Pavlick, E. (2024).** «Circuit Component Reuse Across Tasks in Transformer Language Models». *ICLR*.
    → L'evidenza positiva sul riuso. Il confronto diretto con la tua domanda.

38. **Lindsey, J., et al. (2025).** «On the Biology of a Large Language Model». *Transformer Circuits Thread*, Anthropic.
    → Chiude la fase: circuiti aritmetici ibridi in un modello di frontiera.

**Esito:** saper dire, davanti a un fallimento, se il livello di spiegazione corretto è la difficoltà intrinseca del problema, la classe di complessità dell'architettura, il regime di training, o l'organizzazione del circuito. Sono quattro risposte diverse e vengono comunemente confuse.

---

### Fase 5 — Il presente (continua, con manutenzione)

*Non una sequenza ma un perimetro. Voci di ingresso per ciascun nucleo; il resto si legge quando serve.*

39. **Wei, J., et al. (2022).** «Chain-of-Thought Prompting Elicits Reasoning in Large Language Models». *NeurIPS*. — ingresso al nucleo G.
40. **Mirzadeh, I., et al. (2024).** «GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models». — la critica, stesso nucleo.
41. **Turpin, M., Michael, J., Perez, E., & Bowman, S. R. (2023).** «Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting». *NeurIPS*. — ingresso al nucleo H.
42. **Lanham, T., et al. (2023).** «Measuring Faithfulness in Chain-of-Thought Reasoning». — le metriche di perturbazione.
43. **Gur-Arieh, et al. (2026).** BONAFIDE. — la ground truth. Già nel tuo piano CoT.
44. **Hao, S., et al. (2024).** «Training Large Language Models to Reason in a Continuous Latent Space» (Coconut). — ingresso a I.5.
45. **Manhaeve, R., Dumančić, S., Kimmig, A., Demeester, T., & De Raedt, L. (2018).** «DeepProbLog: Neural Probabilistic Logic Programming». *NeurIPS*. — ingresso al nucleo K.

**Esito:** saper distinguere i risultati che sopravviveranno alla prossima generazione di modelli da quelli che sono osservazioni su una configurazione contingente.

---

### Nota sul ritmo

Le fasi 1 e 2 sono dodici voci e, con sessioni di poche ore a settimana, occupano realisticamente due mesi. La fase 4 da sola ne occupa altrettanti o più. Il documento intero è un impegno di sei-otto mesi a questo ritmo, il che è appropriato: non è una lista da esaurire ma la struttura di un anno di lettura di sfondo, parallela al lavoro sperimentale.

Se il tempo si comprime, il taglio corretto non è leggere tutto più in fretta ma **eliminare la fase 5** — è lo strato che decade — e tenere intere le prime quattro.

---

## 14. Indice trasversale — le distinzioni

Se il documento serve a una cosa sola, è questa. Ogni distinzione, con i lavori che la portano.

| # | Distinzione | Portata da |
|---|---|---|
| 1 | **Logica ≠ teoria del ragionamento** | Harman; Stenning & van Lambalgen |
| 2 | **Livello computazionale ≠ algoritmico ≠ implementativo** | Marr |
| 3 | **Competenza ≠ performance** | Wason; Chomsky (per lo sfondo); Dasgupta |
| 4 | **Reasoning *to* ≠ reasoning *from* an interpretation** | Stenning & van Lambalgen |
| 5 | **Inferenza ≠ verbalizzazione dell'inferenza** | Penn, Holyoak & Povinelli; Luria; Scribner & Cole |
| 6 | **Processo ≠ report** | Nisbett & Wilson; Gazzaniga; Turpin; BONAFIDE |
| 7 | **Plausibilità ≠ importanza causale ≠ faithfulness** | Lanham; BONAFIDE |
| 8 | **Decodificabile ≠ astratto** (generalizza cross-condition) | Rigotti; Bernardi (CCGP) |
| 9 | **Rappresentazione ≠ uso causale ≠ riuso cross-task** | Geiger; Merullo; Todd |
| 10 | **Difficoltà del problema ≠ limite dell'agente** | Cook & Reckhow; Haken *contro* Merrill & Sabharwal |
| 11 | **Difficoltà assoluta ≠ difficoltà relativa al sistema di prova** | Haken; Ben-Sasson & Wigderson |
| 12 | **Limite empirico ≠ limite espressivo** | Merrill & Sabharwal *contro* Mirzadeh, Dziri |
| 13 | **Trovare una dimostrazione ≠ verificarla** | Cook & Reckhow; nucleo K |
| 14 | **Punteggio uguale ≠ misura confrontabile** | psicometria (invarianza di misura); Chollet |

Una quindicesima, implicita e senza un lavoro singolo che la porti bene: **interpolazione ≠ composizione**. È lo spazio più aperto del documento. La CCGP di Bernardi è, fra le misure esistenti, quella che le si avvicina di più, ed è nata in un altro campo.

---

## 15. Campi adiacenti tenuti fuori, e perché

Documentare le esclusioni serve quanto documentare le inclusioni: impedisce di riaprire ogni sei mesi la stessa decisione.

- **Reasoning procedurale / planning classico.** STRIPS, ricerca euristica, PDDL. Escluso perché la nozione di ragionamento è la ricerca in uno spazio di stati, che è un problema tecnico distinto e con una letteratura autosufficiente. Rientra se il lavoro tocca il post-training o gli agenti; la porta d'ingresso in quel caso è PlanBench e la linea Kambhampati (già in G.2).
- **Teoria dei giochi epistemica.** Conoscenza comune, modelli level-k e cognitive hierarchy (Camerer). Ragionamento su ragionamento altrui. Escluso perché rilevante solo in contesti multi-agente. Una riga qui è sufficiente finché non lo diventano.
- **Ragionamento giuridico e medico.** Letterature ricche sull'inferenza sotto standard di prova e sull'incertezza diagnostica. Escluse perché il valore è quasi tutto nel dominio applicativo.
- **Logica modale, epistemica, temporale.** Escluse come corpo, incluse per riferimento se servono per un formalismo specifico. Il rischio è che si porti dietro un apparato tecnico ampio con basso ritorno sulla domanda centrale.
- **NeuroAI in senso lato.** Escluso deliberatamente, nonostante il nucleo J. Il criterio è quello enunciato lì: metodi e distinzioni sì, transfer dei risultati no. La parte della letteratura che pratica il transfer dei risultati è quella meno solida.

---

## 16. Manutenzione

- **Strato portante:** nessuna revisione. Rilettura selettiva.
- **Strato di stato dell'arte:** revisione ogni 12–18 mesi. Alla revisione, la domanda non è "cosa è uscito di nuovo" ma **"quale voce del portante è stata messa in discussione?"**. Se la risposta è nessuna, la revisione ha prodotto solo rumore.
- **Regola di ingresso:** un lavoro nuovo entra solo se cambia una predizione o preempta un'obiezione nominabile. Le rassegne non entrano mai, salvo come punto di ingresso a un'area nuova, e in quel caso vengono sostituite dai primari appena letti.
- **Regola di uscita:** se una voce non è stata usata — citata, contestata, o impiegata per formulare un'ipotesi — in due cicli di revisione, esce. Le voci del nucleo A sono esenti.
- **Segnale di allarme:** se in sei mesi il documento cresce più del 20% senza che nessuna distinzione della sezione 14 sia cambiata, sta diventando una pila.

---

## Nota sulle citazioni

Anni e sedi sono riportati per come li conosco al maggio 2026. Per i lavori 2025–2026 e per alcune sedi di conferenza conviene una verifica prima di citarli in un contesto formale; lo stesso vale per alcune date della letteratura neuroscientifica e di proof complexity, dove ho riportato l'anno della pubblicazione principale e non sempre quello della versione preliminare. I classici (Wason, Nisbett & Wilson, Fodor & Pylyshyn, Harman, Goodman, Pearl, Johnson-Laird, Marr, Luria) sono stabili.
