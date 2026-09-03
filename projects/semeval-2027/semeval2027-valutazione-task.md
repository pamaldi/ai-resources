# SemEval 2027 — valutazione task (sessione del 3 settembre 2026)

Criterio di selezione: **verificabilità formale**. La task deve avere un punto in cui un
componente simbolico *decide* invece di *stimare*. Riferimento: pipeline NS-EDL
(Task 11 SemEval 2026, 96,34% acc., TCE ~1.02).

---

## Correzioni di calendario

Dalla pagina ufficiale SemEval-2027:

- Sample data: **8 agosto 2026** (non 15 luglio)
- Training data: **8 settembre 2026** (non 1° settembre)
- Valutazione: 10–31 gennaio 2027
- Paper: febbraio 2027 · Notifica: marzo 2027 · Camera-ready: aprile 2027

Nota: sul sito ufficiale la Task 2 è ancora registrata come **CoCo-NLI**, mentre il repo
è già stato rinominato DiCo-NLI. Stessa task, stessi autori. Da tenere presente in fase
di citazione.

---

## Task 11 — VAKRA-Advanced (IBM)

### Stato

Non è una task futura: **è già tutta pubblica e girevole**. Train e test su HuggingFace
(`ibm-research/VAKRA`), ambiente eseguibile su GitHub (`IBM/vakra`), leaderboard live su
HF Spaces. Blog di error analysis IBM del 15 aprile 2026.

Costo d'ingresso: ~35 GB di dati, Docker con 8 GB+ (cap. 4 va in OOM con 2 GB), Python
3.11, provider LLM. Test totale ~5.200 dialoghi, catene fino a 10-12 tool call.

### Struttura del punteggio (il pezzo decisivo)

Valutazione **a cascata**:

1. (solo cap. 4) aderenza alla policy verificata **programmaticamente**
2. confronto della traiettoria di tool call con la gold
3. giudizio LLM sulla correttezza (fallback, adattato da CRAG)
4. giudizio LLM sulla groundedness

Tre implicazioni tattiche:

- **Il confronto è orientato al recall**: gold ⊆ predetto, order-invariant. Chiamare in
  più non penalizza (salvo policy); chiamare in meno sì.
- **Le capability sono equipesate ma di dimensioni diverse** (2.077 / 1.597 / 869 / 644).
  Un sample di cap. 4 vale ~3,2× uno di cap. 1. Dentro cap. 4 le query multi-source
  pesano il doppio. → il set più piccolo è il più redditizio, ed è quello formale.
- **Solo l'ultimo turno è valutato**, anche nei dialoghi multi-turno.
- **Il test è più difficile del train per costruzione**: cap. 1 ha 33 domini in train vs
  54 in test; cap. 3 ha max 3 hop in train vs 5 in test. Nessun fitting per dominio.

### Dove morde il simbolico

**Cap. 4 — policy come gate deterministico (forte).**
Le policy sono in linguaggio naturale ma templatiche: `additional_instructions` ha solo
**26 valori distinti su 664 dialoghi** di test. Schema fisso ⟨categoria-topic, glossa,
classe di tool permessa/vietata⟩ → compilabile in regole. La parte neurale residua è solo
`topic(Q, C)` su poche classi; l'enforcement è un filtro sulla tool list *prima* della
scelta → violazione impossibile per costruzione (analogo di SoftCons = 1.0).

Il baseline IBM impone le policy concatenandole nel prompt. Il blog documenta che i
modelli o violano il vincolo o non recuperano informazione sufficiente.

⚠️ Alcune policy sono **distrattori** (inapplicabili alla query). Serve un test di
applicabilità oltre all'enforcement: un falso positivo ti amputa il retriever necessario.
È la stessa curva coverage/precisione di DiCo-NLI.

