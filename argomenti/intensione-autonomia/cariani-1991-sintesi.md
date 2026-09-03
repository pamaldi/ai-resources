# Cariani 1991 — Dispositivi che costruiscono i propri sensori ed effettori

**Riferimento**: Cariani, P. (1991). *Some epistemological implications of devices which construct their own sensors and effectors*. In Varela, F. & Bourgine, P. (a cura di), *Towards a Practice of Autonomous Systems*, MIT Press, 484–493.

Sintesi ragionata delle riflessioni contenute nell'articolo, con le connessioni contemporanee e i punti in cui l'argomento è attaccabile.

---

## 1. L'impianto: la relazione di modellizzazione

L'articolo parte da una nozione che Cariani chiama «molto antica e biologica»: gli organi di senso determinano le categorie con cui un organismo percepisce il mondo, gli organi effettori determinano le categorie con cui può agire su di esso. In mezzo sta un meccanismo di coordinazione.

Tradotto in termini astratti, sono tre funzionalità:

```
sensing        →  misurazione
coordinating   →  computazione
effecting      →  controllo
```

Prese insieme, e incorporate nel modo giusto, costituiscono una **relazione di modellizzazione** — la stessa struttura che si trova in un organismo, in un dispositivo robotico e in un modello scientifico.

### I tre assi semiotici

La figura 1 dell'articolo organizza il tutto su tre assi indipendenti:

| asse | cosa riguarda |
|---|---|
| **semantico** | il rapporto tra stati interni e mondo — determinato da sensori ed effettori |
| **sintattico** | le relazioni tra stati interni — la computazione |
| **pragmatico** | le strutture valutative che modificano la struttura interna per migliorare la performance |

Per gli organismi biologici il test pragmatico è sopravvivenza e riproduzione; per i dispositivi artificiali **i criteri valutativi sono fissati dal progettista-utente**.

### Una definizione minima di categoria

Un organo sensoriale fa una distinzione primitiva sul mondo producendo due o più esiti possibili a seconda della sua interazione con l'esterno. Un recettore che stesse *sempre* nello stesso stato non veicolerebbe alcuna informazione.

> Servono almeno due stati perché ci sia una categoria. Recettori che interagiscono col mondo in modi diversi funzionano come **finestre diverse** sul mondo esterno.

### La causalità circolare

Sensori ed effettori determinano la semantica *immediata* degli stati interni. La parola «immediata» è enfatizzata perché la causalità tra percepire, coordinare e agire è **circolare**: un'azione modifica le percezioni successive, che influenzano le azioni successive.

Riferimenti: Uexküll 1926, le relazioni causali circolari nella cibernetica di Wiener e McCulloch, e la teoria del controllo percettivo di Powers — *i regolatori efficaci aggiustano il proprio comportamento in modo da produrre una percezione desiderata*.

### Quando è lecito parlare di «computazione»

Passaggio che vale la pena isolare, perché regge tutto il resto dell'argomento.

Più la coordinazione è affidabile, più la mappatura assomiglia a una funzione. Quando è completamente affidabile si può descrivere il sistema come uno **state-determined system** (Ashby), descrivibile per intero in termini di operazioni sintattiche formali — ed è in quelle circostanze che è giustificato parlare di «computazioni».

Nel caso ideale:

> la coordinazione implementa una relazione **puramente sintattica** all'interno dell'insieme degli stati interni, mentre sensing ed effecting implementano relazioni **puramente semantiche** col mondo.

---

## 2. Filogenesi e ontogenesi: chi fissa l'alfabeto

Due tempi dell'apprendimento, con una divisione del lavoro convenzionale:

```
filogenesi   →  QUALI distinzioni sono possibili       le categorie di base
ontogenesi   →  COSA fare, data una distinzione        le mappature percetto-azione
```

Cariani riporta questa come la visione standard, la definisce valida «come prima approssimazione», e poi la incrina.

### La crepa: il sistema immunitario

Il caso che porta è l'esempio ovvio di categorie nuove formate **entro la vita dell'individuo**: un array di sensori molecolari evoluto per riproduzione differenziale delle cellule che producono anticorpi capaci di riconoscere molecole estranee.

> L'insieme delle distinzioni che il sistema immunitario può fare sul mondo **evolve nel tempo**.

Le relazioni funzionali tra valutazione dei sensori (quanto un anticorpo lega un antigene) e aggiustamento strutturale sono analoghe a quelle dell'evoluzione morfologica — solo compresse nella scala di una vita.

### E il cervello

