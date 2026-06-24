# How to Redo This Work

This document describes the intended reproduction path for the thesis.

## 1. Rebuild the Thesis PDF

The LaTeX source is archived in:

```text
thesis/thesis_ntu.zip
```

Extract the archive first, then build from the extracted LaTeX project:

```powershell
cd <extracted-thesis-folder>
pdflatex -interaction=nonstopmode mythesis.tex
bibtex mythesis
pdflatex -interaction=nonstopmode mythesis.tex
pdflatex -interaction=nonstopmode mythesis.tex
```

Current note: `bibtex mythesis` reports duplicated keys in `References/first_paper.bib`. Clean the duplicate entries before using the PDF as the final archival version.

## 2. Recreate Multi-Talker-SD

Use the dataset/code repository:

<https://github.com/wyhzhen6/MULTI-TALKER-SD>

High-level steps:

1. Create the Python environment described by the repository.
2. Download LibriSpeech and AISHELL-1.
3. Download the point-source and diffuse-field noise resources listed in that repository.
4. Configure `config/config.yaml`.
5. Run the generation script to produce synthetic meeting audio, RTTM/UEM labels, and metadata.

The generated benchmark is used for high-density speaker-count, overlap-ratio, bilingual-composition, and meeting-type analysis.

## 3. Rerun Clustering-Based Separation Experiments

Use the repository for the speech-separation trade-off paper:

<https://github.com/wyhzhen6/reclustering>

Expected experiment flow:

1. Prepare the diarization baseline.
2. Prepare separated speech outputs from the configured separation models.
3. Run clustering-based diarization with and without separation.
4. Compare DER, missed speech, false alarm, and speaker confusion.
5. Analyze embedding displacement and t-SNE visualizations.
6. Regenerate the Chapter 4 figures.

## 4. Regenerate Thesis Figures

Thesis figures are stored inside:

```text
thesis/thesis_ntu.zip
```

Slide-oriented generated images are stored in:

```text
slides/slide_assets/generated
```

The figure design workflow is documented in:

<https://github.com/wyhzhen6/ai-illustration-guide>

## 5. Update the Thesis

After rerunning experiments:

1. Update the result tables and figures in `thesis/latex/Chapters`.
2. Replace stale files under `thesis/latex/Figures`.
3. Recompile the thesis PDF.
4. Copy the new PDF to `thesis/thesis.pdf`.

## 6. Publish on GitHub

Suggested commands after creating the remote repository:

```powershell
git init
git add .
git commit -m "Initial thesis homepage"
git branch -M main
git remote add origin https://github.com/wyhzhen6/<new-repo-name>.git
git push -u origin main
```

Then add The Anh:

- Personal repository: Settings -> Collaborators -> invite The Anh -> set permission to Admin.
- Organization repository: add both maintainers through the organization team or repository access settings.
