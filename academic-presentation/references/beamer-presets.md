# Beamer presets

Use this file only when the task is on the Beamer path.

## Preset routing

Choose `conference preset` when the deck is primarily for speaking:
- conference
- finalist
- seminar
- defense
- timed talk
- Q&A
- speaker notes

Choose `literature review preset` when the deck is primarily for synthesis:
- literature review
- taxonomy
- classification
- comparison
- survey
- advisor review deck

If both sets appear, `conference preset` wins unless the user explicitly says to use literature-review style.

## Conference preset

### Baseline

- `\documentclass[aspectratio=169,10pt]{beamer}`
- `\usetheme{metropolis}`
- white background
- one restrained accent color
- visible but quiet page numbering
- citation footer kept light

### Typical title frame

```latex
\begin{frame}[plain,noframenumbering]
  % logos across the top
  % title + subtitle
  % authors / affiliation
  % optional short footer with email or repo
\end{frame}
```

### Typical content frame

```latex
\begin{frame}{Slide title}
\begin{columns}[T]
\begin{column}{0.52\textwidth}
  \begin{itemize}
    \item One idea per bullet
    \item Keep prose short
  \end{itemize}
\end{column}
\begin{column}{0.45\textwidth}
  \includegraphics[width=\linewidth]{figure.pdf}
\end{column}
\end{columns}
\end{frame}
```

### Strong patterns

- title page with logos and clean whitespace
- left text, right figure
- 2x2 image grid for setup or mode comparisons
- one results table or one results plot per slide
- bottom reference line instead of dense bibliographic block on content slides

## Literature review preset

### Baseline

- Beamer with clearer block structure than the conference preset
- stronger title-slide identity is acceptable
- content slides may use blocks, cards, and TikZ structure diagrams
- paper tags and class labels must stay consistent

### Typical taxonomy slide

```latex
\begin{frame}[t]{Classification mind map}
  \centering
  \begin{tikzpicture}[every node/.style={align=center}]
    % root card
    % left and right class cards
    % arrows
  \end{tikzpicture}
\end{frame}
```

### Typical comparison slide

```latex
\begin{frame}[t]{Cross-class comparison}
\begin{tabularx}{\textwidth}{>{\bfseries}p{3cm} X X}
\toprule
& Force-first & Compliance-first \\
\midrule
Primary target & ... & ... \\
Common backbone & ... & ... \\
\bottomrule
\end{tabularx}
\end{frame}
```

### Strong patterns

- split the field early
- show a method hierarchy before paper-by-paper detail
- use short blocks for representative anchors
- use dedicated reference slides when citations get dense
- keep review slides concise and structural rather than speech-like

## Common packages

```latex
\usepackage{amsmath,amssymb,bm}
\usepackage{graphicx,booktabs,colortbl,subcaption,tabularx,array}
\usepackage{tikz,hyperref}
```

Load `tabularx` and `array` when the review preset needs structured comparison tables.

## Common layout snippets

### 2x2 image grid

```latex
\includegraphics[width=0.47\linewidth]{a.pdf}\hfill
\includegraphics[width=0.47\linewidth]{b.pdf}\\[3pt]
\includegraphics[width=0.47\linewidth]{c.pdf}\hfill
\includegraphics[width=0.47\linewidth]{d.pdf}
```

### Highlighted table row

```latex
\definecolor{bestgreen}{RGB}{0,120,60}
\rowcolor{bestgreen!12}
\textbf{Best model} & \textbf{0.006} & ...
```

### Tight item spacing

```latex
\small
\begin{itemize}\setlength\itemsep{1pt}
  \item First point
  \item Second point
\end{itemize}
```

## Compile checklist

```bash
cd output_dir
pdflatex -interaction=nonstopmode presentation.tex
pdflatex -interaction=nonstopmode presentation.tex
```

After compile:
- inspect the log for `Error`
- inspect `Overfull` warnings that likely affect visible layout
- rasterize the PDF pages and review those images

## Portability checklist

- keep `.tex` beside the built PDF
- copy referenced figures into the output directory when portability matters
- remove fragile external `\graphicspath` dependencies once assets are localized
- keep the final submission filename aligned with the venue or user rule

## Known failure modes

| Issue | Fix |
|-------|-----|
| Duplicate page numbers with `metropolis` | Use `\setbeamertemplate{frame numbering}{...}` and do not add another footer counter |
| `\rowcolor` not working | Add `\usepackage{colortbl}` |
| Dense slide clips at bottom | Split the slide first; only then consider `[shrink=N]` |
| Title page overflows | Use `[plain,noframenumbering]` and reduce title-frame density |
| LaTeX control words leak into PDF text | Check braces, environments, and recently edited color or block commands |
| Adjacent slides repeat the same main image | Merge the point or change the visual role of one slide |
