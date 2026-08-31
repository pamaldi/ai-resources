# Bibliografia ragionata — CoT drift e interpretabilità meccanicistica su EDOS + HateXplain

**Nota preliminare.** Ho verificato direttamente solo le voci contrassegnate con ✔ (repo, ricerca web o download effettivo durante questa sessione). Tutte le altre provengono dalla mia conoscenza e vanno **controllate su ACL Anthology, arXiv o Semantic Scholar prima di finire in un paper**: nomi degli autori, anno, venue e numero arXiv sono esattamente le cose che si degradano. Le voci con ⚠ sono quelle su cui ho meno confidenza e che verificherei per prime.

---

## 1. Dataset e shared task

- ✔ Kirk, H. R., Yin, W., Vidgen, B., Röttger, P. (2023). *SemEval-2023 Task 10: Explainable Detection of Online Sexism*. SemEval-2023. arXiv:2303.04222.
  Paper di riferimento per EDOS. Contiene la tassonomia a 11 vettori e la confusion matrix aggregata dei top-10 sistemi: è il tuo baseline per dire quali confusioni sono *strutturali del task* e non del tuo modello.

- ✔ Repository EDOS: `github.com/rewire-online/edos` (CC0-1.0).
  Il file `data/edos_labelled_individual_annotations.csv` contiene 60.000 annotazioni (20.000 item × 3 annotatori, 19 annotatori distinti). È la base per la variabile di disaccordo. Verificato: 22,2% di disaccordo sulla binaria, 33,4% sulla categoria tra gli item sessisti. La cartella `guidelines/` contiene le linee guida di annotazione originali — indispensabili per l'ablation sulle definizioni nel prompt.

- Mathew, B., Saha, P., Yimam, S. M., Biemann, C., Goyal, P., Mukherjee, A. (2021). *HateXplain: A Benchmark Dataset for Explainable Hate Speech Detection*. AAAI 2021. arXiv:2012.10289.
  Il dataset con rationale a livello di token. Leggi con attenzione la sezione sulle metriche di plausibility e faithfulness: definisce il protocollo che riuserai per confrontare attribuzioni del modello e rationale umani.

- ✔ Plaza, L., Carrillo-de-Albornoz, J., Arcos, I., Rosso, P., Spina, D., Amigó, E., Gonzalo, J., Morante, R. (2025). *Overview of EXIST 2025: Learning with Disagreement for Sexism Identification and Characterization in Tweets, Memes, and TikTok Videos*. CLEF 2025, CEUR Vol-4038.
  Citalo anche se non usi i dati: giustifica la scelta del paradigma LWD e ti dà il riferimento per la metrica ICM-soft.

- Leonardelli, E., Abercrombie, G., Almanea, D., Basile, V., Fornaciari, T., Plank, B., Rieser, V., Uma, A., Poesio, M. (2023). *SemEval-2023 Task 11: Learning With Disagreements (LeWiDi)*. SemEval-2023. ⚠ verifica la lista autori.
  Il benchmark costruito apposta per il disaccordo. Utile come dataset di replica su dominio adiacente se vuoi un terzo punto dati.

- Kennedy, C. J., Bacon, G., Sahn, A., von Vacano, C. (2020). *Constructing interval variables via faceted Rasch measurement and multitask deep learning: a hate speech application*. arXiv:2009.10277. ⚠
  Il dataset "Measuring Hate Speech" di UC Berkeley D-Lab, con annotatori identificati e punteggio continuo. Alternativa se ti serve più potenza statistica sulla variabile di disaccordo.

- Samory, M., Sen, I., Kohne, J., Flöck, F., Wagner, C. (2021). *"Call me sexist, but...": Revisiting Sexism Detection Using Psychological Scales and Adversarial Samples*. ICWSM 2021.
  Utile per l'inquadramento concettuale: mostra quanto la definizione operativa di sessismo cambia i risultati. Rilevante per la tua ablation sulle definizioni.

---

## 2. Disaccordo annotatoriale e prospettivismo

Questa sezione fonda la tua ipotesi principale: che il drift si concentri dove gli umani stessi disagreano.

- Plank, B. (2022). *The "Problem" of Human Label Variation: On Ground Truth in Data, Modeling and Evaluation*. EMNLP 2022.
  Il riferimento canonico contro l'assunzione del gold singolo. Da citare in introduzione.

