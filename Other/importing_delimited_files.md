---
title: Import a Delimited Data File (CSV, TSV)
parent: Other
has_children: false
nav_order: 1
mathjax: false ## Switch to false if this page has no equations or other math rendering.
---

# Import a Delimited Data File (CSV, TSV)

Often, data is stored in [delimited files](https://en.wikipedia.org/wiki/Delimiter-separated_values). In delimited files, each record has its own line, but the columns or variables are separated by a character, or delimiter. The most common delimiter used is a comma. As a result, you will often encounter comma-delimited files by their more common name, comma-separated values or CSV files. Importing these files is often the first step of any data analysis project, so we show you how to import CSVs (and other delimited files) below. 

## Keep in Mind

- Sometimes delimiting characters also appear in strings in the data - this can cause your program to read the data improperly since it assumes that a new column is starting every time it sees that character. Good data stewards won't let this happen, but when it does happen it can be a real headache. Be on the lookout for that if your data seems to be reading in improperly. 
- When starting out, it can be confusing to know that you are working with a CSV file because you can open CSVs in Excel and they look like normal spreadsheets. Because many software packages have different procedures for importing CSVs and Excel workbooks, the ability to open CSVs in Excel (and the fact that they often appear in your GUI with an Excel icon next to them because that is the default program used to open them) often leads users to want to use the import commands appropriate for Excel. Don't be caught up by this pitfall; the failsafe way to look at the extension connected with your file name. CSV files will have a .csv extension, while Excel files end in .xls or .xlsx
- Other common delimiters include tabs (TSV) and pipes: |. 
- Before doing this you will probably find it useful to [Set a Working Directory]({{ "/Other/set_a_working_directory.html" | relative_url }})



# Implementations

## Julia

```julia?skip=true&skipReason=local_file
import Pkg; Pkg.add("CSV") # This line and the next add the packages CSV and DataFrames to your Julia installation
Pkg.add("DataFrames") # They need to only be run once and not at all if you have previously installed the packages

# Initialize the CSV and DataFrames packages (import also works in place of using, to make the analogy to Python's import more direct)
using CSV, DataFrames

# Import a CSV File from your local computer, if Scorecard.csv is in your working directory
df = CSV.read("Scorecard.csv", DataFrame) # Note, the DataFrame argument tells Julia to read the dataset into a DataFrame object

# Read a CSV File from the web 
using HTTP # Bring in Julia's HTTP package to pull from the web
df_web = CSV.read(HTTP.get("https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv").body, DataFrame)
```

## Python

The approach in Python uses pandas's read_csv function and looks quite similar to Julia's syntax. 

```python?skip=true&skipReason=local_file
# Import a CSV File from your local machine
df = pd.read_csv("Scorecard.csv")

# Import a CSV File from the web 
import pandas as pd # Make pandas available to your Python session 

df = pd.read_csv("https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv")
```

## R

```r?skip=true&skipReason=local_file
# Import a CSV file with the base-R (utils package) read.csv function
df <- read.csv('Scorecard.csv')

# If you are working in the tidyverse, there is the improved read_csv
library(tidyverse)
df <- read_csv('Scorecard.csv')

# The fastest way to read in large CSV files is fread() in the data.table package
library(data.table)
df <- fread('Scorecard.csv')

# In each of these cases you can open a CSV on the internet by just putting the URL in place of the file path
df <- read.csv('https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv')
df <- read_csv('https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv')
df <- fread('https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv')
```


## Stata

```stata?skip=true&skipReason=local_file
* Import a CSV File from your local machine
import delimited Scorecard.csv, clear 
* Note that the ", clear" option on all Stata import commands clears any data in memory before importing the dataset

* Import a CSV File from the web 
import delimited "https://github.com/LOST-STATS/lost-stats.github.io/raw/source/Model_Estimation/Data/Fixed_Effects_in_Linear_Regression/Scorecard.csv", clear 
```
