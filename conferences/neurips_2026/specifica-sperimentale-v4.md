# Specifica sperimentale v4 — autoconferma performativa nel library learning online

**Progetto NEmo 2026 — 3 agosto 2026**
Titolo di lavoro: *Performatively stable abstractions: when a learned library produces the evidence that confirms it*

> **Stato**: versione da implementare. Le prossime correzioni devono venire dal codice, non da un'altra revisione sulla carta.

---

## 0. Cronologia delle correzioni

| | Problema trovato | Correzione |
|---|---|---|
| **v1 → v2** | `riempi_4 × 3` e 12 inserimenti erano fisicamente identici: la libreria cambiava solo la *scrittura* della traccia. Autoconferma della codifica, obiezione fatale | Vincolo di capacità del carrello: le partizioni diventano fisicamente diverse |
| **v2 → v3** | Lo schema `lotto_n(O,N)` era semanticamente invalido per `N > C`; `β` confondeva retroazione ed esplorazione; il gap era misurato nel vocabolario dell'agente | Schema parametrizza la *dimensione del lotto* `q ≤ C`; separati `λ` e `β`; metrica esterna e test congelato |
| **v3 → v4** | `β` uguale non implica esplorazione uguale; il termine `λ·C_rappr` nell'obiettivo è la preferenza che produce il risultato, messa a mano; "qualità della libreria" è un nome scorretto; l'irreversibilità rende ambigua la parola "performativo" | ε-greedy; **planner a budget** al posto del termine simbolico; rinominata la metrica; **`ΔJ_remove` misurato senza permettere la rimozione** |

---

## 1. La domanda

Un sistema che apprende astrazioni online usa la libreria per pianificare. I piani **eseguiti** generano le tracce da cui apprende al giro successivo:

```
L_t  →  comportamento_t  →  dati_{t+1}  →  L_{t+1}
```

La libreria non si limita a interpretare l'esperienza: **contribuisce a produrla**.

**Domanda**: esiste un regime in cui un'astrazione promossa prematuramente genera l'evidenza che la conferma, impedendo o rallentando la propria correzione?

### 1.1 Le tre cose da non confondere

| Ciclo | Cosa dimostra | Forza |
|---|---|---|
| `dati → libreria` | l'ordine dei dati influenza ciò che si apprende | curriculum bias — noto |
| `libreria → scrittura della traccia → libreria` | la libreria cambia come l'esperienza viene registrata | **tautologico** |
| `libreria → comportamento fisico → dati → libreria` | la libreria cambia cosa il robot fa, e quindi cosa osserva | **autoconferma performativa** — l'obiettivo |

Il terzo richiede che decomposizioni diverse dello stesso ordine producano sequenze primitive e stati diversi.

### 1.2 La formulazione in una riga

> Un vocabolario appreso orienta la ricerca del piano; la ricerca orientata produce comportamento; il comportamento produce le tracce che rendono quel vocabolario conveniente.

---

## 2. Il dominio

### 2.1 Il vincolo

Robot con **carrello di capacità `C`** (default 6). Per portare oggetti alla scatola: caricare al deposito, spostarsi, scaricare.

Un ordine da 11 unità ammette decomposizioni **fisicamente diverse**:

```
6 + 5       →  2 viaggi
4 + 4 + 3   →  3 viaggi
11 × 1      → 11 viaggi
```

Diverse sequenze primitive, diversi stati visitati, diverso costo.

### 2.2 Azioni primitive

```
vai_a(Luogo)          spostamento (deposito ↔ scatola)
carica(Oggetto)       nel carrello; fallisce se pieno
scarica               dal carrello nella scatola
verifica              controllo finale
```

### 2.3 Ordini e piani

Un **ordine** è `(Oggetto, N)`. Un **piano** è una partizione `N = q₁ + … + qₘ` con ogni `qᵢ ≤ C`, ciascun lotto eseguito come:

```
vai_a(deposito), carica × qᵢ, vai_a(scatola), scarica × qᵢ
```

### 2.4 Costo fisico

```
C_fisico(p) = n_viaggi × w_viaggio + n_carichi + n_scarichi
```