Il caso è dichiarato meno netto. Per la formazione di strutture concettuali nuove, dice, bisognerebbe guardare a come pattern di scarica neurale **continui e analogici** — per esempio le distribuzioni degli intervalli fra spike — vengano trasformati in **modi discreti e globali** di rappresentazione e azione.

> La nascita di una categoria nuova è un nuovo modo di discretizzare un segnale continuo.

*Nota*: è la stessa domanda della quantizzazione in una rete neurale, posta sul sistema uditivo nel 1991.

---

## 3. La distinzione centrale: ottimizzare le categorie vs ottimizzare dentro le categorie

Il cuore concettuale dell'articolo.

| | oggetto | processo |
|---|---|---|
| **ottimizzazione delle categorie** | quali distinzioni sono disponibili | ricerca **semantica** |
| **ottimizzazione dentro le categorie** | cosa fare, date quelle distinzioni | ricerca **sintattica** |

### Rapporto con intensione ed estensione — e dove NON coincidono

Viene naturale accostare questa coppia a quella logica:

```
sintattico   ~   intensionale    riguarda la FORMA, il "come"
semantico    ~   estensionale    riguarda il RIFERIMENTO, il "cosa"
```

Fin lì è un'analogia utile: la ricerca sintattica di Cariani opera *dentro* un vocabolario dato — trova l'algoritmo migliore per categorie fissate — proprio come l'intensione, in senso ampio, riguarda la struttura interna di un'espressione e non ciò che essa denota.

**Ma l'equivalenza si rompe su due punti:**

1. Il «semantico» di Cariani non è l'estensione di Carnap. Per Cariani è il *rapporto causale* tra stati interni del dispositivo e il mondo — più vicino al riferimento (*Bedeutung*) di Frege che a un insieme di oggetti. L'estensione di un predicato è un insieme; il "semantico" di Cariani è una relazione tra un trasduttore e ciò a cui risponde.
2. La ricerca semantica di Cariani non opera sull'estensione di un predicato già dato: **sceglie quale vocabolario esista**. Carnap lavora sempre dentro un linguaggio fissato e chiede quale sia il riferimento di un predicato; Cariani chiede chi decida quali predicati esistano.

```
Carnap     l'estensione è DETERMINATA dall'intensione, per un vocabolario dato
Cariani    la ricerca semantica CREA il vocabolario stesso
```

Sono due livelli diversi: uno interno a un linguaggio, l'altro sulla scelta del linguaggio. L'imparentamento è reale — entrambe le coppie separano «cosa riguarda il mondo» da «cosa riguarda la manipolazione interna» — ma non sono la stessa distinzione. Trattarle come intercambiabili è il tipo di collegamento che sembra pulito e non regge a uno sguardo attento. *(Apparato completo su intensione/estensione: bibliografia unificata, §0-bis.)*

### L'analogia scientifica

Nel lavoro di uno scienziato:

- **ottimizzare le categorie** = scegliere quali strumenti costruire e quali grandezze misurare — *trovare le relazioni appropriate tra il mondo e le variabili di stato del modello, cioè le misure giuste da fare*
- **ottimizzare le mappature** = date le misure, trovare l'algoritmo che genera le predizioni migliori

Inventare il termometro e trovare la legge dei gas sono attività diverse — e senza la prima la seconda non è nemmeno formulabile.

Le due, dice Cariani, **rappresentano due generi diversi di conoscenza acquisita**, e ciascuno corrisponde a un tipo diverso di dispositivo costruibile.

### La metafora hardware / software

```
hardware    fissa QUALI stati sono possibili       = le categorie
software    sceglie tra quegli stati               = le mappature
```

Il software gira **dentro i vincoli dell'hardware**: può fare qualunque cosa, ma se non c'è un sensore per l'infrarosso nessun programma lo vede.

### La constatazione, e la frase che pesa

> Abbiamo dispositivi adattivi che ottimizzano le computazioni che eseguono — macchine addestrabili, reti neurali, algoritmi genetici — ma **non abbiamo ancora dispositivi che facciano evolvere il proprio hardware**: i loro sensori, il loro hardware computazionale, i loro effettori.

E:

> Molta attenzione è stata dedicata all'adattamento nel dominio computazionale, **estremamente poca all'adattamento nei domini del sensing e dell'effecting**.

*Osservazione*: il campo non ha scelto il problema più importante, ha scelto quello su cui si può iterare. Il software si modifica a costo zero mille volte al secondo; i trasduttori sono materia.

### Come nasce una distinzione nuova

