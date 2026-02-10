# LaTeX Templates for ArXiv Papers

Reusable snippets for Phase 3 (Generate). Assemble the final `main.tex` from these building blocks.

---

## Document Preamble

```latex
\documentclass[11pt,a4paper]{article}

% Encoding
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}

% Math
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{amsfonts}

% Figures and graphics
\usepackage{graphicx}
\usepackage{float}

% Tables
\usepackage{booktabs}
\usepackage{array}
\usepackage{multirow}
\usepackage{longtable}
\usepackage{tabularx}

% Layout
\usepackage[margin=1in]{geometry}
\usepackage{setspace}

% Typography
\usepackage{microtype}

% Colors (if needed)
\usepackage{xcolor}

% Lists
\usepackage{enumitem}

% Algorithms (include only if paper has algorithms)
% \usepackage{algorithm}
% \usepackage{algorithmic}

% Citations
\usepackage{natbib}
\bibliographystyle{plainnat}

% Hyperlinks (load last)
\usepackage[colorlinks=true,linkcolor=blue,citecolor=blue,urlcolor=blue]{hyperref}
```

---

## Title Block

```latex
\title{Paper Title Here}

\author{
  First Author\thanks{Corresponding author: \texttt{email@institution.edu}} \\
  \textit{Department, Institution} \\
  \textit{City, Country}
  \and
  Second Author \\
  \textit{Department, Institution} \\
  \textit{City, Country}
  \and
  Third Author \\
  \textit{Department, Institution} \\
  \textit{City, Country}
}

\date{}  % Leave empty for arxiv submissions

\begin{document}
\maketitle
```

### Single-affiliation variant (all authors at one institution)

```latex
\title{Paper Title Here}

\author{
  First Author\thanks{Corresponding author: \texttt{email@institution.edu}},
  Second Author,
  Third Author \\
  \\
  \textit{Department Name} \\
  \textit{Institution Name} \\
  \textit{City, Country}
}

\date{}
```

---

## Abstract

```latex
\begin{abstract}
Your abstract text here. Should be 150--300 words. Summarize the problem,
your approach, key results, and significance. No citations, equations,
or references to figures/tables.
\end{abstract}

\textbf{Keywords:} keyword one, keyword two, keyword three, keyword four
```

---

## Sections

```latex
\section{Introduction}
\label{sec:introduction}

\section{Related Work}
\label{sec:related-work}

\section{Methods}
\label{sec:methods}

\subsection{Subsection Title}
\label{sec:methods-subsection}

\subsubsection{Sub-subsection Title}
\label{sec:methods-subsubsection}

\section{Experiments}
\label{sec:experiments}

\section{Results}
\label{sec:results}

\section{Discussion}
\label{sec:discussion}

\section{Conclusion}
\label{sec:conclusion}
```

---

## Tables

### Simple table

```latex
\begin{table}[htbp]
  \centering
  \caption{Description of the table.}
  \label{tab:example}
  \begin{tabular}{lcc}
    \toprule
    \textbf{Method} & \textbf{Accuracy (\%)} & \textbf{F1 Score} \\
    \midrule
    Baseline         & 78.3 & 0.76 \\
    Our method       & \textbf{85.1} & \textbf{0.83} \\
    \bottomrule
  \end{tabular}
\end{table}
```

### Multi-column table

```latex
\begin{table}[htbp]
  \centering
  \caption{Results across datasets.}
  \label{tab:multi}
  \begin{tabular}{l*{4}{c}}
    \toprule
    & \multicolumn{2}{c}{\textbf{Dataset A}} & \multicolumn{2}{c}{\textbf{Dataset B}} \\
    \cmidrule(lr){2-3} \cmidrule(lr){4-5}
    \textbf{Method} & Precision & Recall & Precision & Recall \\
    \midrule
    Method 1 & 0.85 & 0.79 & 0.82 & 0.77 \\
    Method 2 & 0.88 & 0.83 & 0.86 & 0.81 \\
    \bottomrule
  \end{tabular}
\end{table}
```

### Long table (spans pages)

```latex
\begin{longtable}{lp{8cm}c}
  \caption{Extended results table.}
  \label{tab:long} \\
  \toprule
  \textbf{ID} & \textbf{Description} & \textbf{Value} \\
  \midrule
  \endfirsthead
  \multicolumn{3}{c}{\tablename\ \thetable\ -- continued from previous page} \\
  \toprule
  \textbf{ID} & \textbf{Description} & \textbf{Value} \\
  \midrule
  \endhead
  \midrule
  \multicolumn{3}{r}{Continued on next page} \\
  \endfoot
  \bottomrule
  \endlastfoot
  1 & First item description & 42 \\
  2 & Second item description & 37 \\
  % ... more rows
\end{longtable}
```

---

## Figures

### Single figure

```latex
\begin{figure}[htbp]
  \centering
  % Upload this image to Prism as figures/fig1.png
  \includegraphics[width=0.8\textwidth]{figures/fig1.png}
  \caption{Description of what this figure shows.}
  \label{fig:example}
\end{figure}
```

### Side-by-side figures