- Uma, A., Fornaciari, T., Hovy, D., Paun, S., Plank, B., Poesio, M. (2021). *Learning from Disagreement: A Survey*. Journal of Artificial Intelligence Research, 72.
  Survey completa. Ti serve per giustificare la scelta della misura di disaccordo (entropia vs soft label vs modelli per-annotatore).

- Davani, A. M., Díaz, M., Prabhakaran, V. (2022). *Dealing with Disagreements: Looking Beyond the Majority Vote in Subjective Annotations*. TACL 10.
  Approccio multi-annotator con teste separate. Rilevante se vuoi modellare gli effetti dei 19 annotatori EDOS invece di collassarli in un'entropia.

- ✔ Risorsa: `github.com/mainlp/awesome-human-label-variation` — lista curata di dataset con etichette **non aggregate**, mantenuta dal gruppo di Plank. È il posto giusto dove cercare un terzo dataset di replica senza fare ricerca bibliografica alla cieca.

- Aroyo, L., Welty, C. (2015). *Truth Is a Lie: Crowd Truth and the Seven Myths of Human Annotation*. AI Magazine, 36(1).
  Riferimento storico, buono per una frase in introduzione.

- Basile, V., Fell, M., Fornaciari, T., Hovy, D., Paun, S., Plank, B., Poesio, M., Uma, A. (2021). *We Need to Consider Disagreement in Evaluation*. Workshop on Benchmarking (ACL-IJCNLP). ⚠
  Argomento diretto sul perché il disaccordo va nella metrica, non solo nei dati.

- Sap, M., Swayamdipta, S., Vianna, L., Zhou, X., Choi, Y., Smith, N. A. (2022). *Annotators with Attitudes: How Annotator Beliefs And Identities Bias Toxic Language Detection*. NAACL 2022.
  Mostra che il disaccordo non è rumore ma segnale socialmente strutturato. Argomento chiave se il tuo risultato è "il drift traccia l'ambiguità genuina".

---

## 3. Chain-of-Thought: efficacia e limiti

- Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., Zhou, D. (2022). *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*. NeurIPS 35.

- Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A., Zhou, D. (2023). *Self-Consistency Improves Chain of Thought Reasoning in Language Models*. ICLR 2023. arXiv:2203.11171.
  Leggi la definizione operativa: il voto è su *reasoning path* campionati. Serve a giustificare la riformulazione della tua implementazione attuale.

- ✔ Sprague, Z., Yin, F., Rodriguez, J. D., Jiang, D., Wadhwa, M., Singhal, P., Zhao, X., Ye, X., Mahowald, K., Durrett, G. (2024). *To CoT or not to CoT? Chain-of-thought helps mainly on math and symbolic reasoning*. ICLR 2025. arXiv:2409.12183 — https://arxiv.org/abs/2409.12183
  **La citazione più importante per la tua tesi.** Meta-analisi su oltre 100 paper che mostra guadagni CoT concentrati su matematica e ragionamento simbolico e sostanzialmente nulli altrove. Sostituisce con molto più peso le citazioni traballanti che avevi nel report A2.

- Min, S., Lyu, X., Holtzman, A., **Artetxe, M.**, Lewis, M., Hajishirzi, H., Zettlemoyer, L. (2022). *Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?*. EMNLP 2022, pp. 11048–11064.
  Nel tuo report A2 il quarto autore era scritto "Mikel Arber": correggilo.

- Wang, B., Min, S., Deng, X., Shen, J., Wu, Y., Zettlemoyer, L., Sun, H. (2023). *Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters*. ACL 2023.

- Zhang, W., Deng, Y., Liu, B., Pan, S. J., Bing, L. (2024). *Sentiment Analysis in the Era of Large Language Models: A Reality Check*. Findings of NAACL 2024.

---

## 4. Fedeltà del ragionamento (il cuore concettuale del "drift")

- Turpin, M., Michael, J., Perez, E., Bowman, S. R. (2023). *Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting*. NeurIPS 2023. arXiv:2305.04388.
  Il paper fondativo. Dimostra che bias non menzionati nella catena determinano la risposta finale. È il modello del tuo esperimento "il drift è generato o rivelato".