con `w_viaggio = 10`. **L'ottimo fisico per `N` usa `⌈N/C⌉` lotti.** Noto per costruzione.

### 2.5 Il chunk è localmente utile, irregolarmente subottimale

Con `C = 6`, un agente che partiziona sempre in lotti da 4:

| N | Partizione con lotti da 4 | Viaggi | Ottimo | Regret |
|---|---|---|---|---|
| 4 | 4 | 1 | 1 | 0 |
| 5 | 4+1 | 2 | 1 | **1** |
| 6 | 4+2 | 2 | 1 | **1** |
| 7 | 4+3 | 2 | 2 | 0 |
| 8 | 4+4 | 2 | 2 | 0 |
| 9 | 4+4+1 | 3 | 2 | **1** |
| 11 | 4+4+3 | 3 | 2 | **1** |
| 12 | 4+4+4 | 3 | 2 | **1** |

> Il chunk non è cattivo: è **ottimo su alcuni conteggi (4, 7, 8) e subottimo su altri in modo irregolare**. È precisamente per questo che sopravvive — l'agente non riceve mai un segnale netto e consistente che sia sbagliato.

Questa struttura del regret in funzione di `N` è un dato da riportare, non un dettaglio.

---

## 3. Lo schema target

Il parametro da scoprire è la **dimensione del lotto**, non il totale dell'ordine:

```
trasporta_lotto(Oggetto, q)      vincolo: 1 ≤ q ≤ C
```

Il livello dell'ordine resta la partizione, scelta dal planner.

| | Struttura | Viaggi per N=11 |
|---|---|---|
| **Schema** | `trasporta_lotto(O,6) ; trasporta_lotto(O,5)` | 2 |
| **Chunk prematuro** | `lotto_4(O) ; lotto_4(O) ; [3 primitive]` | 3 |

`lotto_4(O)` è `trasporta_lotto(O,4)` con il secondo argomento incorporato: la differenza chunk/schema è la variabile al posto della costante.

### 3.1 L'asimmetria di invocazione

Invocare `lotto_4(O)` costa meno bit che invocare `trasporta_lotto(O,4)`: il chunk specializzato **non deve trasmettere l'argomento**.

Conseguenza: anche dopo la promozione dello schema, la ricerca guidata dalla libreria può continuare a raggiungere prima i piani basati sul chunk. È il meccanismo che rende plausibile la diagnosi *planner non-use* (§7.3), e va misurato.

---

## 4. Il flusso di ordini esterni

**Identico tra le condizioni sperimentali.** Vincolo che rende valido il confronto, verificato per hash.

```
seq_len    ordini nella vita dell'agente      default 500
N_range    intervallo dei conteggi            default [2, 12]
C          capacità del carrello              default 6
objects    oggetti distinti                   default 5
schedule   evoluzione della distribuzione
k          lunghezza della fase povera        default 100
```

| Schedule | Descrizione |
|---|---|
| `poor_then_rich` | primi `k` ordini con `N=4`; poi `N` uniforme su [2,12] |
| `rich` | `N` uniforme su [2,12] dall'inizio |
| `poor_forever` | `N=4` sempre |
| `slow_drift` | `N` concentrato su 4, varianza crescente |

**Gli oggetti variano sempre**: il sistema ha una dimensione lungo cui astrarre correttamente fin dall'inizio, così il fallimento riguarda specificamente `q`.

---

## 5. Il sistema

### 5.1 DSL

```
primitive:  vai_a, carica, scarica, verifica
costrutti:  seq(a,b), repeat(n,a) con n costante o variabile, lambda/var
```

> **Da dichiarare nel paper**: il progettista fornisce la capacità di parametrizzare. Il fenomeno studiato è che il sistema, potendo farlo, in certi regimi non lo fa.

### 5.2 Costo MDL

```
J(H,D) = L(H) + L(D|H)
L(H)   = Σ_macro nodi(macro) × log₂(|V|)
L(D|H) = Σ_tracce lunghezza codificata nel vocabolario corrente
```

Il vocabolario cresce a ogni promozione, quindi ogni macro nuova ha un costo che si ripercuote su tutta la libreria.

### 5.3 Proposta e promozione

Ogni `promotion_interval` episodi (default 25):

