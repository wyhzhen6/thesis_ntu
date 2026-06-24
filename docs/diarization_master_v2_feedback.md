# Stage-2 Review — Speaker-Diarization Master-Level Plan (23 Apr 2026)

**Document:** `2-revise/Question List_master_level_thesis.docx`
**Title:** *Robust Speaker Diarization for Multi-Speaker Meetings*
**Stage:** 2 (list of questions / writing plan)
**Skill:** `list-of-questions` (voice v2 — clearer wording, figures as suggestions)

**Classification: AMBIGUOUS.** Filename says `master_level_thesis`, which maps to 1 contribution chapter and ~30–50 p total. The plan declares 2 contribution chapters (Ch 3 *Multi-Talker-SD Benchmark Construction* and Ch 4 *Benchmark-Driven System Optimization*), which is PhD-shape. **No page annotations anywhere** — no `[N pages]` on any chapter, section, or subsection. The classification cannot be completed without either a page declaration or a clarification from the student on format.

> The student must declare, on the first revision: (a) is this a master's thesis (~35–50 p, usually 1 contribution chapter) or a PhD / QE (55–115 p, 1–3 contribution chapters), and (b) the page budget per chapter and per section. Without these, the review below focuses on structure and question quality; balance, sum checks, and scale-sensitive thresholds cannot be run.

---

## Structural Issues

1. **[MUST-FIX] PAGE-MATH: page budgets entirely absent.** Every chapter, section, and subsection must carry an `[N pages]` annotation at Step 2. This is not a stylistic preference — the budget is the mechanism by which the student allocates effort between literature and contribution. Without it, no one can tell whether Ch 3 is a 20-p contribution or a 5-p data-sheet. *Reference:* Fabian's SSL plan (`fabian_v2_feedback.md`) is a worked example of how pages should be declared.
2. **[MUST-FIX] SIGNPOST-OPENER (Ch 2):** Ch 2 begins directly with §2.1. No chapter abstract. Write a 3–4-paragraph abstract at the top of Ch 2 naming (a) what the literature has established about speaker diarization, (b) what gaps the two contribution chapters close, and (c) which lit subsection motivates which contribution chapter (§2.3 datasets → Ch 3 benchmark; §2.1 methods + §2.2 metrics → Ch 4 optimization).
3. **[MUST-FIX] MAPPING: Ch 2 never states which lit section motivates which contribution chapter.** §2.1 reviews methods, §2.2 metrics, §2.3 datasets — but the reader has to guess that Ch 3 (benchmark) is driven by §2.3, and Ch 4 (optimization) by §2.1. Fix by rewriting §2.4 (see item 4 below) *and* by adding one sentence at the end of each Ch 2 lit subsection naming the downstream chapter.
4. **[MUST-FIX] GAP-PLACEMENT: §2.4 *Research Gap in Meeting Scenario Speaker Diarization* is a terminal gap section.** This is the exact defect the supervisor flags most often. By §2.4 the reader has seen all methods, metrics, and datasets and cannot trace which gap supports which chapter. Dissolve §2.4. Insert instead: a short gap paragraph at the end of §2.1 (gap for methods → Ch 4), a short gap paragraph at the end of §2.3 (gap for datasets → Ch 3). The gap for benchmark must be adjacent to the benchmark discussion, not after it.
5. **[MUST-FIX] Ch 2 ordering does not follow contribution order.** Contributions run Ch 3 (benchmark) → Ch 4 (optimization), so Ch 2 should run *datasets first, methods second*. Currently it is methods (§2.1) → metrics (§2.2) → datasets (§2.3). Reorder to §2.1 Datasets and benchmarks → §2.2 Diarization methods → §2.3 Evaluation metrics, which maps Ch 3 ← §2.1, Ch 4 ← §2.2. If the student wants to keep methods first for narrative reasons, that requires justification in the new chapter abstract (item 2).
6. **[MUST-FIX] MISSING-SUMMARY (Ch 3, Ch 4):** Ch 3 ends with §3.3 *Statistical Characteristics of Multi-Talker-SD*, which is a results-style subsection, not a summary. Ch 4 ends with §4.3.6 *Ablation Studies*, likewise. Each contribution chapter must end with a Summary section naming the takeaway and handing off to the next chapter. Add §3.4 *Chapter Summary* (handoff to Ch 4: "what benchmark finding motivates the system-optimization interventions of Ch 4?") and §4.4 *Chapter Summary* (handoff to Ch 5 conclusions).
7. **[SHOULD-FIX] Ch 1 §1.4 *Thesis Organization* has a single bullet.** A one-bullet section is acceptable but thin. Add a second bullet: "How do Ch 3 and Ch 4 build on each other — benchmark → diagnosis → optimisation?"
8. **[SHOULD-FIX] Ch 4 §4.3 has 6 flat sub-subsections (§4.3.1 – §4.3.6).** Borderline FLAT-LIST. Group: §4.3.1 + §4.3.2 → *Experimental protocol* (outline + datasets/metrics); §4.3.3 + §4.3.4 → *Baselines and adaptation strategy*; §4.3.5 + §4.3.6 → *Results and ablations*. Result: 3 sub-subsections, readable.
9. **[SHOULD-FIX] No separate Conclusion chapter in contribution-style.** Ch 5 *Conclusion and Outlook* with only §5.1 (1 bullet) and §5.2 (3 bullets) is compact. A proper conclusion has (a) one summary bullet per contribution, (b) a revisit of the Ch 2 gaps showing each is closed, (c) future work. Expand §5.1 to ask "How do the benchmark contribution (Ch 3) and the optimization contribution (Ch 4) close the gap identified in §2.3 / §2.1?" — making the conclusion round-trip to the gap statements is what turns this from an outline into a thesis.

