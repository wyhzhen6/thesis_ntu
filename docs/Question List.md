# Robust Speaker Diarization for Multi-Speaker Meetings
**Total: Chapters 1–5, 73 pages**

## Thesis Abstract
Speaker diarization—the task of determining "who spoke when" within multi-speaker audio streams—is a fundamental prerequisite for extracting structured information from intelligent meeting systems. Despite growing demand, existing algorithms exhibit severe performance degradation when confronted with complex, real-world acoustic conditions, such as far-field reverberation, high overlap ratios, non-stationary background noise, and dynamic speaker participation. Furthermore, current public benchmarks predominantly feature low speaker densities or controlled environments. Such datasets fail to capture the intricate dynamics of industrial-grade meetings and lack the precise diagnostic granularity required for robust system optimization. To bridge the gap between current training paradigms and real-world complexities, this thesis introduces a benchmark-driven optimization framework that encompasses three interconnected contributions:

**Benchmark construction:** We develop a scenario-driven synthesis pipeline that explicitly models realistic interactive patterns and spatial acoustics. This pipeline generates Multi-Talker-SD, a highly challenging bilingual (English–Mandarin) benchmark comprising 1,110 sessions with 10–30 concurrent speakers, totaling over 1,200 hours. The dataset simulates authentic discussions, interviews, and presentations by rigorously controlling utterance order, overlap ratios, silence durations, and spatial arrangements.

**Diagnostic evaluation:** Utilizing Multi-Talker-SD as a diagnostic tool, we systematically evaluate and pinpoint the precise failure modes of existing modular and end-to-end (E2E) architectures. Our evaluations reveal a critical scalability bottleneck: the Diarization Error Rate (DER) increases substantially when systems are applied to high-density sessions, accompanied by severe cross-lingual performance degradation.

**System-level optimization:** Guided by these diagnostic insights, we address specific algorithmic vulnerabilities through targeted architectural interventions. For modular pipelines, we propose an overlap-aware integration of neural speech separation, fortified by leakage suppression. For target-speaker architectures, we upgrade the conventional framework to TS-VAD+ by integrating large-scale self-supervised learning (SSL) representations and deep profile enhancement. Finally, we mitigate end-to-end domain bias via a density-aware domain adaptation strategy.

Experimental results demonstrate that these synergistic optimizations achieve an absolute DER reduction of 3–4% under severe noise and reverberation conditions. Furthermore, they successfully reduce the zero-shot DER on the independent DIHARD-III benchmark from 19.53% to 17.97%.

---

## Publications
The materials presented in this thesis are based on the following publications:

1. **"A Benchmark Dataset for Multi-Speaker Meeting Diarization"**
   - *Status:* Under review for In Proceedings of the Annual Conference of the International Speech Communication Association (Interspeech), 2026.
   - *Authorship:* First author

2. **"TS-VAD+: Modularized Target-Speaker Voice Activity Detection for Robust Speaker Diarization"**
   - *Status:* In Asia-Pacific Signal and Information Processing Association Annual Summit and Conference (APSIPA ASC), 2025.
   - *Authorship:* Third author

3. **"Analysis of Clustering-based Speaker Diarization Performance Trade-offs with Speech Separation"**
   - *Status:* Under review for 29th International Conference on Text, Speech and Dialogue(TSD), 2026.
   - *Authorship:* First author

---

## Chapter 1: Introduction [7 pages]

### 1.1 Background and Motivation [3 pages]
* How is "Speaker Diarization" (SD) formally defined?
* Why is SD an indispensable front-end technology for downstream tasks like multi-speaker ASR?
* What unique acoustic and conversational complexities characterize multi-speaker meeting scenarios?
* How have historical datasets dictated the trajectory of algorithmic evolution?
* What are the specific structural limitations of current benchmarks regarding speaker density?
* Why is scenario-driven synthetic simulation the most viable path forward?

### 1.2 Challenges in Meeting Speaker Diarization [2 pages]
* How do far-field acoustics and reverberation compromise the discriminative capacity of speech embeddings?
* Why does overlapping speech mathematically violate the mutual exclusivity assumption of modular systems?
* How does overlapping speech cause severe false negatives in E2E architectures?
* How does complex background noise explicitly induce "VAD fragmentation"?
* Why does an unknown and fluctuating speaker count cause cascading failures in distance-based clustering?

### 1.3 Thesis Objectives and Contributions [1.5 pages]
* How does the proposed Multi-Talker-SD framework depart from conventional heuristic random-splicing methods?
* How does the benchmark expose the latent flaws of SOTA models in high-density environments?
* How are these diagnostic insights utilized to implement targeted, modular algorithmic improvements?
* How does benchmark-driven data adaptation mitigate overlap-induced false negatives and far-field identity switching?