```latex
\begin{figure}[htbp]
  \centering
  \begin{minipage}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{figures/fig2a.png}
    \subcaption{Left panel description.}
    \label{fig:left}
  \end{minipage}
  \hfill
  \begin{minipage}[b]{0.48\textwidth}
    \centering
    \includegraphics[width=\textwidth]{figures/fig2b.png}
    \subcaption{Right panel description.}
    \label{fig:right}
  \end{minipage}
  \caption{Overall figure description.}
  \label{fig:sidebyside}
\end{figure}
```

**Note:** Add `\usepackage{subcaption}` to the preamble when using subfigures.

### Figure placeholder (when image is not yet available)

```latex
\begin{figure}[htbp]
  \centering
  \fbox{\parbox{0.8\textwidth}{\centering\vspace{3cm}
    [Figure placeholder: Description of what should appear here]
  \vspace{3cm}}}
  \caption{Description of the figure.}
  \label{fig:placeholder}
\end{figure}
```

---

## Math

### Numbered equation

```latex
\begin{equation}
  \label{eq:loss}
  \mathcal{L} = -\sum_{i=1}^{N} y_i \log(\hat{y}_i)
\end{equation}
```

### Multi-line aligned equations

```latex
\begin{align}
  f(x) &= ax^2 + bx + c \label{eq:quadratic} \\
  g(x) &= \frac{df}{dx} = 2ax + b \label{eq:derivative}
\end{align}
```

### Unnumbered equation

```latex
\[
  E = mc^2
\]
```

---

## Bibliography (Inline — Prism-friendly)

```latex
\begin{thebibliography}{99}

\bibitem{AuthorYear}
Author, A., Author, B., and Author, C. (2024).
\newblock Title of the paper.
\newblock \textit{Journal or Conference Name}, volume(issue):pages.

\bibitem{AuthorYear2}
Author, D. and Author, E. (2023).
\newblock Another paper title.
\newblock In \textit{Proceedings of Conference}, pages 1--10.

\bibitem{AuthorYear3}
Author, F. (2022).
\newblock A book title.
\newblock Publisher Name, City.

\end{thebibliography}
```

**Important:** Use `\begin{thebibliography}` instead of `\bibliography{file.bib}` so the document is self-contained and compiles in Prism without needing a separate .bib file.

---

## Acknowledgments

```latex
\section*{Acknowledgments}
The authors would like to thank [names] for helpful discussions.
This work was supported by [funding agency] under grant [number].
```

---

## Appendices

```latex
\appendix

\section{Supplementary Material}
\label{app:supplementary}

Additional content here.

\section{Proof of Theorem~\ref{thm:main}}
\label{app:proof}

Detailed proof here.
```

---

## URL Overflow Prevention

Always load `url` with hyphens **before** `hyperref`, and wrap the bibliography in `{\sloppy ... }`:

```latex
% In preamble — BEFORE hyperref
\usepackage[hyphens]{url}
\usepackage[colorlinks=true,linkcolor=blue,citecolor=blue,urlcolor=blue,breaklinks=true]{hyperref}

% Around bibliography
{\sloppy
\begin{thebibliography}{100}
...
\end{thebibliography}
}% end sloppy
```

---

## How to Cite This Publication

Always include this section after the bibliography. Provide both a plain-text citation and a BibTeX entry.

```latex
\section*{How to Cite This Publication}

\begin{quote}
LastName, F., LastName, F., and LastName, F. (Year). \textit{Paper Title}. Institution. Month Day, Year.
\end{quote}

\noindent BibTeX:
\begin{verbatim}
@techreport{key,
  author      = {LastName, FirstName and LastName, FirstName},
  title       = {Paper Title},
  institution = {Institution Name},
  year        = {Year},
  month       = {Month},
  url         = {https://...}
}
\end{verbatim}
```

---

## Complete Document Skeleton

```latex
\documentclass[11pt,a4paper]{article}

% --- Packages (include only what's needed) ---
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage[margin=1in]{geometry}
\usepackage{microtype}
\usepackage{natbib}
\usepackage[colorlinks=true,linkcolor=blue,citecolor=blue,urlcolor=blue]{hyperref}

% --- Document ---
\title{Your Paper Title}
\author{
  Author One\thanks{Corresponding author: \texttt{author@email.com}} \\
  \textit{Institution One}
  \and
  Author Two \\
  \textit{Institution Two}
}
\date{}

\begin{document}
\maketitle

\begin{abstract}
Your abstract here (150--300 words).
\end{abstract}

\textbf{Keywords:} keyword1, keyword2, keyword3

\section{Introduction}
\label{sec:intro}

\section{Related Work}
\label{sec:related}

\section{Methods}
\label{sec:methods}

\section{Experiments}
\label{sec:experiments}

\section{Results}
\label{sec:results}

\section{Conclusion}
\label{sec:conclusion}

\section*{Acknowledgments}
We thank...

\begin{thebibliography}{99}
\bibitem{ref1}
Author, A. (2024). Title. \textit{Journal}, 1(1):1--10.
\end{thebibliography}

\end{document}
```