## Section-by-Section

### Chapter 1 — Introduction

- §1.1 *Background and Motivation*: Pyramid opener is correct ("How is SD formally defined … and why is it an indispensable front-end technology …"). Good history bullet in §1.1.3 ("how have historical datasets dictated algorithmic evolution …"). ✓
- §1.1 bullet 1, bullet 3: **VERBOSE-Q**. Both bullets join two questions with ", and ...". Split (see bullet-level annotations below).
- §1.2 *Challenges in Meeting Speaker Diarization*: Good four-challenge enumeration (far-field, overlap, noise, dynamic speaker count). Each bullet is one clause. ✓
- §1.2 bullets use decorative adverbs ("mathematically distort", "notoriously difficult", "factorial scalability bottleneck"). See *Voice and register* note at the end of this section.
- §1.3 *Thesis Objectives and Contributions*: Three bullets, each one of them asks something reasonable. But the contribution split between Ch 3 and Ch 4 is never stated — a reader cannot tell from §1.3 alone that there are two contribution chapters. Add a bullet: "What are the two core contributions of this thesis — benchmark construction (Ch 3) and system optimization (Ch 4) — and how are they coupled?"
- §1.4: See Structural Issue 7.

### Chapter 2 — Related Work

- §2.1 *Speaker Diarization Methods*: 7 bullets, covering GMM → x-vector → EEND → TS-VAD → LLM post-processing → streaming → multi-channel. The history progression is excellent, but: (a) seven bullets is too many for one section — the section will read as a list of unrelated questions rather than a coherent narrative. Split: §2.1.1 *Classical and statistical methods*, §2.1.2 *End-to-end and target-speaker methods*, §2.1.3 *Complementary directions (LLM / streaming / multi-channel)*. (b) No explicit gap bullet anchoring the section to Ch 4. Add one after the section: *Gap for Ch 4 — why none of the reviewed methods work at 10–30 speaker density under overlap*.
- §2.2 *Evaluation Metrics and Performance Evolution*: 2 bullets. Has the "chronological tracking of DER" history bullet. ✓
- §2.3 *Speaker Diarization Datasets and Toolkits*: 2 bullets. This is the section that must motivate Ch 3. Currently the two bullets are descriptive (statistical profiles, toolkit evolution) — neither expresses the gap Ch 3 closes. Add a third bullet: "What specific capability is missing from every existing dataset (overlap density, speaker count, bilingual composition) that motivates the construction of Multi-Talker-SD?"
- §2.4 *Research Gap*: **GAP-PLACEMENT**. See Structural Issue 4 — dissolve.

### Chapter 3 — Multi-Talker-SD Benchmark Construction