- Lanham, T., Chen, A., Radhakrishnan, A., Steiner, B., Denison, C., et al. (2023). *Measuring Faithfulness in Chain-of-Thought Reasoning*. Anthropic. arXiv:2307.13702.
  **Il protocollo comportamentale che ti serve**: troncamento della catena, iniezione di errori, parafrasi, filler token. Da implementare come secondo livello di evidenza indipendente dagli interni.

- Arcuschin, I., et al. (2025). *Chain-of-Thought Reasoning In The Wild Is Not Always Faithful*. arXiv:2503.08679. ⚠ recupera la lista autori completa.

- Jacovi, A., Goldberg, Y. (2020). *Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness?*. ACL 2020.
  Distingue plausibilità e fedeltà. **Da leggere prima di scrivere qualunque frase su "perché" il modello fa qualcosa**: metà degli errori concettuali in questi lavori nasce dal confondere le due.

- Bentham, O., Stringham, N., Marasović, A. (2024). *Chain-of-Thought Unfaithfulness as Disguised Accuracy*. ⚠
  Argomenta che molte misure di infedeltà stanno in realtà misurando accuratezza. Critica metodologica che devi anticipare: il tuo drift potrebbe essere confuso con la difficoltà dell'item.

- Chen, Y., et al. (2025). *Reasoning Models Don't Always Say What They Think*. Anthropic. ⚠ verifica.
  Estensione dei risultati di fedeltà ai modelli con reasoning esplicito.

---

## 5. Interpretabilità meccanicistica: fondamenti e tecniche

- Elhage, N., Nanda, N., Olsson, C., et al. (2021). *A Mathematical Framework for Transformer Circuits*. Transformer Circuits Thread.
  Il formalismo del residual stream. Necessario per parlare correttamente di "scrivere una direzione nel residual stream".

- nostalgebraist (2020). *Interpreting GPT: the Logit Lens*. LessWrong.
  Citazione obbligata ma è un blog post: accompagnala sempre con Belrose et al.

- Belrose, N., Furman, Z., Smith, L., Halawi, D., Ostrovsky, I., McKinney, L., Biderman, S., Steinhardt, J. (2023). *Eliciting Latent Predictions from Transformers with the Tuned Lens*. arXiv:2303.08112.
  **Usa questo, non il logit lens grezzo.** Il logit lens è noto per fallire su alcune famiglie di modelli, e la tua traiettoria della label lungo i layer è il grafico centrale del paper: non puoi permetterti che sia un artefatto.

- Meng, K., Bau, D., Andonian, A., Belinkov, Y. (2022). *Locating and Editing Factual Associations in GPT*. NeurIPS 2022. arXiv:2202.05262.
  Causal tracing / activation patching nella sua formulazione originale.

- Wang, K., Variengien, A., Conmy, A., Shlegeris, B., Steinhardt, J. (2023). *Interpretability in the Wild: a Circuit for Indirect Object Identification in GPT-2 Small*. ICLR 2023. arXiv:2211.00593.
  Il template metodologico per un'analisi di circuito completa.

- Zhang, F., Nanda, N. (2024). *Towards Best Practices of Activation Patching in Language Models: Metrics and Methods*. ICLR 2024. arXiv:2309.16042.
  **Leggilo prima di fare il primo patching.** Le scelte di metrica e di corruzione cambiano le conclusioni; questo paper ti evita di dover rifare tutto.

- Conmy, A., Mavor-Parker, A. N., Lynch, A., Heimersheim, S., Garriga-Alonso, A. (2023). *Towards Automated Circuit Discovery for Mechanistic Interpretability*. NeurIPS 2023. arXiv:2304.14997.

- Syed, A., Rager, C., Conmy, A. (2023). *Attribution Patching Outperforms Automated Circuit Discovery*. arXiv:2310.10348. ⚠
  Approssimazione a gradiente del patching: rilevante se il costo computazionale del patching esaustivo diventa proibitivo.

---

## 6. Probing e interventi direzionali

Questo è il ramo che ti dà la validazione causale con il minor rischio di fallimento.

- Alain, G., Bengio, Y. (2016). *Understanding intermediate layers using linear classifier probes*. arXiv:1610.01644.

