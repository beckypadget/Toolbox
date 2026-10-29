R likes to create many additional files but you probably just need the code files gitted. Also you might not want to git figures or the html files created when using notebooks. This gitignore template stops all of these things being gitted so you've got a nice clean repository and can find your code quickly.

This gitignore ignores any files that R generates automatically (including html previews of R markdown notebooks), images, documents, datafiles and keynote or powerpoints.

```
*.Rproj.user
*.Rproj
*.Rhistory
*.RData
*.Ruserdata
*.png
*.jpeg
*.jpg
*.pdf
*.html
*.csv
*.key
*.ppt
```