In generale richiede la **costruzione adattiva di una nuova struttura materiale** che interagisca con l'ambiente in modo diverso dai sensori esistenti. Se migliora la performance, viene stabilizzata e incorporata nelle specifiche costruttive del dispositivo.

Due vie: parte del dispositivo stesso, oppure **protesi** — un oggetto interposto che modifica il rapporto tra sensori esistenti e mondo.

E l'osservazione sull'uomo nel ciclo:

> In tutti gli esempi artificiali citati, **gli esseri umani fanno parte del ciclo**. Sono gli esseri umani a costruire i nuovi tipi di sensori, i computer più grandi, gli effettori più potenti.

---

## 4. Il dispositivo di Pask

L'unico artefatto che, per Cariani, abbia mai attraversato il confine.

### Il meccanismo

Un array di elettrodi immerso in una soluzione di **solfato ferroso e acido solforico**. Facendo passare corrente crescono filamenti dendritici di ferro tra coppie di elettrodi; allocando la corrente in modo adattivo — cambiando la quota relativa di ciascun elettrodo — la crescita dei filamenti può essere **guidata**.

I filamenti sono instabili: senza corrente si ridissolvono nell'acido. C'è competizione permanente tra crescita e dissoluzione, e sopravvive ciò che viene alimentato.

```
1. la chimica fa crescere filamenti in modo semi-casuale
2. una configurazione cambia resistenza in presenza di suono → ricompensa
3. ricompensa = più corrente a quegli elettrodi
4. più corrente = quei filamenti crescono, gli altri si dissolvono
```

**Mezza giornata**: il dispositivo distingue presenza e assenza di suono, e poi due frequenze diverse.

### La frase decisiva

> Tutto questo poteva essere realizzato **senza una teoria fisica specifica** di come i filamenti si formino e si estendano, più o meno nello stesso modo in cui opera la ricerca «cieca» di substrati sensoriali efficaci nell'evoluzione biologica.

Pask non sapeva come un filamento di ferro potesse diventare sensibile al suono. Non ha progettato un microfono. Ha allestito un ambiente in cui strutture arbitrarie potevano crescere, e un criterio che premiava quelle che si comportavano in un certo modo.

### Il contrasto con una rete neurale

Cariani mette l'osservazione che chiude ogni scappatoia:

> Si potrebbe implementare una rete neurale contemporanea in questo modo — i pesi tra elementi sarebbero proporzionali alle conduttanze tra elettrodi. **Invece** Pask ha guidato l'assemblaggio a costruire strutture sensibili al suono.

La stessa vaschetta poteva essere usata come normale rete addestrabile. **La differenza non è nel materiale: è in cosa viene premiato.** In una rete si premia la mappatura giusta dentro un insieme di input dato; qui è stata premiata la capacità di produrre un input nuovo.

Il dispositivo non ha imparato a classificare meglio il suono. Ha imparato a **sentirlo**, partendo da un sistema in cui il suono non era un input.

### Il verdetto

> Nel corso dell'addestramento una nuova categoria percettiva (una distinzione primitiva) è stata creata dal dispositivo **de novo**. Questo processo è fondamentalmente distinto dalla costruzione di distinzioni complesse a partire da combinazioni logiche di distinzioni preesistenti, come si trova praticamente in **tutte** le strategie contemporanee di intelligenza artificiale.

### McCulloch

Dalla prefazione al libro di Pask del 1960, citata da Cariani:

> Con questa capacità di costruire o selezionare i filtri appropriati sui propri input, un dispositivo del genere spiega il problema centrale dell'epistemologia sperimentale. Gli enigmi dell'equivalenza degli stimoli o dell'azione dei circuiti locali nel cervello restano soltanto problemi parrocchiali.

---

## 5. Trovare i feature primitive giusti per una rete neurale

La sezione più direttamente tecnica.

### L'argomento del plateau

Tutti i classificatori esistenti operano dentro insiemi **fissi** di feature primitive, che il progettista ha stabilito essere appropriate al problema. Il dispositivo poi cerca adattivamente un algoritmo che partizioni lo spazio delle combinazioni.

Se le feature sono informativamente inadeguate, la performance si ferma a un tetto — e nessuna ottimizzazione dell'algoritmo lo supera, perché **l'informazione non c'è**.

Corollario dal paper del 1998, stessa tesi in forma più netta: se l'informazione richiesta semplicemente non è nell'insieme di feature fornito, *nessuna quantità di computazione sulle feature fornite può correggere il problema*.

### Il feature engineering è già ottimizzazione delle categorie

L'osservazione più difficile da liquidare dell'articolo:

