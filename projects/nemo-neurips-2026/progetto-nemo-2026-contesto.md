# Progetto NEmo 2026 — Scoperta autonoma di astrazioni dalla ripetizione

Documento di contesto: sintesi completa dell'idea, della letteratura, dell'architettura e delle decisioni prese. Da usare come base di conoscenza del progetto.

---

## 1. Il target: workshop NEmo 2026

- **NEmo 2026 — Neuro-Symbolic Embodied Intelligence**, workshop a NeurIPS 2026, Sydney, 11-12 dicembre 2026. Sito: https://nemo.semantic.review/
- Temi del workshop: (a) **long-horizon planning** — apprendere/revisionare/verificare modelli di azione simbolici; (b) **LLMs and provenance** — LLM come elicitatori affidabili di domain model, policy prior, generatori di vincoli; (c) **shared semantics** — layer di conoscenza riusabili che colleghino ambienti, affordance, capacità, piani e trace di esecuzione. Motivo conduttore: affidabilità (precondizioni allucinate, domain model fragili come problema di sicurezza).
- **Call for papers non-archival su OpenReview**: long paper ≤ 8 pagine, short paper ≤ 4 pagine (position paper, risultati preliminari, benchmark, demo).
- **Deadline submission: 10 settembre 2026. Notifiche: 29 settembre 2026.**
- Organizzatori: Sapienza (Elena Umili, Emanuele Musumeci, Vincenzo Suriani), WU Vienna (Daniel Dobriy), UniBO (Anna Sofia Lippolis).

**Decisione strategica presa**: puntare a uno **short paper con early results su un toy minimale**, non a un position paper puramente argomentativo. Motivi: (1) l'esperimento è così economico che la sua assenza sarebbe un segnale negativo; (2) il vantaggio comparativo dell'autore è l'implementazione. Il codice non è formalmente richiesto dal CFP, ma nel caso specifico conviene.

---

## 2. L'idea centrale

### Formulazione iniziale
Addestrare un sistema sulle **addizioni** e fare in modo che arrivi **autonomamente alla moltiplicazione**. La moltiplicazione non è statisticamente "più addizione": è addizione *ricorsivamente composta* (`a×b = a + a×(b−1)`). Un modello puramente neurale addestrato sulle addizioni non ci arriva da solo (letteratura su length generalization e shortcut learning).

### L'intuizione chiave: la ripetizione come value function
"Il sistema vede che ripete sempre le stesse cose e cerca autonomamente uno shortcut." Questa intuizione:
- ha un nome: **compressione / MDL** (è il motore di DreamCoder e Stitch);
- ha una radice teorica: **Schmidhuber**, compression progress come reward intrinseca;
- ha una trappola: la compressione da sola trova gli shortcut *sbagliati* (una lookup table memorizzata è anch'essa compressione — è esattamente lo shortcut learning che si vuole evitare).

### La tesi raffinata (il cuore del paper)
> **La compressione è la value function, vincolata dalla correttezza verificata simbolicamente.**

- Il filone self-improvement (Lee et al.) fornisce il **filtro di correttezza**;
- il filone library-learning/MDL fornisce la **spinta a comprimere**;
- il contributo: usare la compressione come segnale intrinseco di valore, ma **gated dalla verifica simbolica**. Senza gate → memorizzazione; senza compressione → non si scopre mai la moltiplicazione.

### La "noia" come criterio computazionale
Non un'emozione ma una condizione: alta ripetitività + alta prevedibilità + elevato costo operativo + opportunità di astrazione → trigger della ricerca di una macro. In pseudocodice: `se frequenza_ripetizione > soglia e costo_totale > soglia allora cerca_macro_azione`.

### Dettagli concettuali importanti
- **Predicato neutro**: il sistema non deve chiamare la scoperta "moltiplicazione" — inventa `operatore1(3,4)=12` e l'equivalenza semantica con la moltiplicazione viene riconosciuta a posteriori, su casi mai visti. Questo evita di contrabbandare il concetto target nel vocabolario e dà una valutazione pulita.
- **Due livelli di compressione, non uno**: la compressione di tracce fisse dà prima astrazioni separate (`a+a → double`, `a+a+a → triple`); per arrivare a `a×b` con b arbitrario serve un secondo passo che astrae il *numero di ripetizioni* come variabile (serve fold/ricorsione nel DSL). Rispecchia lo sviluppo cognitivo (i bambini imparano il raddoppio prima della moltiplicazione generale). Ottimo per la narrazione del paper: il sistema scopre prima ×2, ×3 per compressione, poi la moltiplicazione come meta-compressione.
- **Mattoni di base forniti al sistema** (non la regola target): conteggio, addizione, ripetizione, confronto, composizione di procedure, verifica di ipotesi. Il sistema deve: individuare la ripetizione → proporre una procedura parametrica → verificarla su esempi nuovi → conservarla se corretta, generale, più compatta.

---

## 3. Caso d'uso embodied (taglio NEmo)

Nel setting embodied la "ripetizione" è comportamentale: l'agente nota che emette sempre la stessa sequenza e la comprime in una macro-azione (= option/skill discovery dell'RL gerarchico, ma con la macro *nominata*, *verificata* con regole, e messa in libreria riusabile — che è "self-evolving agents" + "shared semantics" del workshop).

