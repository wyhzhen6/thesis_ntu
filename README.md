# Robust Speaker Diarization for Multi-Speaker Meetings

This repository is the central GitHub homepage for my thesis materials, papers, experiment code pointers, figures, and reproducibility notes.

The thesis studies speaker diarization in dense multi-speaker meetings, with a benchmark-driven workflow: build a harder meeting benchmark, use it to diagnose failure modes in existing diarization systems, then improve diarization pipelines through speech separation, TS-VAD-style modeling, and density-aware adaptation.

## Repository Contents

| Path | Contents |
| --- | --- |
| [`thesis/thesis_yihao.pdf`](thesis/thesis_yihao.pdf) | Compiled thesis PDF. |
| [`thesis/thesis_ntu.zip`](thesis/thesis_ntu.zip) | Raw LaTeX source, bibliography files, NTU thesis class, styles, and thesis figures. |
| [`slides`](slides) | Thesis presentation slides and generated slide assets. |
| [`docs/thesis-improvement-learning.md`](docs/thesis-improvement-learning.md) | My learning notes on how to improve the thesis structure, writing, figures, and reproducibility. |
| [`docs/reproduce.md`](docs/reproduce.md) | Step-by-step notes for rebuilding the thesis and rerunning the research workflow. |
| [`code`](code) | Entry point for the experiment/code repositories used by this thesis. |

## Thesis Contributions

1. **Benchmark construction and diagnosis**  
   Multi-Talker-SD is a large-scale bilingual English-Mandarin meeting diarization benchmark for dense multi-speaker sessions. It is designed to expose failures that are hidden by lower-density public benchmarks.

2. **Clustering-based diarization with speech separation**  
   The thesis analyzes when neural speech separation helps or hurts clustering-based diarization, especially under overlap, noise, and speaker-confusion trade-offs.

3. **Benchmark-driven system optimization**  
   The thesis uses benchmark findings to guide system-level changes, including separation-aware diarization, TS-VAD+ style modeling, and density-aware adaptation.

## Related Paper Repositories

- **Analysis of Clustering-based Speaker Diarization Performance Trade-offs with Speech Separation**  
  Repository: <https://github.com/wyhzhen6/reclustering>

- **A Benchmark Dataset for Multi-Speaker Meeting Diarization**  
  Repository: <https://github.com/wyhzhen6/MULTI-TALKER-SD>

- **AI illustration guide for thesis figures**  
  Repository: <https://github.com/wyhzhen6/ai-illustration-guide>

## How to Redo This Work

Start from [`docs/reproduce.md`](docs/reproduce.md). The short version is:

1. Extract [`thesis/thesis_ntu.zip`](thesis/thesis_ntu.zip) and build the thesis from `mythesis.tex`.
2. Prepare the Multi-Talker-SD data generation environment from the dataset repository.
3. Run the diarization baselines and the separation-enhanced clustering experiments.
4. Regenerate figures from experiment outputs and update the LaTeX source.
5. Recompile the thesis PDF.

## GitHub Ownership Note

The Anh should be added as an owner or admin collaborator after the repository is created on GitHub. For a personal repository, GitHub does not allow another user to be a second "owner"; invite The Anh as a collaborator with **Admin** permission. For organization-owned repositories, add both maintainers as repository owners/admins through the organization team settings.

## Current Build Note

The included PDF was compiled locally from the LaTeX source. BibTeX currently reports duplicated bibliography keys in `References/first_paper.bib`; the PDF is generated, but the bibliography pass should be cleaned before final archival release.
