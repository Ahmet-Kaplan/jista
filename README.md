# JISTA LaTeX Template

LaTeX template for the **Journal of Intelligent Systems: Theory and Applications (JISTA)**, converted from the official Word preparation template.

**Journal:** https://dergipark.org.tr/en/pub/jista

## Requirements

- **XeLaTeX** (included in TeX Live 2022+ or MacTeX)
- **Biber** (included with TeX Live / MacTeX)
- **Times New Roman** font (pre-installed on macOS and Windows; on Linux install via `ttf-mscorefonts-installer`)

## Repository Structure

```
.
├── jista_template.tex   # Main LaTeX template — edit this for your article
├── references.bib       # BibTeX bibliography entries
├── figures/             # Place all figure files here (PDF, PNG, JPG)
│   └── .gitkeep
├── .gitignore           # Excludes LaTeX build artifacts
└── README.md            # This file
```

## Quick Start

1. Copy `jista_template.tex` and `references.bib` to your working directory (or work directly in this repo).
2. Fill in your title, authors, affiliations, and abstract (see [Title Block](#title-block)).
3. Write your body sections.
4. Place figure files in `figures/`.
5. Add references to `references.bib`.
6. Compile (see [Compilation](#compilation)).

## Template Specifications

| Property | Value |
|---|---|
| Paper size | A4 (210 × 297 mm) |
| Margins | Top 3 cm · Bottom 2.5 cm · Left 2 cm · Right 2 cm |
| Body font | Times New Roman 10 pt, single spacing |
| Layout | Two-column |
| Citation style | Harvard author-date (`biblatex` + Biber) |

## Title Block

The full-width title block at the top of `jista_template.tex` contains:

- **English title** — 18 pt, bold
- **Authors** — 11 pt (revealed after acceptance; placeholder provided)
- **Affiliations** — 9 pt, italic (commented out by default, uncomment to use)
- **English abstract** — 9 pt, 70–250 words, followed by keywords
- **Turkish title** — 14 pt, bold
- **Turkish abstract (Öz)** — 9 pt, followed by Turkish keywords

```latex
% English title
{\fontsize{18}{27}\selectfont\bfseries Your Paper Title Here\par}

% Authors
{\fontsize{11}{13}\selectfont First Author$^1$, Second Author$^2$\par}

% Affiliations (uncomment)
% {\fontsize{9}{11}\selectfont\itshape
%   $^1$Department, Institution, City, Country\par}
```

## Sections and Subsections

```latex
\section{Introduction}
Body text in Times New Roman 10 pt.

\subsection{Your Subsection \normalfont\textit{(Turkish Title)}}
Subsection text.
```

| Element | Size | Style | Before / After |
|---|---|---|---|
| Section heading | 12 pt | Bold | 12 pt / 6 pt |
| Subsection heading | 11 pt | Italic | 12 pt / 6 pt |
| Body text | 10 pt | Regular | — |

## Figures

Place image files in the `figures/` folder. The preamble already sets `\graphicspath{{figures/}}`.

**Single-column figure:**
```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=\linewidth]{my_plot.pdf}
  \caption{Figure caption \textit{(English caption)}}
  \label{fig:my_plot}
\end{figure}
```

**Two-column (wide) figure:**
```latex
\begin{figure*}[htbp]
  \centering
  \includegraphics[width=\textwidth]{wide_diagram.pdf}
  \caption{Wide figure caption \textit{(English caption)}}
  \label{fig:wide}
\end{figure*}
```

- Caption: 9 pt, label bold, positioned **below** the figure
- Spacing: 6 pt above caption · 12 pt below caption
- Cross-reference in text: `Figure~\ref{fig:my_plot}`
- Preferred format: **PDF** (vector), then PNG/JPG (raster ≥ 300 dpi)

## Tables

**Single-column table:**
```latex
\begin{table}[htbp]
  \caption{Table title \textit{(English title)}}
  \label{tab:results}
  \centering
  \fontsize{9}{11}\selectfont
  \begin{tabular}{lcc}
    \toprule
    Method  & Accuracy & F1 \\
    \midrule
    Model A & 92.1\%   & 0.91 \\
    Model B & 94.3\%   & 0.93 \\
    \bottomrule
  \end{tabular}
\end{table}
```

**Two-column (wide) table:**
```latex
\begin{table*}[htbp]
  \caption{Wide table title}
  \centering
  \fontsize{9}{11}\selectfont
  \begin{tabular}{lccccc}
    \toprule
    ...
    \bottomrule
  \end{tabular}
\end{table*}
```

- Caption: 9 pt, label bold, positioned **above** the table
- Spacing: 12 pt above caption · 3 pt below caption
- Cross-reference in text: `Table~\ref{tab:results}`

## Equations

```latex
\begin{equation}
  \label{eq:example}
  a = b + c
\end{equation}
```

- Numbered consecutively in parentheses, right-aligned (LaTeX default)
- Leave a blank line before and after each equation block
- Reference in text: `\eqref{eq:example}` → (1)

## Citations and References

Add entries to `references.bib` using standard BibTeX:

```bibtex
@article{Smith2023,
  author  = {Smith, J. and Doe, A.},
  year    = {2023},
  title   = {Paper title},
  journal = {Journal Name},
  volume  = {10},
  pages   = {1--15},
}
```

| Command | Output |
|---|---|
| `\parencite{Smith2023}` | (Smith and Doe, 2023) |
| `\textcite{Smith2023}` | Smith and Doe (2023) |

References are printed automatically at the end via `\printbibliography`.
Style: Harvard author-date · 9 pt · 0.5 cm hanging indent.

## Compilation

Run the full build sequence (required when adding new citations):

```bash
xelatex -interaction=nonstopmode jista_template.tex
biber jista_template
xelatex -interaction=nonstopmode jista_template.tex
xelatex -interaction=nonstopmode jista_template.tex
```

For text-only edits (no new citations), a single `xelatex` pass is sufficient.

## Special Sections

These sections are **unnumbered** and use `\section*{}`:

```latex
\section*{Acknowledgment}
Funding sources and supporters.

\section*{Appendix}
Additional material (immediately after References, no new page).
```

## Tracking the PDF in Git

By default, `*.pdf` is excluded via `.gitignore`. To track the compiled PDF, remove or comment out that line:

```gitignore
# *.pdf   ← comment this out to track PDFs
```

## License

Template structure derived from the official JISTA Word preparation template.