1. **Anti-unificazione** del primo ordine sulle sottosequenze ricorrenti → candidati con nome fresco
2. **Candidato strutturale**: se la libreria contiene ≥ 2 macro che differiscono solo per il numero di applicazioni dello stesso operatore, proponi la versione con `repeat(q, …)`. *Bias esplicito, dichiarato*
3. **Valutazione**: `ΔJ` sull'intero buffer
4. **Verifica**: esecuzione su configurazioni holdout, confronto con l'espansione primitiva
5. **Promozione**: `ΔJ < 0` e verifica superata → in libreria

Promozioni **irreversibili** nella condizione principale (condizione sperimentale, non tesi; controllo in §10).

---

## 6. Il planner — la correzione centrale della v4

### 6.1 Perché non un termine simbolico nell'obiettivo

Nella v3 il planner minimizzava `C_fisico(p) + λ·C_rappr(p|L)`. Obiezione decisiva: **perché un robot dovrebbe accettare un viaggio in più solo perché il piano è più corto da scrivere?** Quel termine è la preferenza necessaria a produrre il risultato, inserita a mano nell'obiettivo.

### 6.2 La formulazione adottata: ricerca sotto budget

Il planner **minimizza il solo costo fisico**. Nessun termine simbolico nell'obiettivo.

```
budget B          numero massimo di nodi espandibili
ordine di ricerca guidato dalla libreria: i piani esprimibili con
                  poche invocazioni della libreria corrente sono
                  raggiunti prima
output            il miglior piano FISICO trovato entro B
```

La libreria non cambia *cosa l'agente preferisce*. Cambia **cosa l'agente trova in tempo**.

Il ciclo diventa:

```
L_t → ordine di ricerca → piano trovato entro budget → traccia fisica → L_{t+1}
```

Il parametro di retroazione è `B`:

- `B` grande → la ricerca è quasi esaustiva, la libreria non influenza l'esito → **nessun ciclo**
- `B` piccolo → l'esito dipende fortemente dall'ordine di esplorazione, quindi dalla libreria → **ciclo pieno**

> Vantaggio decisivo: `B` è un vincolo di risorse, non una preferenza. Nessuno può dire che hai messo nell'obiettivo la conclusione. E il legame con il long-horizon planning è diretto: la pianificazione gerarchica esiste **proprio perché** la ricerca è limitata.

### 6.3 Esplorazione: ε-greedy

`β` è stato rimosso. La policy è:

```
con probabilità 1−ε   → il piano trovato dal planner
con probabilità ε     → una partizione ammissibile scelta a caso
```

`ε` è **identico in tutte le condizioni** (default 0.1). L'esplorazione esplicita è quindi realmente uguale, cosa che con la softmax non era vera: `λ` concentrava la distribuzione e riduceva l'entropia effettiva.

**Da loggare comunque**: entropia delle partizioni scelte, numero di dimensioni di lotto distinte esplorate. La riduzione di esplorazione *effettiva* è parte del meccanismo performativo e va misurata, non nascosta.

### 6.4 Variante di controllo: prior della libreria

Come robustezza, una formulazione alternativa della retroazione:

```
P(p | ordine, L) ∝ exp(−β·C_fisico(p)) · P_L(p)^λ
```

dove `P_L(p)` è il prior indotto dalla libreria. Non afferma che i bit siano un costo fisico: descrive un agente bounded-rational influenzato dal proprio vocabolario.

**Serve a mostrare che il fenomeno non dipende dal particolare meccanismo di retroazione scelto.** Se compare sia con il budget sia con il prior, è robusto.

---

## 7. Condizioni sperimentali

### 7.1 Griglia principale

```
B        ∈ {∞, 500, 200, 100, 50, 20, 10}     7 valori
ε        fisso (default 0.1)
schedule ∈ {poor_then_rich, rich, poor_forever, slow_drift}
k        ∈ {50, 100, 200}                      solo poor_then_rich
semi     10 per cella
```

**Vincolo assoluto**: a parità di `schedule`, `k` e seme, la sequenza di ordini esterni è identica in ogni cella.

**Ablazioni**: `ε ∈ {0.05, 0.1, 0.2}`; variante prior (§6.4).