- Belinkov, Y. (2022). *Probing Classifiers: Promises, Shortcomings, and Advances*. Computational Linguistics, 48(1).
  Le obiezioni standard ai probe (un probe può imparare il task da sé). Devi rispondere a queste obiezioni, ed è il motivo per cui il probe da solo non basta e serve l'intervento causale.

- Marks, S., Tegmark, M. (2023). *The Geometry of Truth: Emergent Linear Structure in LLM Representations of True/False Datasets*. arXiv:2310.06824.
  Difference-in-means come metodo per estrarre direzioni. Semplice, robusto, spesso superiore ai probe addestrati.

- Arditi, A., Obeso, O., Syed, A., Paleka, D., Panickssery, N., Gurnee, W., Nanda, N. (2024). *Refusal in Language Models Is Mediated by a Single Direction*. NeurIPS 2024. arXiv:2406.11717.
  **Il template esatto del tuo esperimento finale**: isolare una direzione, ablarla, mostrare che il comportamento cambia. Se trovi una "direzione di drift" e ne dimostri l'effetto causale sul tasso di flip, la struttura argomentativa è questa.

- Zou, A., Phan, L., Chen, S., et al. (2023). *Representation Engineering: A Top-Down Approach to AI Transparency*. arXiv:2310.01405.
  Reading vector e steering. Approccio complementare, più grezzo ma più veloce da mettere in piedi.

---

## 7. Sparse autoencoder (ramo opzionale, alto rischio)

- Bricken, T., Templeton, A., Batson, J., et al. (2023). *Towards Monosemanticity: Decomposing Language Models With Dictionary Learning*. Transformer Circuits Thread.
- Cunningham, H., Ewart, A., Riggs, L., Huben, R., Sharkey, L. (2023). *Sparse Autoencoders Find Highly Interpretable Features in Language Models*. arXiv:2309.08600.
- Templeton, A., Conerly, T., Marcus, J., et al. (2024). *Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet*. Transformer Circuits Thread.
- Lieberum, T., Rajamanoharan, S., Conmy, A., et al. (2024). *Gemma Scope: Open Sparse Autoencoders Everywhere All At Once on Gemma 2*. arXiv:2408.05147.
  Determina la scelta del modello: se vuoi SAE pre-addestrati senza addestrarne uno tuo, il modello è Gemma-2-2B o 9B.
- He, Z., et al. (2024). *Llama Scope: Extracting Millions of Features from Llama-3.1-8B with Sparse Autoencoders*. arXiv:2410.20526. ⚠

Nota di scoping: questo ramo è il più affascinante e il più probabile candidato a farti perdere due mesi senza risultato. Tienilo come estensione, non come colonna portante.

---

## 8. Intersezione CoT × meccanicistica

Letteratura ancora sottile — è esattamente il motivo per cui il tuo progetto ha spazio.

- ✔ Dutta, S., Singh, J., Chakrabarti, S., Chakraborty, T. (2024). *How to think step-by-step: A mechanistic understanding of chain-of-thought reasoning*. TMLR 2024. arXiv:2402.18312 — https://arxiv.org/abs/2402.18312
  Il lavoro più vicino al tuo. Da leggere per primo per capire cosa è già stato fatto e cosa no.

- Jain, S., Wallace, B. C. (2019). *Attention is not Explanation*. NAACL 2019.
- Wiegreffe, S., Pinter, Y. (2019). *Attention is not not Explanation*. EMNLP 2019.
  **Coppia obbligatoria.** Se misuri la massa di attenzione verso lo span di ragionamento contro lo span di input, un revisore ti citerà Jain & Wallace entro tre righe. Devi già aver risposto: usa l'attenzione come misura descrittiva e affiancala a un intervento causale.

- DeYoung, J., Jain, S., Rajani, N. F., Lehman, E., Xiong, C., Socher, R., Wallace, B. C. (2020). *ERASER: A Benchmark to Evaluate Rationalized NLP Models*. ACL 2020.
  Definisce comprehensiveness e sufficiency. Sono le metriche con cui confronterai attribuzioni del modello e rationale umani di HateXplain.

---

## 9. Metodologia sperimentale e statistica

Sezione breve ma non opzionale, visto il problema di potenza che hai già incontrato con n=300.