- §3.1 *Motivation for Synthetic Benchmark*: 2 bullets, both negative framings of prior work ("fundamental drawbacks", "fail to capture"). The supervisor will ask for a broader pyramid opener — add a first bullet: "Why are synthetic benchmarks necessary in speaker diarization research at all?" Push current bullets to positions 2 and 3.
- §3.2 *Multi-Talker-SD Synthesis Pipeline*: 5 bullets. Well-structured. ✓
- §3.2 bullet 2 "How are the target overlap and silence ratios mathematically extrapolated as logarithmic and exponential functions of the total speaker count?" — **OVER-SPECIFIC** at Step 2. The specific functional form belongs in §3.2 prose at Step 6, not in a plan bullet. Rewrite: "How are target overlap and silence ratios scaled with the number of speakers per session?"
- §3.3 *Statistical Characteristics of Multi-Talker-SD*: 1 bullet — "How does Multi-Talker-SD statistically eclipse traditional datasets in terms of extreme speaker cardinality (**averaging 18.1 speakers**), bilingual composition, and elevated overlap intensity?" **OVER-SPECIFIC** (18.1 avg speakers) and **VERBOSE-Q** (three clauses). Split into: (a) "How does Multi-Talker-SD compare with existing datasets in speaker cardinality?" (b) "... in bilingual composition?" (c) "... in overlap density?". Remove the specific number; cite "averaging 18.1 speakers" in the §3.3 prose at Step 6.
- No §3.4 *Chapter Summary* section. **MISSING-SUMMARY**. See Structural Issue 6.

### Chapter 4 — Benchmark-Driven System Optimization

- §4.1 *Modular Integration of Speech Separation and Enhancement*: 4 bullets. First bullet opens narrow ("Why is integrating speech separation **conceptually appealing** …"). Move the pyramid opener up: "What role does modular speech separation play in the diarization pipeline?" before the conceptually-appealing bullet.
- §4.1 bullet 2 ("How does the Embedding Displacement Ratio (EDR) and t-SNE topological mapping prove that certain separation architectures (e.g., MossFormer2) preserve clustering structures better than others (e.g., Conv-TasNet)?") — **VERBOSE-Q**, four clauses. Split: (a) "What is the Embedding Displacement Ratio and why is it a better proxy for diarization than raw separation SI-SDR?" (b) "How do MossFormer2 and Conv-TasNet compare under EDR?"
- §4.1 bullet 3 "strict empirical boundary conditions (e.g., >5% overlap ratio, >10 dB SNR)" — **OVER-SPECIFIC**. Remove the numbers; rewrite: "Under what overlap-ratio and SNR ranges does separation yield a net DER reduction?"
- §4.2 *Modularized TS-VAD+*: 4 bullets, covering vulnerabilities → SSL features → profile enhancement → cascaded transformer. Good narrative. ✓
- §4.2 bullets use "aggressively", "explicitly", "mathematically" as decorative adverbs. See *Voice and register* note.
- §4.3: 6 flat sub-subsections. **FLAT-LIST (SHOULD-FIX)**. See Structural Issue 8.
- §4.3.1 bullet begins with "Outline:" label — not a question. Drop the label; the question itself ("How is the experimental validation sequentially structured?") is fine.
- §4.3.4 "Why do pre-trained models over-fit to a 'low-density acoustic prior,' and how does layer-wise freezing and data-mixing regularization (replay buffers) prevent catastrophic forgetting during adaptation?" — **VERBOSE-Q**. Split.
- §4.3.6 "How does the system's performance systematically degrade when isolating specific variables such as language code-switching, latent space collapse due to high speaker counts, specific meeting scenarios, and homogeneous gender ratios?" — **VERBOSE-Q**, four clauses. Split into four separate ablation bullets.

### Chapter 5 — Conclusion and Outlook

- §5.1 *Summary of Contributions*: 1 bullet. Too thin — see Structural Issue 9.
- §5.2 *Future Directions*: 3 bullets, reasonable. The LLM bullet ("How can the integration of LLMs and semantic reasoning correct long-term acoustic drift …") is the strongest; keep. The streaming and TTA bullets are fine. Consider adding one architectural bullet: "How can scalable architectures handle ultra-high-density (>30 speaker) sessions beyond the Multi-Talker-SD range?"

## Bullet-level annotations

```
[§1.1.1] VERBOSE-Q (SHOULD-FIX):
"How is 'Speaker Diarization' (SD) formally defined, and why is it an indispensable front-end technology for modern multimodal comprehension?"
→ Comment: two questions joined with "and". Plan bullets should be one clause.
→ Fix: split into
  - "How is speaker diarization formally defined?"
  - "Why is it a front-end technology for multimodal comprehension?"
```

```
[§1.1.3] VERBOSE-Q (SHOULD-FIX):
"How have historical datasets dictated algorithmic evolution, and what are the specific structural limitations (e.g., low speaker density) of current benchmarks?"
→ Comment: two questions, parenthetical example.
→ Fix: split into
  - "How have historical datasets shaped algorithmic evolution in SD?"
  - "What structural limitations of current benchmarks (e.g., low speaker density) remain unaddressed?"
```

