# Experiment Code

This directory is the entry point for the code used by the thesis. The main experiment repositories are maintained separately so they can keep their own dependencies, issues, and release histories.

## Repositories

| Work | Repository | Role in Thesis |
| --- | --- | --- |
| Multi-Talker-SD benchmark | <https://github.com/wyhzhen6/MULTI-TALKER-SD> | Chapter 3 benchmark construction, metadata generation, acoustic simulation, and diagnostic evaluation. |
| Speech separation and clustering trade-off analysis | <https://github.com/wyhzhen6/reclustering> | Chapter 4 clustering-based diarization experiments with neural speech separation. |
| Thesis illustration workflow | <https://github.com/wyhzhen6/ai-illustration-guide> | Figure design and visual consistency workflow for thesis diagrams. |

## Suggested Local Layout

After cloning this repository, clone the experiment repositories beside it or inside this directory:

```powershell
git clone https://github.com/wyhzhen6/MULTI-TALKER-SD.git code/MULTI-TALKER-SD
git clone https://github.com/wyhzhen6/reclustering.git code/reclustering
git clone https://github.com/wyhzhen6/ai-illustration-guide.git code/ai-illustration-guide
```

Large generated datasets, checkpoints, separated audio, and intermediate experiment outputs should not be committed directly. Use external storage or Git LFS when an artifact must be versioned.
