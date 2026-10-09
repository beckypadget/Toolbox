biblatex offers more customisability than just natbib so it's useful to use that. 
* The `\AtEveryBibitem` line and the `\clearfield` commands remove fields from the reference list because it adds too much information. 

```
\usepackage[natbib=true, 
			style=authoryear, 
			uniquename=false, % stops it adding extra names 
			maxcitenames=2, 
			mincitenames=1, 
			uniquelist=false]{biblatex} % for references
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
```

```
\printbibliography
```