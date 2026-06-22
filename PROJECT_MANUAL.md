# Project Manual

This repository is a LaTeX bachelor thesis/report project. It does not contain a runnable Python application or web service. The main output is `main.pdf`, generated from `main.tex`.

## 1. Project Structure

- `main.tex` is the root LaTeX document. Compile this file, not the individual chapter files.
- `preamble.tex` contains document-wide packages, page layout, fonts, hyperlinks, and bibliography configuration.
- `frontmatter/` contains title page, acknowledgement, and Czech/English abstracts.
- `chapters/` contains the thesis chapters that are included from `main.tex`.
- `Images/` contains title-page logos.
- `pdf/` contains externally included PDF pages, currently `zadani_bk.pdf` and `prohlaseni.pdf`.
- `main.pdf` is the generated output file.

## 2. How the Document Is Assembled

`main.tex` performs the build in this order:

1. Loads the global setup from `preamble.tex`.
2. Starts the front matter with empty page style.
3. Inserts `frontmatter/titlepage.tex`.
4. Inserts external PDFs from `pdf/zadani_bk.pdf` and `pdf/prohlaseni.pdf`.
5. Inserts acknowledgement and abstracts.
6. Starts the main matter and table of contents.
7. Adds the introduction written directly inside `main.tex`.
8. Includes thesis chapters from `chapters/`.
9. Prints the bibliography through `biblatex`/`biber`.

The existing source currently contains two chapter files:

- `chapters/mlops_monitoring.tex`
- `chapters/drift_theory.tex`

## 3. Required Tools

Install a LaTeX distribution that includes:

- `pdflatex`
- `biber`
- `latexmk`

On Windows, MiKTeX works. If MiKTeX says it is a fresh installation, open MiKTeX Console once and finish setup/update checks, or allow the first command-line run to initialize MiKTeX.

## 4. Build Command

From the project root, run:

```powershell
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

The output is written to:

```text
main.pdf
```

Alternative manual build sequence:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error main.tex
biber main
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

## 5. Current Build Status

I tested the project locally on 2026-05-13.

The project currently generates `main.pdf`, but it is incomplete. `latexmk` finishes with a PDF output, but reports these missing inputs:

- `chapters/architecture.tex`
- `chapters/implementation.tex`
- `chapters/evaluation.tex`
- `chapters/discussion.tex`
- `chapters/conclusion.tex`
- `Bibliography.bib`

Biber fails directly because `Bibliography.bib` does not exist.

Because of these missing files, the generated PDF contains only the front matter, introduction, and the two available chapters. The bibliography is empty.

## 6. How to Add or Restore Chapters

Each `\include{chapters/name}` line in `main.tex` expects a matching file:

```text
chapters/name.tex
```

To complete the current chapter list, create or restore:

```text
chapters/architecture.tex
chapters/implementation.tex
chapters/evaluation.tex
chapters/discussion.tex
chapters/conclusion.tex
```

Each file should usually start with a chapter command, for example:

```latex
\chapter{Architecture}
\label{ch:architecture}
```

## 7. How to Add Bibliography

Create `Bibliography.bib` in the project root. Add BibTeX entries there, for example:

```bibtex
@book{example2024,
  author = {Example, Alice},
  title = {Example Book},
  year = {2024},
  publisher = {Example Publisher}
}
```

Then cite it in text:

```latex
\cite{example2024}
```

The project currently has `\nocite{*}` in `main.tex`, which prints every entry from `Bibliography.bib`. Remove that line later if you only want cited sources to appear.

## 8. Common Maintenance Tasks

Clean generated LaTeX build files:

```powershell
latexmk -c
```

Fully clean generated files, including the PDF:

```powershell
latexmk -C
```

Check the log for missing files or warnings:

```powershell
Select-String -Path main.log -Pattern "No file|Warning|Error|Undefined|Empty bibliography"
```

## 9. Known Content TODOs

- The introduction contains `This Bachelor's Degree Project consists of //(needs finishing)//`.
- `frontmatter/abstract_cz.tex` contains a TODO comment.
- `frontmatter/abstract_en.tex` contains a TODO comment.
- The five later chapter source files are missing.
- The bibliography database is missing.