### 7.2 Le tre condizioni diagnostiche

| | B | ε | schedule | Esito atteso |
|---|---|---|---|---|
| **A** — nessuna retroazione | ∞ | 0.1 | poor_then_rich | scopre lo schema dopo la varietà |
| **B** — retroazione forte | 20 | 0.1 | poor_then_rich | **bloccato** |
| **C** — esperienza ricca | 20 | 0.1 | rich | scopre lo schema |

**A vs B**: isola la retroazione a esperienza esterna ed esplorazione esplicita identiche.
**B vs C**: isola la povertà iniziale a retroazione ed esplorazione identiche.

Se entrambe le differenze sono nette:

> **La retroazione non causa il blocco. Lo rende irreversibile quando l'esperienza iniziale è povera.**

### 7.3 La diagnosi a quattro vie

Il blocco può avere meccanismi distinti, e separarli è probabilmente il contributo più originale.

| Meccanismo | Descrizione |
|---|---|
| **Evidence starvation** | il comportamento poco vario non genera mai gli esempi che innescherebbero il candidato → **lo schema non viene mai proposto** |
| **MDL rejection** | lo schema viene proposto, ma sui dati autoindotti `ΔJ` non è favorevole → **non promosso** |
| **Planner non-use** | lo schema viene promosso ma la ricerca sotto budget raggiunge prima i piani basati sul chunk (§3.1) → **promosso e inutilizzato** |
| **Persistenza meccanica** | il chunk resta solo perché la rimozione è vietata, non perché sia ancora conveniente → **non è autoconferma** |

**Condizione `oracle_proposal`**: a ogni intervallo, `trasporta_lotto(O,q)` è reso disponibile come candidato indipendentemente da cosa il proponente avrebbe generato. Valutazione e verifica invariate.

| Osservazione con oracolo | Meccanismo |
|---|---|
| Promosso e usato | il blocco era nella **generazione dei candidati** |
| Rifiutato da `ΔJ` | il blocco è nella **valutazione MDL sui dati indotti** |
| Promosso ma non usato | il blocco è nel **planner** |

### 7.4 `ΔJ_remove` — la misura che rende difendibile la parola "performativo"

**Correzione critica.** Se `lotto_4` non può essere rimosso, la sua permanenza non dimostra nulla: potrebbe restare solo perché la rimozione è vietata.

A ogni intervallo di promozione, calcolare — **senza permettere la rimozione**:

```
ΔJ_remove(lotto_4) = J(L \ {lotto_4}, D_buffer) − J(L, D_buffer)
```

| Osservazione | Interpretazione |
|---|---|
| `ΔJ_remove > 0` — rimuoverlo peggiorerebbe | **autoconferma vera**: è ancora MDL-favorevole sui dati che ha indotto |
| `ΔJ_remove < 0` — MDL vorrebbe rimuoverlo | **semplice irreversibilità**: la persistenza è meccanica |
| Schema presente ma chunk dominante nell'uso | **planner non-use** |

Senza questa misura, "performativamente stabile" sarebbe un'etichetta su un fatto meccanico.

---

## 8. Protocollo di valutazione — congelato

```
TRAINING                        TEST
B variabile (la condizione)     B_eval fisso, uguale per tutti, FINITO
ε come da condizione            ε_eval = 0 (deterministico)
libreria aggiornata             libreria congelata
ordini dallo schedule           test set fissato in anticipo
```

> `B_eval` deve essere **finito**. Con ricerca illimitata anche l'agente con `lotto_4` trova `6+5`, e il gap collassa a zero per tutti: si misurerebbe solo che tutte le librerie contengono le primitive.

### 8.1 Due misure distinte

**(a) Generalità rappresentazionale** — proprietà della libreria in sé:
- presenza dello schema parametrico
- copertura dei valori di `q` rappresentati
- lunghezza MDL su un **corpus esterno bilanciato**, indipendente da ciò che l'agente ha generato

**(b) Prestazione operativa del sistema libreria–planner** — con planner, `B_eval` e test set identici per tutti:
- costo fisico totale
- numero di viaggi (la misura più leggibile)
- regret su `N` mai osservati
- transfer fuori dominio: `N ∈ [13,30]`
- struttura del regret in funzione di `N`

