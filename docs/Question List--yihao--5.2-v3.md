---
marp: true
---

# Robust Speaker Diarization for Multi-Speaker Meetings

## Thesis Abstract
Speaker diarization—the task of determining “who spoke when”—is a fundamental front-end for intelligent meeting understanding systems. However, its performance degrades in real-world multi-speaker scenarios characterized by high speaker density, frequent overlap, far-field acoustics, and heterogeneous noise conditions. A limitation of current research is that existing public benchmarks predominantly reflect low-density(换一个词) or controlled environments, failing to capture the complex interaction dynamics of real meetings. As a result, they lack the diagnostic resolution required to explain why modern diarization systems struggle and when such errors occur. To address this gap, this thesis proposes a benchmark-driven optimization framework that tightly couples benchmark construction, diagnostic evaluation, and system-level optimization.

First, we introduce Multi-Talker-SD, a scenario-driven synthetic benchmark designed to model realistic conversational dynamics and spatial acoustics with fine-grained controllability. The dataset comprises 1,110 bilingual (English–Mandarin) sessions with 10–30 speakers, totaling over 1,200 hours. By explicitly parameterizing overlap ratios, turn-taking behavior, silence patterns, and spatial configurations, the benchmark provides the precise ground-truth granularity required to isolate algorithmic failure modes that often remain hidden in existing datasets.

Second, leveraging Multi-Talker-SD as a diagnostic instrument, we conduct a evaluation of both clustering-based and end-to-end diarization architectures. The analysis reveals that as speaker density increases, the latent representation space becomes overcrowded, leading to increased speaker confusion and missed speech. Furthermore, we observe significant cross-lingual degradation, highlighting the models’ sensitivity to domain mismatch and their reliance on implicit low-density acoustic priors.

Finally, guided by these diagnostic insights, we propose targeted system-level optimizations to address the identified limitations. For modular pipelines, we introduce an overlap-aware integration of neural speech separation with explicit leakage suppression to reduce speaker confusion. For target-speaker paradigms, we develop TS-VAD+, which incorporates large-scale self-supervised representations and profile enhancement to improve robustness under noisy and unconstrained conditions. Additionally, we propose a density-aware domain adaptation strategy to mitigate the bias of end-to-end models toward low-density scenarios.

Experimental results demonstrate that the proposed framework achieves consistent improvements across challenging conditions, yielding an absolute DER reduction of 3–4% under background noise and reverberation, and reducing zero-shot DER on the DIHARD-III benchmark from 16.28% to 13.11% (The previous numerical values ​​were incorrect.). These findings suggest that diagnostic benchmarks are essential not only for evaluation, but for systematically driving architectural innovation in speaker diarization.

---

**Thesis Format Declaration:** Master's Thesis (~68-73 pages total). 
**Structure:** 2 Contribution Chapters (Chapter 3: Benchmark Construction & Diagnosis; Chapter 4: System Optimization & Evaluation).

## Publications

The materials presented in this thesis are based on the following publications:

**1. "A Benchmark Dataset for Multi-Speaker Meeting Diarization"**
* **Status:** Under review for *Proceedings of the Annual Conference of the International Speech Communication Association (Interspeech)*, 2026.
* **Authorship:** First author
* **Related Chapter:** Chapter 3
* **Core Contribution:** Details the scenario-driven synthetic simulation pipeline, the construction of the Multi-Talker-SD benchmark, and the diagnostic evaluation revealing the scalability limits of existing baseline models.

**2. "TS-VAD+: Modularized Target-Speaker Voice Activity Detection for Robust Speaker Diarization"**
* **Status:** Published in *Asia-Pacific Signal and Information Processing Association Annual Summit and Conference (APSIPA ASC)*, 2025.
* **Authorship:** Third author
* **Related Chapter:** Chapter 4 (Section 4.2)
* **Core Contribution:** Proposes the TS-VAD+ architecture, detailing the integration of large-scale SSL representations (WavLM) and profile enhancement to address E2E scalability challenges.

