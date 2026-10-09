Running (e.g., agent-based) models often results in many outputted files that ultimately need to be combined. There are many ways to do this in R or Python for example, but this is a nice, quick way to do it that doesn't require the files to be imported anywhere (which could take a while if you've got a lot).

---
To use:
1. Make sure all data files are in one folder; the first row of each data file should be identical and it should be the headers for the columns (i.e., all data files should be in exactly the same format).
2. cd into the folder
3. Run this code to combine all csv files in the folder into one

```
awk '(NR == 1) || (FNR > 1)' *.csv > combined_data.csv
```

There are different ways to specify which files you want. `*.csv` gets all files ending with `.csv`. If you were to use `data_*` instead, this would get all files beginning with `data_`. 