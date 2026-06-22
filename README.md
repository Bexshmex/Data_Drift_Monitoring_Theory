# Automatic Monitoring of Data Drift and Model Performance

This repository contains a LaTeX bachelor thesis project about automatic monitoring of data drift and machine learning model performance in production systems.

The project is a document source repository. It does not contain a runnable software application. The main deliverable is the compiled thesis PDF, generated from `main.tex`.

## Project Contents

- `main.tex` - root LaTeX document. This file assembles the full thesis.
- `preamble.tex` - shared LaTeX configuration, packages, layout, fonts, hyperlinks, and bibliography setup.
- `Bibliography.bib` - bibliography database used by `biblatex` and `biber`.
- `frontmatter/` - title page, acknowledgement, Czech abstract, and English abstract.
- `chapters/` - thesis chapter source files.
- `Images/` - images used in the document, including title-page logos.
- `pdf/` - externally included PDF files, such as assignment and declaration pages.
- `main.pdf` - compiled PDF output.
- `PROJECT_MANUAL.md` - additional build and maintenance notes.

## Thesis Structure

The document currently consists of:

1. Front matter
   - title page
   - assignment PDF
   - declaration PDF
   - acknowledgement
   - Czech abstract
   - English abstract

2. Main matter
   - introduction
   - operational monitoring of machine learning models
   - data drift and drift detection methods
   - system requirements and architecture
   - implementation
   - evaluation
   - discussion
   - conclusion

3. Back matter
   - bibliography

## Current Chapter Status

The following chapter files contain thesis content:

- `chapters/mlops_monitoring.tex`
- `chapters/drift_theory.tex`
- `chapters/system-requirements-architecture.tex`

The following chapter files currently exist as placeholders and are empty:

- `chapters/implementation.tex`
- `chapters/evaluation.tex`
- `chapters/discussion.tex`
- `chapters/conclusion.tex`

The abstract files also still contain TODO comments.

## Required Tools

To build the thesis, install a LaTeX distribution that provides:

- `pdflatex`
- `biber`
- `latexmk`

On Windows, MiKTeX or TeX Live can be used.

## Build

From the project root, run:

```powershell
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

The compiled output is:

```text
main.pdf
```

Manual build sequence:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error main.tex
biber main
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

## Cleaning Generated Files

Remove temporary LaTeX build files:

```powershell
latexmk -c
```

Remove temporary files and the generated PDF:

```powershell
latexmk -C
```

## Notes

- Compile `main.tex`, not individual chapter files.
- `main.tex` includes external PDFs from the `pdf/` directory.
- Bibliography is configured in `preamble.tex` with `biblatex` and `biber`.
- The project currently keeps generated LaTeX files such as `.aux`, `.log`, `.toc`, and `main.pdf` in the working directory.