> **Nome corretto**: non "qualità della libreria". Una libreria contiene sempre le primitive e non è intrinsecamente incapace di produrre il piano ottimo — lo diventa **quando usata da un planner a risorse limitate**. La metrica riguarda il sistema, non la libreria isolata.

### 8.2 Costo di vita

Terza quantità, distinta dalle due sopra: **costo fisico totale sostenuto durante l'apprendimento**. Cosa l'agente ha realmente speso.

Può divergere dalla prestazione finale: un agente può spendere poco durante la vita (usa sempre la macro che trova subito) e finire con un sistema pessimo.

---

## 9. Altre metriche

**Esito dell'apprendimento**
- `reached_schema`, `time_to_schema` (∞ se mai), composizione della libreria

**Tempo di recupero** — distingue *rallenta* da *impedisce*
Episodi dopo `k` prima della promozione dello schema. Riportare la **distribuzione sui semi**, plausibilmente bimodale.

**Comportamento fisico** — la prova diretta della performatività
- istogramma delle **dimensioni di lotto scelte**, per condizione
- viaggi medi per ordine
- entropia delle partizioni scelte (§6.3)

Stessi ordini esterni, comportamento fisico diverso: la figura che rende il fenomeno non contestabile.

**Dinamica della libreria**
- `|libreria|` e `L(H)` nel tempo
- `ΔJ_remove` del chunk nel tempo
- frequenza di attivazione del candidato strutturale

---

## 10. Controlli

- [ ] **Ordini identici verificati** per hash tra condizioni. Se differiscono, l'esperimento è invalido
- [ ] **Condizione `oracle_proposal`** (§7.3)
- [ ] **`ΔJ_remove`** loggato a ogni intervallo (§7.4)
- [ ] **Controllo di reversibilità**: promozioni revocabili
- [ ] **Variante prior** (§6.4): il fenomeno non deve dipendere dal meccanismo di retroazione
- [ ] **Ablazione su ε**: {0.05, 0.1, 0.2}
- [ ] **Ablazione del candidato strutturale**: senza il bias di §5.3.2, qualcuno arriva allo schema?
- [ ] **Sensibilità a `C`**: {4, 6, 8}
- [ ] **Sensibilità al `promotion_interval`**: {10, 25, 50}
- [ ] **Sensibilità alla codifica di `L(H)`**: due schemi alternativi
- [ ] **Semi**: 10 per cella, riportare varianza

---

## 11. Figure

**F1 — Diagramma di fase.** `B` (crescente verso sinistra = più retroazione) sull'asse x, `k` sull'asse y, colore = probabilità di raggiungere lo schema.

**F2 — Comportamento fisico.** Istogramma delle dimensioni di lotto in A e B, stessi ordini esterni.

**F3 — Prestazione operativa.** Costo fisico sul test set congelato in funzione di `B`, curve per schedule.

**F4 — Diagnosi.** Distribuzione delle run bloccate tra starvation / rejection / non-use / persistenza meccanica.

**F5 — `ΔJ_remove` nel tempo.** Mostra se il chunk resta conveniente sui dati indotti.

---

## 12. Posizionamento

| Precedente | Relazione |
|---|---|
| **Performative prediction** (Perdomo et al. 2020) | stesso fenomeno; parametri continui, punti fissi ben definiti. Qui: **simboli discreti con dipendenze** |
| **Primacy bias** (Nikishin et al. 2022) | commitment prematuro nei pesi; cura = reset periodici |
| **Loss of plasticity** (Dohare, Sutton) | meccanismo analogo: soluzioni a rango basso che restringono lo spazio successivo. Qui il restringimento è **nel vocabolario**, dicibile e ispezionabile |
| **Ciclo ROD** (Machado 2019) | formalizza rappresentazione → option → rappresentazione come ciclo **virtuoso**. Nessuno ha chiesto quando è vizioso |
| **Certificati anytime-valid** (2607.00871) | nota che il passo MDL di Stitch è one-shot e che DreamCoder non ha garanzie di convergenza. Cura senza caratterizzazione |
| **Bounded/resource-rational planning** | il planner a budget è nella loro tradizione; qui il budget interagisce con un vocabolario che evolve |

