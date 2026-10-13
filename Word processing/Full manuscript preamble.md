To set up a nice LaTeX document for a manuscript, there are some basic packages you'll need for things like maths, tables, references etc. This preamble is an example/template for a fairly standard manuscript. 
* First, it sets up the document with sensible margins and a nice (12pt) font. 
* Next, it deals with references. This uses biblatex and natbib (I'm not really sure how these two play together but this code seems to work nicely). The other arguments make sure that in-text references show a maximum of two author names before using 'et. al' and makes sure it doesn't do something weird if the first two authors and year are the same for multiple references. Then `\AtEveryBibitem` formats the reference list so it doesn't show any of this extra info.
* Sets it to be doublespaced.
* Adds clickable links to the pdf but doesn't show them with boxes/lines.
* Sets up maths.
* Deals with figures and tables.
* Line numbers.

```
\documentclass[12pt]{article}
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

\usepackage{amsmath} % for maths
\usepackage{bm} % for bold maths

\usepackage{graphicx} % for inserting figures
\usepackage{booktabs} % for nice lines on tables
\usepackage{subcaption} % for subfigures
\usepackage[table]{xcolor} % for colourful text (including in tables)

\usepackage{lineno} % for line numbers
\renewcommand\linenumberfont{\normalfont\normalsize} % makes line numbers a normal size not tiny
\linenumbers % actually adds the line numbers

```