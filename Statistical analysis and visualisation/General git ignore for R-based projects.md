R likes to create many additional files but you probably just need the code files gitted. Also you might not want to git figures or the html files created when using notebooks. This gitignore template stops all of these things being gitted so you've got a nice clean repository and can find your code quickly.

```
*.Rproj.user
*.Rproj
*.Rhistory
*.RData
*.Ruserdata
*.png
*.html
*.csv
*.key
```