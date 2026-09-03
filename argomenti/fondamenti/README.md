# Fondamenti

**La domanda.** Il vocabolario che gli altri cinque argomenti usano senza definirlo: complessità, decisione, valore, campionamento.

**Stato.** attivo, ma è l'argomento più disomogeneo dell'archivio · ultima revisione: 3 settembre 2026

---

## Cosa c'è qui

| Documento | Cos'è |
|---|---|
| [riassunto-p-np.md](riassunto-p-np.md) | P e NP, macchine di Turing non deterministiche, la tesi di Cobham come assunzione e non teorema |
| [stanford-ai-mdp.md](stanford-ai-mdp.md) | appunti Stanford: MDP, funzione di valore di stato *V* e di azione *Q* |
| [watermarking-llm-sampling.md](watermarking-llm-sampling.md) | dal campionamento dei token al watermarking: softmax, temperatura, top-p, seed, il tournament sampling di SynthID |
| [risorse-cs.md](risorse-cs.md) | risorse di informatica raccolte dal triage |
| [pdf/](pdf/) | il testo divulgativo su P e NP |

## Agganci

- [Autonomous and Adaptive Systems](../../formazione/autonomous-adaptive-systems/) — **il seguito naturale di [stanford-ai-mdp.md](stanford-ai-mdp.md)**: dalla definizione di *V* e *Q* agli algoritmi che le stimano (bandit, Monte Carlo, differenze temporali, approssimazione di valore, policy gradient), con le slide pubbliche
- [Reasoning](../reasoning/) — il nucleo F poggia sui limiti formali di questa cartella
- [Interpretability](../interpretability/) — [watermarking-llm-sampling.md](watermarking-llm-sampling.md) comincia dove finisce l'analisi del residual stream

## Aperto

- **Questo argomento è una raccolta, non una domanda.** Complessità computazionale, decisione sequenziale e campionamento stanno insieme perché servono agli altri, non perché condividano un problema. Va bene finché resta piccolo; se cresce, va spezzato.
- Manca del tutto l'**astrazione dell'azione** — option, hierarchical RL, skill discovery. Non la copre nemmeno il corso AAS. Il posto dove cercarla è [scoperta-di-astrazioni-letteratura.md](../compressione-astrazione/scoperta-di-astrazioni-letteratura.md).