> Quando una rete neurale non migliora oltre un certo livello, nonostante i migliori sforzi dei progettisti per ottimizzare l'algoritmo, **spesso quei progettisti vanno a cercare osservabili nuovi o più adatti**, alterando così la dimensionalità e la semantica esterna dello spazio in cui stanno cercando. A volte funziona.

Il passo non manca. Manca **dentro il sistema**: a farlo è una persona.

### L'argomento della dimensionalità

Tecnico, trasferibile, e sorprendentemente moderno:

> Se si aggiunge un osservabile, lo spazio delle feature cresce di una dimensione, e **quello che era un minimo locale nel vecchio spazio può facilmente essere un punto di sella in quello aumentato**. L'hill-climbing, oltre a seguire i gradienti locali verso l'alto, può quindi coinvolgere aumenti nella dimensionalità della collina stessa.

Cioè: **far crescere l'inventario non è una comodità, è un modo di uscire da un minimo locale.**

E Cariani nota perché la cosa non si discute: si assume tacitamente che i sensori — e quindi le feature primitive — siano fissi, e che l'adattamento computazionale sia l'unica forma di apprendimento possibile.

### Una proposta concreta

Costruire dispositivi alla Pask e usarli come **front-end** per reti neurali e macchine addestrabili. Ogni volta che la performance non migliora entro l'insieme corrente di primitive, l'assemblaggio cerca primitive migliori, e il ciclo ricomincia.

---

## 6. Aumentare i modi di segnalazione indipendenti

La sezione più originale, e quella con la maggiore risonanza contemporanea.

### Il meccanismo

In una rete di elementi capaci di far evolvere sensori ed effettori, ogni volta che nasce una nuova combinazione effettore-sensore tra due elementi, il sensore di uno può rilevare le azioni del nuovo effettore dell'altro. Se sensore ed effettore sono diversi dai preesistenti, il canale che ne risulta è **almeno parzialmente ortogonale** a quelli già presenti.

Esempio dato: un elemento evolve una sensibilità primitiva al suono, un altro un modo primitivo di produrre suono → la rete ha un canale nuovo.

> Strategia generale per aumentare la banda: **proliferare nuovi modi di segnalazione ortogonali.**

### Il confronto che anticipa la superposizione

> Un vantaggio maggiore dell'aumentare la dimensionalità rispetto al proliferare stati dentro le dimensioni esistenti è che segnali diversi possono essere tenuti separati; pattern diversi non devono interferire tra loro — **come accade invece in molti tipi di reti connessioniste** — e i nuovi segnali non devono essere combinazioni logiche dei preesistenti.

Più: consente il **multiplexing**, la trasmissione simultanea di tipi di segnale diversi.

*Nota*: è una descrizione dell'interferenza da superposizione con la diagnosi corretta — quando hai più cose da rappresentare che dimensioni disponibili, le rappresentazioni si pestano i piedi. Scritta nel 1991.

### Il neurone come elemento misto digitale-analogico

La parte più speculativa, ed è il programma di ricerca personale di Cariani.

Invece di trattare il neurone come un elemento logico discreto che somma input sinaptici per produrre **un solo output scalare**, considerarlo capace di trasmettere informazione **multidimensionale** attraverso le distribuzioni degli intervalli fra spike.

Regolando i processi di recupero della membrana e le risonanze elettriche, un neurone potrebbe far proliferare nuovi pattern temporali di scarica, aumentando la dimensionalità dell'informazione codificata nei propri treni di spike — possibilmente tramite allocazione adattiva di canali ionici e pompe su porzioni locali di membrana, contingente alla loro storia di eccitazione.

In aggiunta all'alterazione delle connettività tramite pesi sinaptici (concepiti come scalari), si avrebbe **un meccanismo di apprendimento operante nel dominio della frequenza**, con i vantaggi conferiti dalle ortogonalità parziali di intervalli diversi.

E reti ricorrenti di tali elementi potrebbero far proliferare nuovi modi risonanti, aumentando il numero di stati globali stabili disponibili alla rete nel suo complesso.

> Cariani dichiara lui stesso il carattere ipotetico: *che questa organizzazione funzionale risulti o meno operante nel sistema nervoso*, reti artificiali miste digitale-analogiche si possono comunque costruire su queste linee.

---

## 7. L'osservatore epistemicamente autonomo

### La definizione

Un dispositivo è **epistemicamente autonomo** quando fa entrambe le cose:

1. costruisce le proprie categorie per percepire e agire
2. ottimizza la mappatura tra quelle categorie

Con un limite dichiarato, che è la parte onesta della definizione: **entro i limiti imposti dalla loro struttura materiale**, tali dispositivi determinano la natura di ciò che vedono e di come agiscono sul mondo.