### 1.4 Thesis Organization [0.5 pages]
* How is the remainder of the thesis structured?

---

## Chapter 2: Related Work [28 pages]

### 2.1 Speaker Diarization Methods [18 pages]
#### 2.1.1 History of Speaker Diarization Development [3 pages]
* What defined the Statistical Era (GMM-UBM, i-vectors) of speaker diarization?
* What specific environmental bottlenecks drove the transition to the Deep Learning Era?
* What characterizes the emerging Multi-Task Era?

#### 2.1.2 Clustering-based Methods [3 pages]
* How do AHC and VBx function within the standard modular pipeline?
* Why is the distance threshold in AHC highly sensitive to acoustic domain shifts?
* How does the overlap problem mathematically break the core assumptions of clustering?

#### 2.1.3 End-to-End Neural Diarization [3 pages]
* How does EEND reframe diarization entirely as a multi-label sequence-to-sequence classification problem?
* How does the self-attention mechanism capture local temporal dynamics and global speaker characteristics?
* Why does Permutation Invariant Training (PIT) create a factorial scalability bottleneck?

#### 2.1.4 Target-Speaker Voice Activity Detection [3 pages]
* How does TS-VAD decouple identity extraction from temporal boundary prediction?
* How does the architecture utilize pre-extracted speaker embeddings as "attractors"?
* Why does the Binary Cross-Entropy (BCE) loss resolve the factorial limits of PIT?

#### 2.1.5 LLM Post-Processing Methods [3 pages]
* Why do purely acoustic models inevitably suffer from "semantic blindness"?
* How do Large Language Models correct acoustic confusion using conversational logic?
* How are prompts engineered to anchor lexical correction to continuous acoustic evidence?

#### 2.1.6 Online Methods [1.5 pages]
* What is the critical trade-off between algorithmic latency and accuracy in streaming diarization?
* How do chunking mechanisms and global memory operate within the causal horizon?
* What is the "absolute decision" dilemma inherent in low-latency streaming architectures?

#### 2.1.7 Multi-Channel Methods [1.5 pages]
* How does far-field reverberation artificially homogenize the single-channel acoustic space?
* How do multi-channel arrays extract orthogonal spatial features like TDOA and DOA?
* How do modern neural architectures directly fuse acoustic and spatial representations?

### 2.2 Evaluation Metrics and Performance Evolution [5 pages]
#### 2.2.1 Standard Evaluation Metrics [3 pages]
* How is the Diarization Error Rate (DER) mathematically formulated?
* What specific algorithmic failures do Missed Speech, False Alarms, and Speaker Confusion indicate?
* Why does the Jaccard Error Rate (JER) provide a more balanced, speaker-centric evaluation?

#### 2.2.2 Benchmark Performance Comparison and Methodological Evolution [2 pages]
* What do historical DER evaluations on DH3, AliMeeting, and AMI reveal about algorithmic vulnerabilities?
* How does benchmark saturation on low-density datasets indicate a deceptive algorithmic plateau?

### 2.3 Speaker Diarization Datasets and Toolkits [3 pages]
* What are the statistical density profiles of foundational corpora like CALLHOME and AMI?
* How have software ecosystems evolved from Kaldi's statistical pipelines to ESPnet, Pyannote, and NeMo?

### 2.4 Research Gap in Meeting Scenario Speaker Diarization [2 pages]
* Why are current public benchmarks fundamentally insufficient for evaluating large-scale meetings?
* Why do threshold-based clustering systems completely collapse when the latent space is overcrowded?

---

## Chapter 3: Multi-Talker-SD Benchmark Construction [10 pages]

### 3.1 Motivation for Synthetic Benchmark [2 pages]
* What are the fundamental drawbacks of traditional random-splicing synthesis methodologies?
* Why do purely heuristic models fail to capture long-term temporal dependencies and bursty overlap behaviors?

### 3.2 Multi-Talker-SD Synthesis Pipeline [6 pages]
#### 3.2.1 Source Data and Preprocessing [1 page]
* Why were LibriSpeech and AISHELL-1 selected as the source corpora?
* How are clean speech segments standardized, normalized, and fragmented during preprocessing?

#### 3.2.2 Overlap and Silence Patterns [2 pages]
* How is the target overlap rate modeled as a logarithmic growth function of the speaker count?
* How is the target silence rate modeled as an exponential decay function?

#### 3.2.3 Dialogue Scene Generation [1 page]
* How does the pipeline explicitly govern turn-taking logic for Discussions, Interviews, and Presentations?

#### 3.2.4 Acoustic Scene Simulation [1 page]
* How does the Image Source Method (ISM) simulate complex room geometries and reverberation?
* How are distinct point-source noises and diffuse ambient noise fields injected into the mixture?