**Il claim:**

> Il ciclo rappresentazione → astrazione → rappresentazione è stato formalizzato e assunto virtuoso. Mostriamo che quando la ricerca del piano è limitata da risorse — la ragione stessa per cui esiste la pianificazione gerarchica — il vocabolario appreso orienta la ricerca, la ricerca orientata produce comportamento, e il comportamento produce le tracce che confermano il vocabolario. Caratterizziamo il regime, distinguiamo quattro meccanismi di blocco, e osserviamo che le tecniche di reset dei parametri non si trasferiscono direttamente a commitment simbolici con macro dipendenti.

**Da NON dire**: "nessuno ha guardato questo fenomeno"; "reset e pruning non sono applicabili ai simboli"; "A e B hanno esplorazione identica" (hanno la stessa esplorazione *esplicita*).

---

## 13. Aggancio al workshop

Tema (a) *long-horizon planning*: apprendimento e revisione di modelli d'azione simbolici.

Motivo conduttore *affidabilità*: un'astrazione performativamente stabile è un modello d'azione che l'agente **continua a confermare perché ha smesso di generare l'esperienza che lo smentirebbe**. La verifica non lo intercetta: la macro è corretta su tutto ciò che l'agente esegue. È un fallimento invisibile ai criteri di correttezza esistenti.

---

## 14. Esiti possibili

| Esito | Pubblicabile? |
|---|---|
| Transizione netta in `B` | sì, risultato pieno |
| Degradazione graduale della prestazione operativa | sì, più debole |
| Blocco con meccanismo identificato dalla diagnosi a quattro vie | sì, forse il migliore |
| Solo persistenza meccanica, `ΔJ_remove < 0` | **no**: non è performatività, è irreversibilità |
| Nessun blocco | negativo onesto, non automaticamente sufficiente |
| Blocco anche con `B = ∞` | è curriculum bias: l'esperimento ha detto di no |

---

## 15. Implementazione

| Componente | Righe | Giorni |
|---|---|---|
| Dominio con carrello, ordini, schedule | 120 | 1,5 |
| DSL, costo MDL, `ΔJ_remove` | 140 | 1,5 |
| Planner a budget con ordine di ricerca guidato | 150 | 2 |
| Proposta, anti-unificazione, verifica, oracle | 170 | 2 |
| Loop online, protocollo di test, logging | 120 | 1,5 |
| Griglia, analisi, figure | 150 | 2 |

**~850 righe, 10-11 giorni.** Con margine: due settimane.

### Ordine di costruzione, con i gate

**1. Dominio e planner fisico esaustivo** — verificare che l'ottimo sia `⌈N/C⌉` lotti.

**2. GATE OFFLINE.** MDL e promozione su corpus fisso e ricco, senza loop. **Il sistema arriva a `trasporta_lotto(O,q)`?**
> Se non ci arriva in condizioni ideali, il problema è nel DSL o nel costo, non nel fenomeno. Fermarsi e risolvere. **Due giorni.**

**3. Loop online con `B = ∞`** — deve riprodurre il comportamento offline.

**4. Introdurre il budget** — è qui che si scopre se il fenomeno esiste.

**5. GATE DEL PILOT.** Con `B` piccolo e schedule povero: si blocca? Con quale meccanismo? `ΔJ_remove` è positivo?
> Se non si blocca, o se `ΔJ_remove < 0`, non c'è paper in questa forma. Meglio saperlo al giorno cinque.

**6. Griglia, oracle, ablazioni.**

---

## 16. Prima cosa da fare

Passi 1 e 2. Due giorni.

**Se `trasporta_lotto(O,q)` emerge offline su corpus ricco, l'esperimento ha una base. Altrimenti si torna alla funzione di costo prima di scrivere altro.**

> **Nota sul processo.** Questa è la quarta versione, e ogni round ha trovato correzioni reali. Ma le specifiche non convergono da sole: il prossimo errore importante emergerà dal gate offline, non da un'altra revisione astratta. Da qui in avanti le modifiche vanno guidate da cosa fa il sistema.
