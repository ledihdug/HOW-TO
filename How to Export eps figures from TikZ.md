# How to Export eps figures from TikZ
## For Linux, Mac OS with TeX Live (or MacTeX)
* Setup tikz externalization as following: 
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
* Run file with `latex --shell-escape filename.tex` (not `pdflatex!`) in command line.
## For Windows with TeX Live
* There is a small change should be noticed in the system call definition. The `;` has to be changed to `&&` as following:
```latex
\documentclass{article}
\usepackage{tikz}

% set up externalization
\usetikzlibrary{external}
\tikzset{external/system call={latex \tikzexternalcheckshellescape -halt-on-error
-interaction=batchmode -jobname "\image" "\texsource" &&
dvips -o "\image".ps "\image".dvi &&
ps2eps "\image.ps"}}
\tikzexternalize

\begin{document}
\begin{tikzpicture}
[some graphic]
\end{tikzpicture}
\end{document}
```
* Compile it with `latex --shell-escape filename.tex`
