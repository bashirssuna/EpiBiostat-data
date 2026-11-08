# Data for *Epidemiology and Biostatistics for Masters Students using R and STATA*

Revised Edition, by Dr. Bashir Ssuna (Makerere University School of Public Health;
Makerere Epidemiology and Statistical Center). Revised by Prof. Noah Kiwanuka, PhD
(Professor of Epidemiology and Biostatistics).

This repository holds the data for the book's worked examples: ten datasets in 17 files,
in the [`data`](data) folder. This page shows how to get the files and how to load each
one in STATA and in R.

## Two ways to use the data

- **Download once, work offline.** Download the files (Step 1) and load them from your
  own folder (Step 2). This suits a class, or a slow or costly connection.
- **Read from the internet.** Skip the download and read each file straight from this
  repository (Step 3). You need a connection each time you load a file.

The book's commands load each file from `D:/Statistics Book/book/data`, the folder on
the author's computer. Whichever way you choose, the only part of the book's code you
change is that folder.

## Step 1. Download the files

1. Open <https://github.com/bashirssuna/EpiBiostat-data>.
2. Click the green **Code** button, then **Download ZIP**.
3. Unzip the file (on Windows, right-click it and choose **Extract All**). You get a
   folder called `EpiBiostat-data-main`. Rename it `EpiBiostat-data` and move it to
   `C:/`, so that the data files sit in `C:/EpiBiostat-data/data`. Any other folder
   works too; use its path in Step 2.

To download a single file, open the `data` folder, click the file's name, then click
**Download raw file** (the downward arrow above the file, on the right).

## Step 2. Load a file from your folder

Replace the author's folder with yours:

```stata
* The book:
use "D:/Statistics Book/book/data/multiple_myeloma.dta", clear
* You:
use "C:/EpiBiostat-data/data/multiple_myeloma.dta", clear
```

Or tell the program where the files are, once per session, and then give the file name
alone:

```stata
cd "C:/EpiBiostat-data/data"
use multiple_myeloma.dta, clear
```

```r
setwd("C:/EpiBiostat-data/data")
d <- haven::read_dta("multiple_myeloma.dta")
```

Write paths with forward slashes (`/`), even on Windows: in R a single backslash inside
quotes causes an error. On a Mac the folder looks like
`/Users/yourname/EpiBiostat-data/data`.

## Step 3. Or read a file straight from the internet

Every file has its own web address: this folder address followed by the file name.

```text
https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data/
```

```stata
use "https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data/multiple_myeloma.dta", clear
```

```r
d <- haven::read_dta("https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data/multiple_myeloma.dta")
```

A web address cannot contain a space, so in an address write `Linear regression.dta` as
`Linear%20regression.dta`.

## Load commands for every file

Put the location in one place, then run the line for the data you need. Each STATA
command replaces the data in memory; each R command makes the data frame named on the
left.

**STATA** (version 14 or later)

```stata
* Run ONE of these two lines: your folder, or the internet
global bookdata "C:/EpiBiostat-data/data"
global bookdata "https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data"

import delimited "$bookdata/antibiotics.csv", clear
import delimited "$bookdata/its_lcg.csv", clear
use "$bookdata/Linear regression.dta", clear
label define Sex 1 "Female", modify
import delimited "$bookdata/wdbc.csv", clear
use "$bookdata/multiple_myeloma.dta", clear
use "$bookdata/pigs.dta", clear
use "$bookdata/piglong.dta", clear
use "$bookdata/cd4trial.dta", clear
use "$bookdata/schizo.dta", clear
use "$bookdata/muscatine.dta", clear
use "$bookdata/epilepsy.dta", clear
```

**R**

```r
# Run ONE of these two lines: your folder, or the internet
bookdata <- "C:/EpiBiostat-data/data"
bookdata <- "https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data"

# install.packages("haven")   # once, to read .dta files

d      <- read.csv(file.path(bookdata, "antibiotics.csv"))
d      <- read.csv(file.path(bookdata, "its_lcg.csv"))
d      <- haven::read_dta(file.path(bookdata, "Linear regression.dta"))
d$Sex  <- factor(d$Sex, levels = 1:2, labels = c("Female", "Male"))
wdbc   <- read.csv(file.path(bookdata, "wdbc.csv"))
d      <- haven::read_dta(file.path(bookdata, "multiple_myeloma.dta"))
pigs   <- read.csv(file.path(bookdata, "pigs.csv"))             # wide: one row per pig
wide   <- haven::read_dta(file.path(bookdata, "pigs.dta"))      # the same, wide
pigs   <- haven::read_dta(file.path(bookdata, "piglong.dta"))   # long: one row per pig-week
cd4    <- read.csv(file.path(bookdata, "cd4trial.csv"))
schizo <- read.csv(file.path(bookdata, "schizo.csv"))
musc   <- read.csv(file.path(bookdata, "muscatine.csv"))
epi    <- read.csv(file.path(bookdata, "epilepsy.csv"))
```

Notes on these commands:

- **From the internet, `Linear regression.dta` needs `%20`.** Write
  `"$bookdata/Linear%20regression.dta"` in STATA and
  `file.path(bookdata, "Linear%20regression.dta")` in R.
- **The `Sex` label.** In `Linear regression.dta` the value label for `Sex` = 1 is
  spelled `Femele`. The line after each load corrects it, as the book's code does.
