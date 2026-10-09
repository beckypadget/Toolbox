The worst part about writing papers in LaTeX is the conversion that must happen in order for publications to accept it. One thing that is a bit of a faff is creating a tracked changes version of the manuscript for revisions as Overleaf doesn't do this automatically (you can track code changes in Overleaf but the pdf will never show the changes). Instead, what you can do is get your original file (either by creating a whole new document for resubmission or going to the version history in Overleaf) and your new file and then creating a new version that shows the changes. 

---
To use:
1. Download both `main.tex` files, name them something different and put them in the same folder.
2. cd into the folder.
3. Run the code below. This takes your `old.tex` file and compares it to your `new.tex` file and outputs `diff.tex`, which will show bold text where additions have been made.

```
latexdiff --type=BOLD old.tex new.tex > diff.tex
```

There are different options for `type`, I think it is possible to use highlighting etc. Beware, using bold will mean that line numbering doesn't match between the clean and the tracked changes version.