
```
\documentclass[12pt]{article}
\usepackage{graphicx} % for inserting figures
\usepackage[margin=2cm]{geometry} % for sensible margins
\usepackage{charter} % nice font
\usepackage[natbib=true, style=authoryear, uniquename=false, maxcitenames=2, mincitenames=1, uniquelist=false]{biblatex} % for references
\addbibresource{references.bib} % tell it the references file
\AtEveryBibitem{%
  \clearfield{month}
  \clearfield{url}
  \clearfield{urlyear}
  \clearfield{urlmonth}
  \clearfield{urlday}
  \clearfield{urlendyear}
  \clearfield{urlendmonth}
  \clearfield{urlendday}
  \clearfield{issn}
}

\usepackage{setspace} % for nice spacing
\doublespacing
\usepackage[hidelinks]{hyperref} % for links (to references mostly), [hidelinks] stops it drawing boxes around them but they're still clickable
% \usepackage{hyperref}
\usepackage{amsmath} % for maths
\usepackage{booktabs} % for nice lines on tables
\usepackage{subcaption} % for subfigures
\usepackage[table]{xcolor} % for colourful text
\usepackage{bm} % for bold maths
\usepackage{lineno} % for line numbers
\renewcommand\linenumberfont{\normalfont\normalsize} % makes line numbers a normal size not tiny
\linenumbers % actually adds the line numbers

```