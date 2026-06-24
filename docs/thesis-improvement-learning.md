# Learning: How to Improve the Thesis

This document summarizes what I learned while revising the thesis, based on supervisor feedback, review notes, and the process of integrating the two paper contributions into one coherent thesis.

## 1. Make the Thesis a Single Argument

The thesis should not read as separate papers placed back to back. The main argument is:

> Existing diarization benchmarks do not sufficiently stress dense multi-speaker meeting conditions; therefore, we need a controllable benchmark to diagnose system failures, and those diagnoses should guide targeted system improvements.

This means each chapter must have a clear role:

- Chapter 1 introduces the problem and the benchmark-driven thesis logic.
- Chapter 2 explains why existing methods and datasets are insufficient.
- Chapter 3 builds Multi-Talker-SD and uses it diagnostically.
- Chapter 4 improves diarization systems based on the observed failures.
- Chapter 5 closes the loop by mapping each contribution back to the original gaps.

## 2. Put Research Gaps Next to the Literature They Come From

One important lesson was that a late, generic "research gap" section is weaker than topic-adjacent gap paragraphs. Dataset gaps should appear immediately after reviewing datasets. Method gaps should appear immediately after reviewing methods.

This makes the thesis easier to defend because the reader can see:

- what the literature established,
- what it failed to solve,
- which thesis chapter addresses that failure.

## 3. Align Chapter Order with Contribution Order

The contribution order is benchmark construction followed by system optimization. The literature review should therefore prepare the reader for that sequence. If methods are reviewed before datasets, the chapter must explicitly explain why.

The best structure is:

1. speaker diarization history and methods,
2. datasets and benchmark limitations,
3. metrics and performance evolution,
4. explicit mapping to Chapter 3 and Chapter 4.

## 4. Use Page Budgets as a Thinking Tool

Page budgets are not just formatting. They force decisions about importance. Without them, a chapter can become unbalanced, and the thesis may spend too much space on background while under-explaining the actual contributions.

The working target was a master's thesis of roughly 67-72 pages, with two contribution chapters:

- Chapter 3: benchmark construction and diagnostic evaluation.
- Chapter 4: benchmark-driven system optimization and adaptation.

## 5. End Contribution Chapters with Summary and Handoff

Each contribution chapter should end with a short summary that does more than repeat results. It should answer:

- What did this chapter establish?
- Which limitation remains?
- How does the next chapter address that limitation?

For this thesis, Chapter 3 should hand off to Chapter 4 by showing which Multi-Talker-SD failure modes motivate separation-aware clustering, TS-VAD+, and density-aware adaptation.

## 6. Keep Plan Questions Clean

The question-list drafts improved when each bullet asked one question only. Multi-clause questions make the thesis plan look unfocused.

Good plan questions are:

- short,
- answerable,
- tied to a section,
- free of decorative adverbs,
- not overloaded with final numerical results.

Numbers such as exact DER reductions or average speaker counts belong in the thesis prose and results tables, not in early planning bullets.

## 7. Figures Should Explain the Argument

The most useful figures are not decorative. They should help the reader understand the thesis logic:

- a challenge overview for dense meeting diarization,
- a benchmark-to-diagnosis-to-optimization flow,
- a diarization method timeline,
- a Multi-Talker-SD synthesis pipeline,
- dataset comparison tables,
- Gantt-style RTTM visualizations,
- ablation charts for language, density, meeting type, and gender composition.

The separate illustration guide repository records the figure-making workflow:

<https://github.com/wyhzhen6/ai-illustration-guide>

## 8. Reproducibility Must Be Visible

A thesis repository should make it obvious where to find:

- the final PDF,
- raw LaTeX files,
- raw figures,
- experiment code,
- data generation instructions,
- commands for rebuilding the work.

That is why this repository separates thesis source, slides, documents, and code pointers instead of leaving everything mixed in one folder.
