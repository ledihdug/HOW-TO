# How to Export eps figures from TikZ
## For Linux, Mac OS with TeX Live (or MacTeX)
```latex
\documentclass{article}
\usepackage{tikz}

% set up externalization
\usetikzlibrary{external}
\tikzset{external/system call={latex \tikzexternalcheckshellescape -halt-on-error
-interaction=batchmode -jobname "\image" "\texsource";
dvips -o "\image".ps "\image".dvi;
ps2eps "\image.ps"}}
\tikzexternalize

\begin{document}
\begin{tikzpicture}
[some graphic]
\end{tikzpicture}
\end{document}
```