**Cap. 1 e 3 — type-checking dei piani (buono).**
Le catene BI-API sono dataflow tipati: `get_data` restituisce handle + `key_details` con
dtype; le chiamate successive referenziano `data_label` e `key_name`. La validità di un
piano è decidibile prima dell'esecuzione. Gli errori documentati sono esattamente lì
(nomi di argomenti errati su SLOT-BIRD, selezione tool errata su SEL-BIRD).
→ generi k piani, scarti i mal tipati, voti sui superstiti. Zero training.

**Cap. 2 — non morde.** Selezione di 1 tool su 6-328 (media 116), 1 sola call per sample.
È ranking. Stesso verdetto di RETECO.

### Problema aperto

Il **PolicyJudge non è nel repo**. L'evaluator accetta `--policy-judge-path` ma il file va
richiesto aprendo una issue. Se il contributo è il gate di policy, oggi non è misurabile
in locale.

### Verdetto

**Seconda opzione, opportunistica, limitata a cap. 4 (+ eventualmente 3).**
Non un run full-benchmark. L'edge non può essere "un agente più grosso": deve essere
"a parità di LLM, violazioni = 0 e piani mal tipati = 0".

---

## Task 6 — MMCultureQA — **NO**

Ranking ufficiale: **BERTScore F1**. BLEU/ROUGE solo per contesto, analisi LLM eventuale.

- La verità di base è una stringa; la correttezza è definita *dalla metrica*, che è essa
  stessa un modello neurale. Nessun punto in cui inserire un validatore.
- **Peggio di RETECO**: lì almeno la rilevanza è discreta.
- BERTScore ha floor alto e range utile compresso → classifica decisa da rumore.
- Premia lo **style matching** (le risposte gold hanno forma molto stereotipata).
- L'unico aggancio (consistenza audio/testo e cross-lingua sugli stessi item, che sarebbe
  garantibile per architettura) **non è nella metrica**: le tracce sono valutate
  separatamente.
- Costi alti (VLM + ASR su arabo dialettale), concorrenza con QCRI e gruppi nativi,
  trasferimento zero dallo stack esistente.

Da salvare: solo il paper OASIS (arXiv:2510.06371) come lettura.

---

## Task 7 — CLaS — **NO, ma il più interessante dei no**

Steering della lingua di output via interventi inference-time. Modelli fissi:
Llama-3.1-8B-Instruct e tiny-aya-global. Tracce T1 (90 coppie), T2 (100), T3 (19×3),
bonus refusal. 12 classifiche totali.

