
This code should be added to the preamble of a LaTeX document. It will add continuous line numbers that are the same size as the text.

```
\usepackage{lineno} % for line numbers
\renewcommand\linenumberfont{\normalfont\normalsize} % makes line numbers a normal size not tiny
\linenumbers % actually adds the line numbers
```