```
[§2.1 bullet 1] VERBOSE-Q (SHOULD-FIX):
"What specific environmental bottlenecks drove the paradigm shift from the Statistical Era (GMM-UBM, i-vectors) to the Deep Learning Era (x-vectors), and now to the Multi-Task Era?"
→ Comment: three-era question in one bullet. Also uses decorative capitalisation ("Statistical Era", "Deep Learning Era").
→ Fix: split into
  - "What drove the shift from statistical methods (GMM-UBM, i-vector) to deep-learning methods (x-vector)?"
  - "What drives the current shift toward multi-task and end-to-end approaches?"
```

```
[§2.1 bullet 3] VERBOSE-Q (SHOULD-FIX):
"What architectural innovations allowed End-to-End Neural Diarization (EEND) to natively resolve overlap, and why does Permutation Invariant Training (PIT) create a factorial scalability bottleneck?"
→ Comment: two questions; second is narrower than the first.
→ Fix: split; also drop "factorial" as it is a mathematical claim that belongs in the Step-6 prose.
```

```
[§3.2 bullet 2] OVER-SPECIFIC (SHOULD-FIX):
"How are the target overlap and silence ratios mathematically extrapolated as logarithmic and exponential functions of the total speaker count?"
→ Comment: specific functional form (log / exponential) belongs at Step 5/6.
→ Fix: "How are target overlap and silence ratios scaled with the number of speakers per session?"
```

```
[§3.3 bullet 1] VERBOSE-Q + OVER-SPECIFIC (SHOULD-FIX):
"How does Multi-Talker-SD statistically eclipse traditional datasets in terms of extreme speaker cardinality (averaging 18.1 speakers), bilingual composition, and elevated overlap intensity?"
→ Comment: three claims in one bullet plus a specific number.
→ Fix: split into three one-clause bullets; move "18.1" to §3.3 prose.
```

```
[§4.1 bullet 3] OVER-SPECIFIC (SHOULD-FIX):
"What are the strict empirical boundary conditions (e.g., >5% overlap ratio, >10 dB SNR) required for separation to yield a net positive reduction in DER?"
→ Comment: 5 %, 10 dB are results, not plan-bullet content.
→ Fix: "Under what overlap-ratio and SNR ranges does separation yield a net reduction in DER?"
```

```
[§4.1 bullet 2] VERBOSE-Q (SHOULD-FIX):
"How does the Embedding Displacement Ratio (EDR) and t-SNE topological mapping prove that certain separation architectures (e.g., MossFormer2) preserve clustering structures better than others (e.g., Conv-TasNet)?"
→ Comment: compound question.
→ Fix: split into two bullets (EDR definition; EDR-based comparison between architectures).
```

```
[§4.3.4 bullet] VERBOSE-Q (SHOULD-FIX):
"Why do pre-trained models over-fit to a 'low-density acoustic prior,' and how does layer-wise freezing and data-mixing regularization (replay buffers) prevent catastrophic forgetting during adaptation?"
→ Comment: two questions.
→ Fix: split into
  - "Why do pre-trained diarization models over-fit to low speaker density?"
  - "How do layer-wise freezing and replay-buffer regularisation mitigate catastrophic forgetting during adaptation?"
```

```
[§4.3.6 bullet] VERBOSE-Q (SHOULD-FIX):
"How does the system's performance systematically degrade when isolating specific variables such as language code-switching, latent space collapse due to high speaker counts, specific meeting scenarios, and homogeneous gender ratios?"
→ Comment: four ablation axes in one bullet.
→ Fix: four separate ablation bullets (language; speaker density; meeting scenario; gender composition).
```

## Voice and register (applies throughout)

The plan uses decorative language that obscures the technical claim:

- *"mathematically distort"*, *"notoriously difficult"*, *"aggressively purify"*, *"factorial scalability bottleneck"*, *"natively resolve"*, *"latent space collapse"*.

At Step 2 the bullet has one job: name the question the chapter is going to answer. An adverb that is not load-bearing ("mathematically") should be dropped; a technical claim dressed as an adjective ("factorial") should either be cut or moved to the answer. This is not a per-bullet fix list — it is a pass the student should make on every bullet once before resubmitting. Reference: `academic-writing §2.1` (decorative connectives, peacock adverbs).

## Figure Suggestions

These are suggestions, not required fixes. No figure placeholders currently exist in the plan.

```
[§1.2] Figure suggestion: four-challenge overview (far-field, overlap, noise, dynamic count).
→ Why it helps: §1.2 enumerates four challenges as bullets; a diagram communicates them as a joint failure surface.
→ Rough content: 2×2 grid, one challenge per cell, with a representative spectrogram / diagram per cell.
```