Non autonomia assoluta: autonomia **relativa al progettista**. Il concetto è graduabile, non binario — ed è questo che lo salva dal misticismo.

### La famiglia concettuale

Cariani si posiziona esplicitamente accanto a:

| concetto | autore |
|---|---|
| chiusura semantica | Pattee 1982 |
| chiusura organizzativa | Maturana 1981, Varela 1979 |
| dispositivo automodificante | Kampis 1991, Csanyi 1989 |
| sistema anticipatorio | Rosen 1985, 1991 |

*Nota*: è la sezione che colloca l'articolo sulla giuntura tra la tradizione logico-computazionale e quella enattivo-biologica. Pubblica nel volume curato da Varela e Bourgine, cita gli enattivisti, ma il suo argomento resta semiotico-computazionale.

### La giustificazione finale

> Una volta che abbiamo il concetto di autonomia epistemica e comprendiamo le strutture materiali necessarie a sostenere questo tipo di organizzazione funzionale, abbiamo i mezzi per costruire un soggetto autonomo: **un punto di vista indipendente dal nostro, capace di dirci qualcosa che non sappiamo già**.

Questo riformula l'intera impresa. Il fine non è costruire macchine coscienti, né macchine più potenti. È costruire **strumenti che possano sorprendere** — perché un sistema che opera dentro le tue categorie può solo ricombinare cose che ci avevi messo tu.

È la stessa ragione per cui si costruisce un telescopio nuovo invece di guardare meglio le fotografie vecchie.

---

## 8. Dove l'argomento è vulnerabile

Tre punti, in ordine di gravità.

### 8.1 La divisione semantico / sintattico è in parte definitoria

Dalla premessa che la coordinazione implementi relazioni *puramente sintattiche* mentre sensori ed effettori implementino relazioni *puramente semantiche*, segue **immediatamente** che la computazione non possa creare nuovi primitivi semantici.

Non è una scoperta: è una conseguenza della definizione. Chi contesta l'argomento attacca lì.

### 8.2 La metafora hardware / software regge male sui computer universali

In una macchina general-purpose l'hardware è già universale, e la distinzione fatica ad applicarsi. La risposta di Cariani sarebbe che un computer universale resta universale *solo dentro il vocabolario che i suoi trasduttori gli forniscono* — ma questo rimanda al punto 8.1.

### 8.3 Se i primitivi vengono dalla chimica, chi li ha creati?

Il dispositivo di Pask non inventa la sensibilità al suono: la **seleziona** da uno spazio di configurazioni fisiche che l'acido solforico rendeva già disponibile. La creatività sta nella materia, e il dispositivo fa selezione.

Cariani risponderebbe che è esattamente ciò che fa l'evoluzione biologica, e che chiamarla per questo non-creativa svuota la parola. È una risposta ragionevole, non una risposta conclusiva.

### 8.4 Un'unica prova di esistenza

L'intero argomento costruttivo poggia su **un solo dispositivo**, degli anni Cinquanta, ricostruito da documenti e testimonianze frammentarie. Nessuno lo ha rifatto in settant'anni.

Il che è, a seconda di come lo si legge, la conferma della difficoltà del problema oppure il segno che il programma non era praticabile.

---

## 9. Cosa resta, oggi

**La distinzione**, che è il lascito principale e si applica ovunque:

> Questo sistema può cambiare il proprio vocabolario, o solo cosa dice con esso?

**L'argomento della dimensionalità**, che è tecnico e trasferibile: aggiungere una dimensione può trasformare un minimo locale in un punto di sella. È il ponte più diretto con qualunque questione moderna sulla crescita di un inventario discreto.

**L'anticipazione dell'interferenza da superposizione**, con la diagnosi corretta e una soluzione — aumentare le dimensioni invece di riempire quelle esistenti — che nessuna architettura contemporanea implementa in corso d'opera.

**L'osservazione sull'uomo nel ciclo**: il feature engineering è ottimizzazione delle categorie eseguita da una persona. Non manca il passo; manca *dentro* il sistema.

E la formulazione che riassume tutto, valida oggi come nel 1991:

> Un sistema di machine learning ha la sua filogenesi — architettura, spazio delle feature, tokenizer, spazio delle azioni. Scelte fatte prima che veda un dato, che nessuna quantità di addestramento rivede. L'addestramento è ontogenesi: ottimizza mappature dentro categorie che non ha scelto.
>
> Solo che in questo caso la filogenesi non è cieca. **È una persona.**