- **Two formats, same values.** Where a dataset comes as both `.dta` and `.csv`, the two
  files hold the same values. The book's STATA code reads the `.dta` file. Its R code
  reads the `.csv` file, except for the myeloma data, and the wide pig weights in
  Sections 9.3 and 9.8, which it reads from the `.dta` file.
- **`haven`.** R reads `.dta` files with the `haven` package. Some chapters run
  `library(haven)` first and then write `read_dta(...)` without `haven::`; both forms do
  the same thing.

These commands were tested with Stata/MP 17 and R 4.5.2 on Windows, from a local folder
and from the internet.

## The files

| File | What it holds | Size | Used in | Source |
|---|---|---|---|---|
| `antibiotics.csv` | The author's trial of prophylactic antibiotics against none | 260 patients | Section 5.5 | The author's own trial; only the allocated arm and the outcome are kept |
| `its_lcg.csv` | A monthly interrupted time series | 48 months | Section 5.6 | Simulated for the book (not a hospital's data) |
| `Linear regression.dta` | Forced expiratory volume and its predictors | 60 adults | Section 7.1 | The author's teaching dataset |
| `wdbc.csv` | Wisconsin breast tumours: 30 measurements of the cell nuclei | 569 tumours | Sections 7.3, 10.1, 10.2 | Street WN, Wolberg WH, Mangasarian OL. Nuclear feature extraction for breast tumor diagnosis. Proc SPIE. 1993;1905:861-870 (UCI Machine Learning Repository) |
| `multiple_myeloma.dta`, `multiple_myeloma.csv` | Survival of patients with multiple myeloma; `sex` 1 female, 2 male; `bj` (Bence-Jones protein) 0 no, 1 yes | 48 patients | Chapter 8 | Krall JM, Uthoff VA, Harley JB. A step-up procedure for selecting variables associated with survival. Biometrics. 1975;31(1):49-57 |
| `pigs.dta`, `pigs.csv`, `piglong.dta` | Weekly weights of pigs over nine weeks, wide and long | 48 pigs (432 rows long) | Sections 9.1, 9.3, 9.4, 9.8 | Diggle PJ, Heagerty P, Liang KY, Zeger SL. Analysis of Longitudinal Data. 2nd ed. Oxford University Press; 2002 |
| `cd4trial.dta`, `cd4trial.csv` | AIDS trial: log CD4 counts at up to six visits | 1308 patients, 4391 visits | Sections 9.1, 9.2, 9.4 | Henry K, Erice A, Tierney C, et al. J Acquir Immune Defic Syndr Hum Retrovirol (ACTG 193A trial) |
| `schizo.dta`, `schizo.csv` | Schizophrenia trial: weekly severity of illness | 437 patients, 1603 ratings | Sections 9.6, 9.7 | Hedeker D, Gibbons RD. Longitudinal Data Analysis. Wiley; 2006 (written from the R package `lme4`, `schizophrenia`) |
| `muscatine.dta`, `muscatine.csv` | Obesity in schoolchildren at three surveys | 4856 children, 14,568 rows | Section 9.6 | Woolson RF, Clarke WR. J R Stat Soc A. 1984;147(1):87-99 (written from the R package `geepack`) |
| `epilepsy.dta`, `epilepsy.csv` | Seizure counts in a trial of progabide | 59 patients, 295 rows | Sections 9.6, 9.7 | Thall PF, Vail SC. Biometrics. 1990;46(3):657-671; Leppik IE, et al. Neurology. 1987;37(6):963-968 |

Appendix B of the book describes every variable.

## Data the software fetches itself

Some examples use data that come with STATA or R, so they are not in this repository.
Appendix B, Section B.2 of the book describes them.

- **STATA:** `sysuse auto`, installed with STATA, and the Stata Press example datasets
  that `webuse` downloads: `catheter`, `diet`, `dollhill3`, `epilepsy`, `fuel`, `hanley`,
  `iris`, `lbw`, `rate2` and `stan3`. `webuse` needs an internet connection.
- **R:** `iris`, `mtcars`, `PlantGrowth` and `sleep`, which come with R, and three
  datasets in packages: `birthwt` in `MASS`, which comes with R, and `popmis` in `mice`
  and `api` in `survey`, which you install once with
  `install.packages(c("mice", "survey"))`.

## When a file will not load

- **STATA says `file ... not found`.** Check the folder in the path; `pwd` shows the
  folder STATA is working in. Keep the quotation marks around
  `"Linear regression.dta"`, whose name has a space.
- **R says `cannot open file` or `does not exist`.** Check the folder; `getwd()` shows
  R's working folder. Use forward slashes.
- **R says `there is no package called 'haven'`.** Run `install.packages("haven")` once.
- **An old STATA refuses a `.dta` file.** The `.dta` files need STATA 14 or later. With
  an older STATA, load the `.csv` file where there is one.
- **Reading from the internet fails.** Check the connection, and spell the file name
  exactly, capitals included. Some institutional networks block such downloads; if
  yours does, download the files (Step 1) and load them from your folder.

## Citing and using the data

These files are shared for learning with the book. Please cite the book, and the
original source listed above when you use a published dataset; the published datasets
remain subject to their original sources' terms.

Stata and Stata Press are registered trademarks of StataCorp LLC. R is free software
from the R Foundation for Statistical Computing. This repository and the book are
independent and are not endorsed by StataCorp LLC or the R Foundation.