**3. "Analysis of Clustering-based Speaker Diarization Performance Trade-offs with Speech Separation"**
* **Status:** Under review for *Proceedings of the Annual Conference of the International Speech Communication Association (Interspeech)*, 2026.
* **Authorship:** First author
* **Related Chapter:** Chapter 4 (Section 4.1)
* **Core Contribution:** Analyzes the integration of neural speech separation into clustering pipelines and proposes leakage suppression mechanisms to reduce speaker confusion rates.

---

## Chapter 1: Introduction [5 pages]

**1.1 Background and Motivation [2 pages]**
 *[Proposed Figure: Conceptual diagram of the compounding acoustic and conversational challenges in a multi-speaker meeting environment]*
* How is speaker diarization formally defined, and what role does it play as a front-end for downstream tasks such as ASR and speaker-attributed TTS?
* What are the primary acoustic and conversational complexities associated with multi-speaker meeting scenarios?
* How can scenario-driven synthetic simulation help address the limitations observed in current datasets?

**1.2 Challenges in Meeting Speaker Diarization [1 page]**
* *[Proposed Figure: 2x2 grid overview of the four challenges: far-field, overlap, noise, dynamic count]*
* In what ways do overlapping speech and far-field acoustics impact the performance of modular clustering and E2E architectures?

**1.3 Thesis Objectives and Contributions [1.5 pages]**
* *[Proposed Figure: Benchmark → Diagnosis → Optimization contribution flow block diagram]*
* What are the three core contributions of this thesis (Benchmark, Diagnosis, Optimization), and how do they interconnect?
* **Contribution 1:** How does the constructed Multi-Talker-SD benchmark provide the diagnostic granularity needed to analyze algorithmic failure modes?
* **Contribution 2:** What scalability bottlenecks are revealed through the systematic diagnostic evaluation of baseline models?
* **Contribution 3:** How do the proposed system-level optimizations (Speech Separation, TS-VAD+, and Domain Adaptation) address these identified vulnerabilities?

**1.4 Thesis Organization [0.5 pages]**
* How is the remainder of the thesis structured?

---

## Chapter 2: Related Work [20 pages]

**Chapter 2 Abstract [1 page]**
* What has the existing literature established regarding speaker diarization datasets, algorithmic methodologies, and evaluation metrics?
* What specific capability and structural gaps remain in the current paradigms that necessitate further research?
* How do the subsequent sections motivate the thesis contributions?

**2.1 Speaker Diarization Methods [13 pages]** 
* *[Proposed Figure: Timeline of diarization methods]*

* **2.1.1 History of Speaker Diarization Development [3 pages]**
  * What were the limitations of early statistical methods (GMM-UBM), and how did these challenges motivate the transition toward deep-learning clustering approaches (x-vector/VBx)?
* **2.1.2 Clustering-based Methods [2 pages]**
  * How does increased speaker density impact the effectiveness of traditional distance-based clustering thresholds?
* **2.1.3 End-to-End Neural Diarization [2 pages]**
  * How does End-to-End Neural Diarization (EEND) reframe the diarization task, and what performance improvements are introduced by recent architectures such as DiariZen?
* **2.1.4 Target-Speaker Voice Activity Detection [1.5 pages]**
  * How do hybrid paradigms (incorporating TS-VAD concepts within modern neural frameworks) address the limitations associated with permutation invariant training (PIT)?
* **2.1.5 LLM Post-Processing Methods [1.5 pages]**
  * What role do Large Language Models (LLMs) play in semantic post-processing to mitigate acoustic ambiguities?
* **2.1.6 Online Methods [1.5 pages]**
  * How do streaming methods navigate the trade-off between algorithmic latency and segmentation accuracy?
* **2.1.7 Multi-Channel Methods [1.5 pages]**
  * In what ways do multi-channel arrays utilize spatial features to distinguish geometrically separated sound sources?
