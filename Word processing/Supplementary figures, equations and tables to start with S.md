If you're creating a Supplementary Information document in LaTeX, you can include these lines to make sure that all visual elements are numbered starting with an 'S'.

```
\renewcommand{\thefigure}{S\arabic{figure}}
\renewcommand{\theequation}{S\arabic{equation}}
\renewcommand{\thetable}{S\arabic{table}}
```