**Scenario: robot di magazzino/confezionamento.** Task: riempire 6 scatole con 4 bottiglie ciascuna. Azioni primitive: `afferra, sposta, deposita, verifica`. Dopo molte ripetizioni il sistema inventa `riempi_scatola(Scatola, Oggetto, Quantità)` e poi `prepara_lotto(NumeroScatole, OggettiPerScatola)`. La moltiplicazione (6×4=24) è la struttura simbolica sottostante. La scoperta importante non è il simbolo matematico ma la capacità di trasformare sequenze ripetitive in **abilità riutilizzabili e parametriche**.

L'aritmetica pura (addizione→moltiplicazione) resta il **probe controllato** — da posizionare come toy example dentro la cornice agentica.

---

## 4. Architettura (prima versione, senza RL)

```
percezione (neurale, o simulata) → fatti simbolici → ASP/clingo pianifica
→ registrazione tracce → rilevatore di ripetizioni
→ proposta macro per compressione/anti-unificazione → verifica clingo → libreria
```

- **Niente RL nella prima versione**: al posto della value function RL, una funzione obiettivo simbolica. Forma: `Costo(H) = 100·errori(H) + λ·lunghezza(H) + μ·azioni_primitive(H) − γ·casi_coperti(H)` — cioè MDL + correttezza (errori pesati al massimo). ASP supporta ottimizzazione nativamente (`#minimize`). L'RL diventerebbe utile solo per presa fisica, forza, traiettorie, scelta tra macro — fase successiva.
- **"Embodied" non implica RL**: l'agente è embodied perché percepisce, ha un corpo (reale o simulato), agisce, osserva conseguenze, aggiorna la conoscenza.
- Stack: rete supervisionata per percezione (o percezione simulata), ASP/clingo per pianificazione e verifica, Python per analisi tracce, sistema ILP per le regole.

### Correzioni tecniche importanti (da mantenere nel paper)
1. **"ILASP inventa la macro" non è accurato**: ILASP/FastLAS apprendono regole dentro un mode bias su predicati *esistenti*; creare un simbolo nuovo è **predicate invention**, che non fanno nativamente. Alternative oneste: (a) **Popper** (Cropper) o Metagol/MIL, che fanno predicate invention; (b) la strada consigliata: **la compressione propone e nomina** (anti-unificazione delle tracce ripetute → template parametrico → nome fresco), e ILASP entra *dopo* per apprendere/raffinare la definizione del predicato ormai nominato. La divisione "compressione propone, logica verifica" va dichiarata esplicitamente.
2. **Rischio "neurale decorativo"**: se la rete fa solo percezione banale, i revisori diranno che è un sistema simbolico con frontend percettivo. Opzioni: dichiararlo (il tema shared semantics lo copre) oppure far lavorare l'interfaccia (percezione rumorosa, grounding fallibile, verifica simbolica che recupera dagli errori). 
3. **Ricorsione su interi in clingo**: il grounding esplode — per la parte aritmetica pura **Prolog è più adatto**; ASP resta la scelta giusta per pianificazione, vincoli, ottimizzazione delle macro. (Datalog scartato: domini finiti, ricorsione procedurale scomoda.)
4. **JEPA**: valutato come world model neurale (prevedere conseguenze, segnalare transizioni regolari/prevedibili → trigger della "noia"). Decisione: **fuori dallo scope della submission**, paragrafo di future work. Integrarlo davvero è un progetto a sé.
5. **Scope per la deadline**: niente telecamera, niente robot reale, niente JEPA. Versione minima: **mondo simulato a stato simbolico** (griglia/blocks world del magazzino), logging tracce, rilevatore di ripetizioni, invenzione macro per compressione, verifica clingo con `#minimize`, test su configurazioni mai viste (scatole/quantità diverse).