```
[§1.3] Figure suggestion: benchmark → diagnosis → optimisation contribution flow.
→ Why it helps: §1.3 introduces two contribution chapters (Ch 3 benchmark, Ch 4 optimisation) that feed into each other. The dependency is the thesis' structural claim.
→ Rough content: three boxes (Multi-Talker-SD benchmark, diagnostic study, targeted optimisation) with arrows.
```

```
[§2.1] Figure suggestion: timeline of diarization methods (GMM / x-vector / EEND / TS-VAD / LLM / streaming).
→ Why it helps: §2.1 has 7 bullets that are essentially a chronological list. A timeline reads faster than prose.
→ Rough content: horizontal timeline with markers for each era; short caption per marker.
```

```
[§2.3] Figure suggestion: dataset-comparison table (CALLHOME / DIHARD / CHiME / AliMeeting vs. Multi-Talker-SD).
→ Why it helps: the Ch 3 gap is a dataset-shape gap; a table showing speaker count, overlap ratio, language, duration, and domain is the concrete comparison the student will want to defend.
→ Rough content: 5-column × 6-row comparison table.
```

```
[§3.2] Figure suggestion: Multi-Talker-SD synthesis pipeline block diagram.
→ Why it helps: §3.2 has 5 bullets covering preprocessing → ratio extrapolation → turn-taking simulation → acoustic scene → metadata. A pipeline diagram is the natural reading aid.
→ Rough content: five-stage horizontal pipeline with inputs (LibriSpeech, AISHELL-1) and outputs (RTTM, UEM, metadata).
```

```
[§3.3] Figure suggestion: per-session speaker-count distribution histogram.
→ Why it helps: §3.3 makes a cardinality claim; a histogram is the most direct evidence.
→ Rough content: stacked histogram with Multi-Talker-SD in colour and AMI / AliMeeting / DIHARD as reference bars.
```

```
[§4.1] Figure suggestion: modular pipeline with separation + leakage suppression.
→ Why it helps: §4.1 introduces several plug-in components (OSD gating, Crosstalk VAD, boundary refinement). A diagram clarifies the order.
→ Rough content: signal path with separation → OSD → CtVAD → speaker-embedding extraction → clustering.
```

```
[§4.2] Figure suggestion: TS-VAD+ architecture (SSL features + profile enhancement + cascaded transformer).
→ Why it helps: §4.2 is the paper's main algorithmic contribution. A concrete architecture figure is essentially required.
→ Rough content: three-block diagram: WavLM Base+ → DEMUCS → ECAPA-TDNN → cascaded Transformer → frame-level decisions.
```

```
[§4.3.5] Figure suggestion: Gantt-chart visualisation (truncation / fragmentation in heavy overlap).
→ Why it helps: the §4.3.5 bullet already promises "Gantt chart visualisations" — the bullet is itself a figure request. Make it explicit.
→ Rough content: reference RTTM (top) vs. system RTTM before / after fine-tuning in a heavy-overlap window.
```

```
[§4.3.6] Figure suggestion: ablation bar chart across four factors.
→ Why it helps: if the four ablation axes are split as suggested, a single four-panel bar chart captures all ablations.
→ Rough content: 2×2 panel — language code-switching, speaker density, meeting scenario, gender composition — DER on y-axis.
```

## Summary Verdict

The plan is **not yet Step-2-ready**. The biggest blocker is the complete absence of page budgets: without them, balance, allocation, and feasibility cannot be assessed by the supervisor and the student has no mechanism for pacing effort across chapters. Second-biggest blocker is the terminal gap section (§2.4) combined with the missing Ch 2 chapter abstract and the reversed Ch 2 ordering relative to Ch 3 / Ch 4 — together these make the literature-to-contribution mapping invisible. Third, Ch 3 and Ch 4 both lack summary sections, breaking the chapter-to-chapter handoff. At the bullet level the dominant issue is verbose multi-clause questions (eight flagged above) and decorative adverbs throughout; a single cleanup pass will fix this. Another full Step-2 iteration is required before the student can move to Step 5. Suggested first revision pass, in order: (1) declare page budgets, (2) write a Ch 2 chapter abstract, (3) dissolve §2.4 into topic-adjacent gap paragraphs, (4) reorder Ch 2 so §2.3 (datasets) precedes §2.1 (methods), (5) add §3.4 and §4.4 summary sections, (6) one cleanup pass on verbose-question bullets.

---

*Review generated by Supervisor-Agent (`list-of-questions` skill, voice v2), 2026-04-23.*