* **Research Gap (Methods):** What factors contribute to the performance degradation of state-of-the-art methods (including DiariZen) in environments with 10–30 overlapping speakers?

**2.2 Speaker Diarization Datasets and Toolkits [3 pages]** 
* What are the statistical density profiles of foundational corpora like CALLHOME and AMI?
* **Research Gap (Datasets):** What are the limitations of existing datasets regarding overlap density and speaker count, and how do these gaps motivate the construction of Multi-Talker-SD?

**2.3 Evaluation Metrics [1 page]** 
* How are DER and JER mathematically formulated?
* What specific algorithmic behaviors do Missed Speech (MS), False Alarm (FA), and Speaker Confusion (SC) metrics indicate?

**2.4 Performance Evolution and State-of-the-Art Baselines [4 pages]**

* *[Proposed Figure: Comprehensive benchmarking table mapping leading methodologies (e.g., VBx, TS-VAD, DiariZen) against foundational datasets (AMI, DIHARD-III, AliMeeting), detailing overall DER and error component breakdowns.]*
* What are the current lower bounds of DER achieved by state-of-the-art architectures on established benchmarks? 
- How do clustering-based pipelines compare against E2E architectures across datasets with varying overlap ratios?
- How do error distributions (e.g., the MS to SC ratio) shift between modular and E2E systems as benchmark complexity increases?
- What evidence suggests that algorithmic improvements are plateauing on foundational datasets?
- Does this performance saturation indicate that modern architectures are over-fitting to low-density acoustic priors?
- How does zero-shot generalization degrade when models are applied to unconstrained conversational data?
- How does high performance on standard benchmarks obscure critical vulnerabilities? How does this motivate the need for a high-density evaluation framework

---

## Chapter 3: Multi-Talker-SD Benchmark Construction & Diagnostic Evaluation [14 pages]

**3.1 Motivation for Synthetic Benchmark [1.5 pages]**
* What is the rationale for developing synthetic benchmarks in speaker diarization research?
* What are the shortcomings of heuristic random-splicing models in capturing long-term temporal dependencies?

**3.2 Multi-Talker-SD Synthesis Pipeline [5 pages]**
* *[Proposed Figure: Multi-Talker-SD synthesis pipeline block diagram]*
* How are source corpora processed, and how are target overlap/silence ratios parametrically scaled?
* How does the pipeline govern turn-taking logic for varying meeting scenarios?
* How does the Image Source Method (ISM) simulate complex room geometries and reverberation?

**3.3 Statistical Characteristics of Multi-Talker-SD [1.5 pages]**
* *[Proposed Figure: Per-session speaker-count distribution stacked histogram]*
* How does Multi-Talker-SD compare to traditional datasets in terms of speaker cardinality and overlap intensity?

**3.4 Diagnostic Evaluation of SOTA Methods on Multi-Talker-SD and Real-World Datasets [5 pages]** 
* How do representative baselines (VBx, Pyannote, and DiariZen) perform on the new Multi-Talker-SD benchmark?
* How is the performance of these models affected when transitioning from standard real-world datasets to the high-density conditions of Multi-Talker-SD?
* What do the Gantt-chart visualizations and DER breakdowns reveal regarding Missed Speech (MS) and Speaker Confusion (SC) patterns in these baselines?

**3.5 Chapter Summary [1 page]**
* Which specific algorithmic limitations, as revealed by the benchmark, motivate the system-level optimizations proposed in Chapter 4?

---

## Chapter 4: Benchmark-Driven System Optimization and Adaptation [20 pages]

**4.1 Solving Clustering Confusion: Modular Integration of Speech Separation [4 pages]** 
* *[Proposed Figure: Modular pipeline mapping separation + leakage suppression + clustering]*
* To what extent does integrating neural speech separation (e.g., MossFormer2) address the Speaker Confusion (SC) rates observed in clustering baselines?
* How can OSD gating and explicit boundary refinement be utilized to mitigate non-linear separation artifacts and reduce False Alarms?