### Esperimento minimo e metriche
Condizioni da confrontare: compressione **senza** gate di verifica (trova lookup table / macro fragili) vs compressione **con** gate (trova l'operatore corretto). Anche il *fallimento pulito* della condizione senza gate è un risultato da short paper: isola esattamente il gap.
Metriche: % task completati; numero medio di azioni primitive; lunghezza simbolica del piano; episodi compressi dalla nuova regola; generalizzazione a configurazioni nuove; errori prodotti dalla macro. Il risultato ispezionabile è un punto di forza: si può mostrare letteralmente *quale regola è nata, perché è stata scelta, quanto ha migliorato la pianificazione*.

### Domanda di ricerca
> Può un agente embodied neuro-simbolico, dotato di un world model predittivo, individuare sequenze di azioni ripetitive e altamente prevedibili e trasformarle autonomamente in nuove macro-azioni simboliche, parametriche e generalizzabili?

(Caso generale: come un agente possa creare autonomamente nuovi concetti e abilità per comprimere e rendere più efficiente la propria esperienza.)

---

## 5. Mappa della letteratura

### Filone A — Self-improvement e easy-to-hard/length generalization (neurale)
- **Lee, Cai, Schwarzschild, Lee, Papailiopoulos — Self-Improving Transformers Overcome Easy-to-Hard and Length Generalization Challenges** (arXiv:2502.01612, ICML 2025). Il baseline diretto: loop genera → filtra i corretti → ri-addestra; generalizza da addizione a 10 cifre a 100 cifre; miglioramenti esponenziali OOD filtrando gli esempi auto-generati. Il filtro di correttezza è il punto d'ingresso naturale del verificatore simbolico.
- Learning to Add, Multiply, and Execute Algorithmic Instructions Exactly with Neural Networks (2502.16763).
- Zhou et al., What Algorithms can Transformers Learn? (2310.16028) — congettura RASP-L.
- Extrapolation by Association: Length Generalization Transfer (2506.09251) — transfer tra task.
- Recursive Latent Space Reasoning per OOD (2510.14095); bound sulla training length (2510.27015).
- Messaggio del filone: i transformer imparano scorciatoie, serve self-improvement con verifica o bias strutturali.

### Filone B — Library learning / induzione di astrazioni (simbolico)
- **DreamCoder** (Ellis et al., PLDI 2021) — wake-sleep + compressione per scoprire astrazioni riusabili. Fondazionale.
- **Stitch** (Bowers et al., POPL 2023) — library induction come ottimizzazione MDL greedy.
- Prospective Compression in Human Abstraction Learning (2605.09985, 2026) — library learning **online**, vicino all'agente che si evolve mentre agisce.
- LaSR — Symbolic Regression with a Learned Concept Library (2409.09359).
- Combining Induction and Transduction for Abstract Reasoning (2411.02272, filone ARC).
- LLM-guided compositional program synthesis (2503.15540).
- Ren et al. 2026 — library learning con e-graph su armonia jazz (pattern e-graph + deduzione).

### Filone C — Compressione come valore / skill discovery
- **Skill Reuse as Compression in Agentic RL** (2605.31509, 2026) — il match più diretto: skill discovery come compressione MDL in setting agentico. Related work ricca (codebook di skill, BPE-style merging di Kozma & Voderholzer 2024 — la versione più letterale dell'intuizione, PRISE).
- Learning options via compression (NeurIPS 2022, gruppo Levine).
- Garcia, da Silva, Thomas — compression-inspired macro discovery (1711.09048, 2017).
- Molinaro et al. — Reward function compression facilitates goal-dependent RL (2509.06810) — plausibilità cognitiva, munizione per l'intro.
- **Schmidhuber** — Formal Theory of Creativity, Fun, and Intrinsic Motivation (2010) — compression progress drive, lignaggio teorico.

### Il gap (posizionamento)
Nessuno combina **compressione online come reward intrinseca** con un **gate di verifica simbolica** che promuove l'astrazione candidata a primitiva riusabile solo se certificata corretta e generale. Skill-Reuse-as-Compression resta neurale/statistico; DreamCoder/Stitch sono simbolici ma offline. Il ponte **online + verificato** è lo spazio libero.

---

## 6. Simbolizzazione dentro gli LLM (discussione collaterale, possibile estensione)

Domanda: si può "simbolizzare" *dentro* un LLM? Due direzioni esplorate in letteratura:

1. **Simboli emergenti (mech interp)**: grokking sull'aritmetica modulare (Nanda et al. — il transformer inventa internamente un algoritmo via DFT); Emergent Symbolic Mechanisms (ICML 2025 — symbol abstraction heads → symbolic induction heads → retrieval heads); function/task vectors (Todd et al.). Ma sono quasi-simboli: direzioni continue, superposition, nessuna garanzia composizionale, non nominabili né verificabili.
2. **Simbolizzazione forzata**: (a) bottleneck discreti (VQ-VAE, Gumbel, codebook) — fragili per il reasoning; (b) token nuovi appresi: neologismi (Hewitt et al.), gist tokens (Mu et al.); (c) **simboli esterni** — la via su cui il campo è convergito: **Voyager** (skill library di funzioni riusabili, ambiente come verificatore) e **LILO** (Stitch comprime + LLM nomina e documenta), ReGAL (refactoring in astrazioni).

Conclusione: la simbolizzazione interna genuina (discreta, verificabile, componibile) non è stata ottenuta; l'architettura "il neurale propone, il simbolo vive fuori, la verifica lo promuove" è dove sono atterrati tutti — quindi il design del progetto non è un ripiego.

**Frontiera possibilmente libera** (claim piccolo ma pulito per future work o secondo paper): chiudere il cerchio con l'**internalizzazione** — macro scoperta per compressione → verificata logicamente → distillata dentro il modello come token nuovo (alla neologism) o via fine-tuning sul curriculum auto-generato (loop di Lee et al.). Simbolo nei pesi *con pedigree* (garantito dal verificatore esterno). Da verificare che nessuno l'abbia già pubblicato.

---

## 7. Stato pratico e logistica

- **Account OpenReview creato** con email istituzionale UniFi (dominio edu.unifi.it) → attivazione automatica, niente moderazione da 2 settimane (che colpisce i domini pubblici; le conference non fanno eccezioni per account creati < 2 settimane prima della deadline).
- Profilo OpenReview — impostazione decisa: posizione corrente principale = **Engineer @ Olivetti/TIM** (end year vuoto); **Laurea Magistrale come titolo concluso** (end year compilato); per UniFi: testo libero "Non-degree graduate student" (i corsi singoli non sono un corso di laurea; "MS student" è l'approssimazione accettabile se serve un'etichetta standard; "Intern" e "Undergrad student" sono sbagliati). In alternativa: nessuna voce UniFi, solo email confermata.
- Research areas of interest (in inglese, specifiche, 5-7): neuro-symbolic AI; knowledge representation and reasoning; answer set programming; inductive logic programming; program synthesis / library learning; mechanistic interpretability; opzionali: hierarchical RL / skill discovery, graph neural networks, spatio-temporal data / intelligent transportation systems.
- Completare profilo con homepage/GitHub, Scholar, DBLP se disponibili.
- Status studente su OpenReview irrilevante per la submission; per la tariffa student alla registrazione NeurIPS serve proof of enrollment (i corsi singoli potrebbero non bastare).

## 8. Prossimi passi aperti

1. Verificare lo stato attuale di **Popper sulla predicate invention** per scegliere tra "ILP con invention" e "compressione propone + ILASP raffina".
2. Abbozzare lo **scheletro sperimentale minimo** (setup, cosa loggare, condizioni con/senza gate).
3. Lettura prioritaria: Lee et al. 2502.01612 (loop di curriculum), Skill Reuse as Compression 2605.31509 (taglio embodied), DreamCoder.
4. Eventuale ricerca 2025-2026 sull'internalizzazione (neologismi, gist/skill token, distillazione di tool nei pesi) per verificare che l'anello "scoperta → verifica → internalizzazione" sia libero.
