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

## For Window with MikTeX
* MikTeX uses a `-enable-write18` instead of `--shell-escape`. So tell TikZ about it by adding `\tikzexternalize[shell escape=-enable-write18]`: 
```latex
\documentclass{article}
\usepackage{tikz}

% set up externalization
\usetikzlibrary{external}
\tikzset{external/system call={latex \tikzexternalcheckshellescape -halt-on-error
-interaction=batchmode -jobname "\image" "\texsource" && 
dvips -o "\image".ps "\image".dvi &&
ps2eps "\image.ps"}}
\tikzexternalize[shell escape=-enable-write18] % MikTeX uses a -enable-write18 instead of --shell-escape.

\begin{document}
\begin{tikzpicture}
\draw (0,0) circle (1cm);
\end{tikzpicture}
\end{document}
```
* Compile it with `latex -enable-write18` (not `pdflatex`!)

## Notes:
* If you want to run `pdflatex` and create an .eps file from the image, replace the `system call` by:
```latex
pdflatex \tikzexternalcheckshellescape -halt-on-error 
-interaction=batchmode -jobname "\image" "\texsource" && % or ;
pdftops -eps "\image".pdf
```