- Card, D., Henderson, P., Khandelwal, U., Jia, R., Mahowald, K., Jurafsky, D. (2020). *With Little Power Comes Great Responsibility*. EMNLP 2020.
  Analisi di potenza per esperimenti NLP. Ti dice quanti item ti servono per rilevare la differenza di tasso di drift che ti aspetti.

- Dror, R., Baumer, G., Shlomov, S., Reichart, R. (2018). *The Hitchhiker's Guide to Testing Statistical Significance in Natural Language Processing*. ACL 2018.

- Berg-Kirkpatrick, T., Burkett, D., Klein, D. (2012). *An Empirical Investigation of Statistical Significance in NLP*. EMNLP 2012.
  Bootstrap accoppiato: la procedura corretta per confrontare due metodi sullo stesso test set.

---

## 10. Strumenti

- Nanda, N., Bloom, J. (2022). *TransformerLens*. `github.com/TransformerLensOrg/TransformerLens`.
  Supporto completo per GPT-2, Pythia, Llama, Gemma-2. Verifica il supporto per il modello che scegli **prima** di impegnarti.
- Fiotto-Kaufman, J., et al. (2024). *NNsight and NDIF: Democratizing Access to Foundation Model Internals*. arXiv:2407.14561. ⚠
  Più flessibile di TransformerLens sui modelli HuggingFace arbitrari. Se resti su Qwen2.5-7B, probabilmente è questa la scelta.
- Bloom, J., Chanin, D., et al. *SAELens*. `github.com/jbloomAus/SAELens`.

---

## Ordine di lettura suggerito

Link verificati durante la compilazione, tranne dove indicato.

**1. Fissare il vocabolario** — prima di scrivere qualunque frase su "perché" il modello fa qualcosa.

- ✔ Jacovi & Goldberg (2020), *Towards Faithfully Interpretable NLP Systems*, ACL 2020, pp. 4198–4205
  https://arxiv.org/abs/2004.03685 · https://aclanthology.org/2020.acl-main.386/

**2. Capire cosa significa operativamente "drift"** — le due letture che definiscono il tuo oggetto di studio.

- Turpin, Michael, Perez, Bowman (2023), *Language Models Don't Always Say What They Think*, NeurIPS 2023
  https://arxiv.org/abs/2305.04388
- Lanham et al. (2023), *Measuring Faithfulness in Chain-of-Thought Reasoning*
  https://arxiv.org/abs/2307.13702

**3. Verificare che la premessa comportamentale regga.**

- ✔ Sprague et al. (2024), *To CoT or not to CoT?*, ICLR 2025
  https://arxiv.org/abs/2409.12183 · codice e dati: https://github.com/Zayne-sprague/To-CoT-or-not-to-CoT

**4. Vedere quanto spazio resta all'intersezione CoT × meccanicistica.**

- ✔ Dutta, Singh, Chakrabarti, Chakraborty (2024), *How to think step-by-step*, TMLR
  https://arxiv.org/abs/2402.18312

**5. Progettare gli esperimenti causali prima di scrivere codice.**

- Zhang & Nanda (2024), *Towards Best Practices of Activation Patching in Language Models*, ICLR 2024
  https://arxiv.org/abs/2309.16042
- Arditi et al. (2024), *Refusal in Language Models Is Mediated by a Single Direction*, NeurIPS 2024
  https://arxiv.org/abs/2406.11717

**6. Formalizzare la variabile di disaccordo.**

- ✔ Plank (2022), *The 'Problem' of Human Label Variation*, EMNLP 2022, pp. 10671–10682
  https://arxiv.org/abs/2211.02570 · https://aclanthology.org/2022.emnlp-main.731/
- Uma, Fornaciari, Hovy, Paun, Plank, Poesio (2021), *Learning from Disagreement: A Survey*, JAIR 72
  https://www.jair.org/index.php/jair/article/view/12752 ⚠ non verificato, JAIR è open access ma controlla il numero dell'articolo

**7. Dimensionare il campione prima di lanciare l'inferenza.**

- ✔ Card, Henderson, Khandelwal, Jia, Mahowald, Jurafsky (2020), *With Little Power Comes Great Responsibility*, EMNLP 2020, pp. 9263–9274
  https://arxiv.org/abs/2010.06595 · notebook di analisi di potenza: https://github.com/dallascard/NLP-power-analysis