**Metrica** (dall'abstract di CLaS-Bench, non dalla pagina della task): media armonica di
**controllo della lingua** e **rilevanza semantica**.

### Il lato buono

Metà della metrica è quasi-decidibile (LID = classificatore duro, non similarità di
embedding). E c'è una mossa a garanzia architetturale: per i target in script non latino
(`ja` `zh` `ru` `ar` `ko` `hi` `el` `fa` `th` `uk` — 10 su 20) puoi mascherare i logit al
sottoinsieme del tokenizer compatibile → controllo lingua ≈ 1.0 per costruzione.

### Perché comunque no

- La **media armonica neutralizza la versione banale**: controllo perfetto + contenuto
  spazzatura = 0. Il lavoro vero resta steering, non logica.
- Gli organizzatori **hanno già mappato lo spazio**: CLaS-Bench valuta DiffMean, probe,
  neuroni lingua-specifici, PCA/LDA, SAE, prompting — e il semplice DiffMean residuale
  vince. Il repo chiede esplicitamente "piccoli miglioramenti a metodi esistenti".
- Trasferimento zero dallo stack. L'unico validatore possibile è un check LID
  post-generazione = best-of-n con filtro, cioè euristica di decoding.
- Submission via codice/Docker su test privato: nessuna iterazione, un bug d'ambiente
  vale zero.
- Legame col corso XAI **tematico, non metodologico** (è la metà post-hoc della
  disciplina; il blocco ILP non tocca nulla).

Lato positivo: costo d'ingresso più basso di tutta la lista, campo piccolissimo
(repo con 0 star).

**Se la si volesse valutare ancora**: leggere la sezione di valutazione di CLaS-Bench
(Findings ACL 2026, pp. 21591–21628) per capire *come* calcolano il language control —
quale LID, a livello di documento o di token. Mezza giornata. Determina se il vincolo di
script è una leva reale o un'illusione.

---

## Task 8 — StereoQueerEval

### Stato

**Nessun sito, nessun repo.** Sulla pagina ufficiale c'è solo il contatto.
Organizzatori: Cignarella, Damo, Marchiori Manerba, Abdolmaleki, Lefever, Nozza.

### Antecedenti (da cui si ricostruisce il formato probabile)

- **HODI** (EVALITA 2023, Nozza et al.): 6.000 tweet italiani, etichetta binaria di odio
  verso persone LGBTQIA+ + span odiosi (rationales).
- **QUEEREOTYPES** (LREC-COLING 2024, Cignarella et al.): due sotto-corpora italiani da
  Facebook/Twitter, stereotipo + dimensioni ortogonali (hate speech, aggressività,
  offensività, ironia; stance nell'altro sotto-corpus). Sviluppato con attivisti di
  un'associazione LGBTQIA+.
- **HODIAT** (WOAH 2025, Damo et al.): estende HODI con aggressività e tipo di target;
  tre annotatori indipendenti tutti membri della comunità, **annotazioni disaggregate
  rilasciate**. Repo: `github.com/HODI-EVALITA/HODI_2023` (accesso su richiesta email).
- "Is Hate Lost in Translation?" (Muti, Marchiori Manerba, Korre, Barrón-Cedeño).

→ Molto probabilmente **multilingue**, non solo italiano.

### Verdetto sul criterio

Verificabilità formale **zero e per scelta**: il gruppo è esplicitamente perspettivista
(rilasciano le annotazioni disaggregate proprio perché non credono in una singola
etichetta vera). Non c'è un teorema da verificare, c'è un disaccordo da modellare.

Unico aggancio: lo spazio delle etichette ha **dipendenze logiche** (aggressività
presuppone odio; il target è definito solo se hateful=1). Consistenza su predizioni
congiunte = stessa forma di DiCo-NLI. E c'è un risultato empirico che lo motiva: in
HODIAT l'addestramento congiunto dei tre label **peggiora** rispetto a quello separato.
Ma il ranking sarà F1 per layer → la garanzia di consistenza non verrebbe premiata.

**Ranking: sopra MMCultureQA, a livello di CLaS.** Fuori dalle prime due.

---

## L'idea che vale più della task: mech int su HODIAT

### Cosa NON fare

"Trovare la direzione dell'annotatore A nel residual stream". Con **n = 3** lo spazio
delle differenze a coppie è bidimensionale per costruzione: non falsificabile. E ogni
direzione trovata è confusa con la calibrazione — se il disaccordo è una soglia diversa
sullo stesso continuum di severità, la "direzione prospettiva" è uno scalare.

### La domanda giusta

> Un modello addestrato sull'aggregato **rappresenta internamente il dissenso**, o
> l'aggregazione cancella la prospettiva minoritaria prima del layer di output?

Con n=3 funziona: servono solo gli item con split **2–1**. Fine-tuning sull'etichetta di
maggioranza → probing lineare layer-wise sull'etichetta *dissenziente*.

Tre esiti, tutti pubblicabili:

| Esito | Interpretazione |
|---|---|
| Decodificabile | Il modello rappresenta il dissenso e lo scarta al decoding → argomento tecnico pro-perspettivismo, dall'interno del modello |
| Decodificabile solo nei layer intermedi | Localizzi il punto di collasso |
| Mai decodificabile | Risultato negativo forte: rappresentazione mono-prospettica |

**Secondo filone nello stesso dataset**: spiegare meccanicisticamente *perché* il
multi-task su hatefulness/aggressività/target collassa. Interferenza nel residual stream,
direzioni non ortogonali, capacità contesa. È un'anomalia dichiarata e non spiegata dagli
autori.

### Ponte con NS-EDL

Non è continuità di macchina (algebra lineare, non Prolog) ma di **principio**: un probe
che segnala "item rappresentazionalmente conteso" è un gate di astensione. Stessa
superficie coverage/accuratezza di DiCo-NLI, con rilevatore interno invece che simbolico.
Astenersi dove il *dissenso* è decodificabile — invece che dove l'entropia dell'output è
alta — è una tesi nuova e difendibile.

### Due avvertenze

- **Framing etico**: "direzione dell'annotatore queer nello spazio delle attivazioni"
  suona come ridurre un'esperienza vissuta a un vettore, davanti a un gruppo che scrive
  positionality statement e lavora con attivisti. "Il modello cancella la prospettiva
  minoritaria?" è un **audit di erasure rappresentazionale**: stessa matematica,
  ricezione opposta.
- **La task non lo premia, e va bene**: partecipazione onesta e non ambiziosa alla shared
  task (accesso ai dati, rapporto con gli organizzatori, system paper breve) + contributo
  di mech int portato altrove (BlackboxNLP, WOAH).

### Costo

**Zero attesa: HODIAT e QUEEREOTYPES esistono già.** Non serve aspettare SemEval.
Esperimento minimo: richiesta accesso HODIAT → isolare gli item 2–1 → fine-tuning sulla
maggioranza → probing lineare layer-wise. Due settimane, una GPU.

Frizione: dati in italiano, infrastruttura di interpretabilità pre-confezionata quasi
tutta anglocentrica. DiffMean e probe lineari funzionano lo stesso; per le feature sparse
(SAE) il pezzo va costruito.

---

## Quadro finale

| Task | Verdetto | Motivo in una riga |
|---|---|---|
| **2 — DiCo-NLI** | **Primaria** | Verificabilità nella metrica, edge architetturale garantito, costo basso |
| **11 — VAKRA cap. 4** | Seconda, opportunistica | Policy formalizzabili (26 template) verificate programmaticamente *dentro* la metrica |
| **10 — AgentRisk** | Aperta | Criterio: policy formali o vaghe? Ora c'è VAKRA come precedente concreto |
| **8 — StereoQueerEval** | No come task | Ma il dataset apre un filone mech int indipendente e già disponibile |
| **7 — CLaS** | No | Metà metrica dura, ma spazio delle soluzioni già mappato dagli organizzatori |
| **6 — MMCultureQA** | No | BERTScore F1: nulla da validare |
| **1 — RETECO** | No | Ranking puro |

**Vincolo di realtà**: tre task in parallelo con valutazione tutte a gennaio 2027 non
stanno in piedi. Il filone mech int è l'unico che si può portare avanti *fuori* da quel
budget, perché non ha scadenza SemEval.

---

## Azioni concrete

**Immediate (costo ~zero)**

- [ ] Issue su `IBM/vakra`: richiedere il PolicyJudge; chiedere se VAKRA-Advanced userà lo
      stesso evaluator, se il test SemEval sarà nuovo (contaminazione: la leaderboard è
      già pubblica), se sono ammesse submission su capability parziali
- [ ] Issue su DiCo-NLI per l'artefatto `NEGATIVE_OTHER` singleton (già in coda)
- [ ] Email a Cignarella per l'accesso a HODIAT

**Prototipi economici (nessun Docker, nessun download da 35 GB)**

- [ ] Scaricare da HF solo il subset `multihop_multisource_with_policies`; estrarre le 26
      policy; contare applicabili vs distrattrici; identificare le "policy updates the
      answer"
- [ ] Parsare i piani gold del train cap. 1 (1.324 sample) e verificare che il
      type-checker accetti il **100%** dei gold → soundness check che rende difendibile
      il gate
- [ ] HODIAT: isolare gli item con split 2–1, contarli, verificare che ce ne siano
      abbastanza per il probing

**Da leggere**

- [ ] CLaS-Bench, Findings ACL 2026 pp. 21591–21628 — solo la sezione di valutazione,
      per chiudere o riaprire la Task 7
