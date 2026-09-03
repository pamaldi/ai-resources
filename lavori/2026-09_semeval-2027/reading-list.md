# Reading list — SemEval 2027: DiCo-NLI (ex CoCo-NLI) vs AgentRisk

Riferimento: valutazione candidati per SemEval 2027, in continuità con la pipeline neuro-simbolica NS-EDL usata per il Task 11 (2026, 96,34% accuratezza, TCE ~1.02).

Approfondimento operativo: [Task 2 — DiCo-NLI: repository, organizzatori e paper](task-2-dico-nli-organizzatori.md).

> **Superata in parte.** Questa lista confronta due task. La [valutazione del 3 settembre 2026](valutazione-task.md) ne copre **sette** con lo stesso criterio, corregge il calendario e ribalta il quadro: Task 2 (DiCo-NLI) resta primaria, entra Task 11 (VAKRA cap. 4) come seconda opzione opportunistica, AgentRisk resta aperta. Quel documento è ora il riferimento del progetto; questo resta per il dettaglio bibliografico su DiCo-NLI e AgentRisk.

Criterio guida: formale/strutturato vs vago nelle specifiche di task, da verificare sui dati reali (sample data dall'8 agosto 2026, training data dall'8 settembre 2026) e non solo sulle descrizioni.

---

## DiCo-NLI (nome precedente: CoCo-NLI)

La pagina centrale SemEval conserva il nome CoCo-NLI; il repository e la proposta revisionata degli organizzatori usano DiCo-NLI, con focus più preciso sulla consistenza direzionale delle predizioni NLI.

Organizzatori: Apaolaza Larraya, Soroa, Agerri, Lopez-Gazpio — gruppo HiTZ.

Il segnale più forte: uno degli organizzatori ha già pubblicato quello che è con ogni probabilità il seme diretto della task.

1. **Apaolaza, Altuna, Soroa, Lopez-Gazpio — "Assessing Logical Coherence of LLMs via Fine-Grained NLI" (2026)**
   Pubblicazione HiTZ. Praticamente il paper-progenitore della task. Da leggere per primo: mostra come il gruppo operazionalizza "coerenza logica" e "fine-grained NLI" — risponde già in parte alla domanda su quanto la composizionalità sia sfruttabile logicamente.

2. **Apaolaza et al. — "Exploring the dilemma of causal incoherence: A study on the approaches and limitations of large language models in natural language inference"** (Procesamiento del Lenguaje Natural 74, 2025)
   Lavoro precedente dello stesso autore, stessa linea (incoerenza causale in NLI). Utile per capire dove gli LLM falliscono tipicamente — spesso il punto d'attacco naturale per un validatore simbolico.

3. **Fu & Frank — "Exploring Continual Learning of Compositional Generalization in NLI"** (TACL 2024)
   Introduce la C2Gen NLI challenge, dove un modello acquisisce conoscenza di inferenze primitive come base per inferenze composizionali. Non è degli organizzatori della task ma è il riferimento teorico più diretto sul concetto di composizionalità in NLI.

4. **Sfondo generale sul metodo:** letteratura NLI4CT (SemEval 2023 Task 7 / SemEval 2024 Task 2)
   Non per il dominio clinico, ma per come altri team hanno strutturato validatori/regole sopra a un layer NLI — schema pipeline molto simile a quello che useresti tu.

---

## AgentRisk

Organizzatori: Menis Mastromichalakis, Zerva, Martins et al.

Provenienza mista degli organizzatori: Zerva e Martins lavorano insieme su quality estimation e conformal prediction (WMT Shared Task on Quality Estimation), mentre Menis-Mastromichalakis è associato a lavori di knowledge graph e AI neuro-simbolica (NCSR Demokritos). Questo mix rende plausibile che la task abbia una componente formale/strutturata nelle policy — buon segno per il pattern NS-EDL — ma anche una componente di stima di confidenza calibrata, non solo classificazione secca.

Benchmark chiave sul rischio agentico multi-turn:

1. **AgentHarm** (Andriushchenko et al., 2024)
   Standard de facto per "safety in agentic multi-step": 110 task malevoli (440 con augmentation) su 11 categorie di harm, ciascuno richiede esecuzione multi-step. Da leggere per primo.

2. **ToolEmu** (Ruan et al., 2023)
   Sandbox LLM-emulato per identificare failure ad alto rischio su toolkit diversi. Interessante perché il "sandbox emulato" è concettualmente vicino a un ambiente dove inserire un verificatore deterministico.

3. **Agent-SafetyBench** (Zhang et al., 2024)
   Tassonomia di rischio su tool use multi-step. Utile per capire come si costruiscono tassonomie di rischio strutturate — se AgentRisk 2027 usa un approccio simile, è già mezzo formalizzato.

4. **R-Judge**
   Benchmark per valutare la capacità degli LLM di giudicare/identificare rischi di sicurezza dati i record di interazione di un agente (569 record multi-turn). Il framing "giudicare se un comportamento viola una policy" è molto vicino a quello che probabilmente servirà per AgentRisk.

5. **MT-AgentRisk** (Li et al., 2026)
   Citato in letteratura come lavoro che mostra come i rischi si compongano su orizzonti multi-turn. Nome quasi identico alla task SemEval — da controllare se c'è overlap diretto con gli organizzatori o se è convergenza terminologica nel campo.

6. **AgentDojo / InjecAgent**
   Per la parte di prompt injection e ambienti dinamici, nel caso la task includa anche input adversarial oltre a policy compliance "pulita".

---

## Nota pratica

Dato il pattern Zerva/Martins (quality estimation, conformal prediction), non è da escludere che AgentRisk richieda anche calibrazione dell'incertezza sul giudizio di rischio, non solo classificazione binaria. Da tenere a mente quando arrivano i sample data: cambierebbe la forma del validatore (non solo valido/non valido, ma con che confidenza).