#### 3.2.5 Output and Evaluation Metadata [1 page]
* How does the generated RTTM provide millisecond-level temporal boundary precision?
* What multidimensional metadata is generated to support fine-grained algorithmic diagnostics?

### 3.3 Statistical Characteristics of Multi-Talker-SD [2 pages]
* How does the benchmark's extreme speaker cardinality (average 18.1) eclipse traditional datasets?
* How does its bilingual composition and high overlap intensity (20%-40%) stress-test modern architectures?

---

## Chapter 4: Benchmark-Driven System Optimization and Data Adaptation [24 pages]

### 4.1 Modular Integration of Speech Separation and Enhancement [6 pages]
#### Motivation [1 page]
* Why is integrating neural speech separation an intuitive architectural solution for speaker confusion?

#### The Modular Evaluation Framework [1 page]
* How is the sequential pipeline structured to isolate non-linear separation artifacts?

#### Representational Trade-off (EDR) [1.5 pages]
* How does the Embedding Displacement Ratio (EDR) mathematically quantify structural deviation?
* How does t-SNE visualization prove that MossFormer2 preserves clustering topologies better than Conv-TasNet?

#### Utility Boundary of Speech Separation [1.5 pages]
* Why is an intrinsic overlap ratio of at least 5% empirically required for a net DER reduction?
* Why does separation regress performance under severe noise conditions (e.g., 0 dB SNR)?

#### System-Level Optimization and Ablation Analysis [1 page]
* How does cross-channel leakage mechanically inflate the False Alarm rate?
* How do OSD gating, Crosstalk VAD, and explicit boundary refinement suppress these artifacts?

### 4.2 Modularized Target-Speaker Voice Activity Detection (TS-VAD+) [5 pages]
#### Motivation [1 page]
* What vulnerabilities exist in conventional TS-VAD frameworks regarding BLSTM temporal modeling and noisy enrollment profiles?

#### The Proposed Framework [2 pages]
* How do large-scale SSL representations (e.g., WavLM) provide greater robustness than traditional features?
* How does the Profile Enhancement module (DEMUCS) actively purify target speaker profiles?
* How does the cascaded Transformer architecture leverage global contextual information?

#### Experimental Efficacy and Ablation Analysis [2 pages]
* How significantly does the TS-VAD+ front-end outperform conventional pipelines on the AliMeeting dataset?
* How does intersecting soft Transformer probabilities with hard Pyannote VAD edges slash the FA rate on DIHARD-III?

### 4.3 Experimental Results and Discussion [13 pages]
#### 4.3.1 Outline [1 page]
* How does the experimental evaluation logically progress from foundational setups to analytical ablations?

#### 4.3.2 Datasets and Evaluation Metrics [1 page]
* Why is a strict 0.0-second forgiveness collar enforced to accurately diagnose overlap vulnerabilities?

#### 4.3.3 Implementation Details and Baselines [2 pages]
* What are the dataset partitioning protocols, hardware specifications, and sliding-window configurations?
* How are the zero-shot baseline inferences established for VBx, Pyannote, and E2E systems?

#### 4.3.4 Benchmark-Driven Data Adaptation Strategy [3 pages]
* Why do pre-trained end-to-end models structurally over-fit to a "low-density acoustic prior"?
* How does layer-wise freezing preserve universal phonetic representations while optimizing the EEND header?
* How does the data-mixing regularization strategy prevent catastrophic forgetting of sparse conversational dynamics?

#### 4.3.5 Comprehensive Performance and Qualitative Analysis [3 pages]
* What are the absolute quantitative DER reductions achieved by fine-tuning DiariZen across clean and noisy conditions?
* How do Gantt chart visualizations prove the resolution of truncation and boundary bridging in dense overlap regions?

#### 4.3.6 Ablation Studies and Factor Analysis [3 pages]
* How do frequent language shifts in code-switching disrupt long-term spectral averages?
* How does the t-SNE visualization explicitly illustrate latent space collapse at high speaker densities (16+)?
* How do varying meeting scenarios and homogeneous gender ratios parametrically influence the DER?

---

## Chapter 5: Conclusion and Outlook [4 pages]

### 5.1 Summary of Contributions [2 pages]
* How did the creation of Multi-Talker-SD bridge the gap between dataset limitations and algorithmic evaluation?
* How did the density-aware domain adaptation strategy and modular TS-VAD+ architecture effectively overcome low-density biases?

### 5.2 Future Directions [2 pages]
* How can joint acoustic-lexical reasoning with LLMs resolve long-term intra-speaker variance?
* What are the next architectural requirements for achieving ultra-low latency streaming without sacrificing segmentation accuracy?
* How can unsupervised test-time adaptation (TTA) enable true open-world deployment without reliance on pre-annotated data?