**4.2 Solving E2E Scalability: Modularized Target-Speaker VAD (TS-VAD+) [4 pages]** 
* *[Proposed Figure: TS-VAD+ architecture block diagram including WavLM, DEMUCS, and Transformer]*
* How does the proposed TS-VAD+ architecture (incorporating large-scale SSL representations and cascaded Transformers) help address the scalability limitations of EEND models?
* What is the effect of the Profile Enhancement module (DEMUCS) on noisy enrollment profiles in unconstrained environments?

**4.3 Solving Domain Bias: Density-Aware Data Adaptation for DiariZen [3.5 pages]** 
* What evidence suggests that pre-trained models like DiariZen tend to over-fit to a "low-density acoustic prior"?
* How does the proposed layer-wise freezing and data-mixing strategy facilitate DiariZen's adaptation to dense overlap scenarios while mitigating catastrophic forgetting?

**4.4 Comprehensive Experimental Evaluation and Ablation Analysis [8 pages]** 
* **4.4.1 Experimental Protocol and Implementation Details [1.5 pages]**
  * What are the specific hyperparameter configurations, sliding-window settings, and hardware environments used for model training and inference?
  * What is the rationale for enforcing a 0.0-second forgiveness collar across evaluations to analyze overlap performance?
* **4.4.2 Quantitative Results on Multi-Talker-SD [2 pages]**
  * What are the absolute Diarization Error Rate (DER) reductions achieved by the three proposed optimizations (Separation, TS-VAD+, DiariZen adaptation) across varying noise and overlap conditions?
  * How do the specific error components (Missed Speech vs. False Alarm vs. Speaker Confusion) shift after applying these interventions?
* **4.4.3 Cross-Domain Generalization (DIHARD-III & AliMeeting) [1.5 pages]**
  * How do the models optimized on synthetic Multi-Talker-SD perform in cross-domain transfers to realistic datasets like DIHARD-III and AliMeeting?
* **4.4.4 Qualitative Visual Analysis [1 page]**
  * *[Proposed Figure: Gantt-chart visualization comparing reference RTTM vs. baseline vs. optimized system]*
  * How do Gantt chart visualizations illustrate the impact of the proposed methods on temporal truncation and boundary bridging in dense overlap regions?
* **4.4.5 Ablation Studies on Systemic Vulnerabilities [2 pages]**
  * *[Proposed Figure: 2x2 panel ablation bar chart across four factor axes]*
  * How is the system's tracking stability affected when evaluated on bilingual code-switching segments?
  * How does performance vary as speaker density increases to 16+ participants, and what does this indicate about latent space representation?
  * How does the performance vary across structurally different meeting scenarios (e.g., Interviews vs. Discussions)?
  * How does homogeneous gender composition (e.g., all-male or all-female sessions) affect the embedding discriminability of the optimized systems?

**4.5 Chapter Summary [0.5 pages]**
* To what extent do these experimental findings support the efficacy of the proposed benchmark-driven optimization framework?

---

## Chapter 5: Conclusion and Outlook [3 pages]

**5.1 Summary of Contributions [1.5 pages]**
* How did the creation of Multi-Talker-SD (Chapter 3) address the dataset gaps identified in the literature review?
* How did the density-aware domain adaptation strategy and TS-VAD+ architecture (Chapter 4) address the methodological limitations of existing models?

**5.2 Future Directions [1.5 pages]**
* How might joint acoustic-lexical reasoning with LLMs help address long-term intra-speaker variance?
* What are the next architectural requirements for achieving ultra-low latency streaming without sacrificing segmentation accuracy?
* How can scalable architectures handle ultra-high-density (>30 speakers) sessions beyond the Multi-Talker-SD range?
* How could unsupervised test-time adaptation (TTA) enable open-world deployment without reliance on pre-annotated data?