# Data for *Epidemiology and Biostatistics for Masters Students using R and STATA*

Revised Edition, by Dr. Bashir Ssuna (Makerere University School of Public Health;
Makerere Epidemiology and Statistical Center). Revised by Prof. Noah Kiwanuka, PhD.

This repository holds the data files that the book's worked examples load from disk:
ten datasets in 17 files, in the `data` folder.

## Getting the data

1. On this page choose **Code**, then **Download ZIP**, and unzip it into a folder of
   your own, for example `C:/EpiBiostat-data`.
2. The book's code reads each file from the folder `D:/Statistics Book/book/data` on
   the author's computer. Replace that part of the path with your own folder:

   ```stata
   use "C:/EpiBiostat-data/data/multiple_myeloma.dta", clear
   ```

   ```r
   d <- haven::read_dta("C:/EpiBiostat-data/data/multiple_myeloma.dta")
   ```

   Or set your folder once at the start of a session (`cd` in STATA, `setwd()` in R)
   and use the file name alone.
3. You can also read a file straight from the internet:

   ```stata
   use "https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data/multiple_myeloma.dta", clear
   ```

   ```r
   d <- haven::read_dta("https://raw.githubusercontent.com/bashirssuna/EpiBiostat-data/main/data/multiple_myeloma.dta")
   ```

Where a dataset comes in both formats, the book's STATA code reads the `.dta` file and
its R code reads the `.csv` file (the two hold the same values); the myeloma data are the
one exception, which R also reads from the `.dta` file with the `haven` package.

## The files

| File | What it holds | Size | Used in | Source |
|---|---|---|---|---|
| `antibiotics.csv` | The author's trial of prophylactic antibiotics against none | 260 patients | Section 5.5 | The author's own trial; only the allocated arm and the outcome are kept |
| `its_lcg.csv` | A monthly interrupted time series | 48 months | Section 5.6 | Simulated for the book (not a hospital's data) |
| `Linear regression.dta` | Forced expiratory volume and its predictors | 60 adults | Section 7.1 | The author's teaching dataset. The value label for `Sex` = 1 is spelled `Femele` in the file; the book's code corrects it as it loads the data |
| `wdbc.csv` | Wisconsin breast tumours: 30 measurements of the cell nuclei | 569 tumours | Sections 7.3, 10.1, 10.2 | Street WN, Wolberg WH, Mangasarian OL. Nuclear feature extraction for breast tumor diagnosis. Proc SPIE. 1993;1905:861-870 (UCI Machine Learning Repository) |
| `multiple_myeloma.dta`, `multiple_myeloma.csv` | Survival of patients with multiple myeloma; `sex` 1 female, 2 male; `bj` (Bence-Jones protein) 0 no, 1 yes | 48 patients | Chapter 8 | Krall JM, Uthoff VA, Harley JB. A step-up procedure for selecting variables associated with survival. Biometrics. 1975;31(1):49-57 |
| `pigs.dta`, `pigs.csv`, `piglong.dta` | Weekly weights of pigs over nine weeks, wide and long | 48 pigs (432 rows long) | Sections 9.1, 9.3, 9.4, 9.8 | Diggle PJ, Heagerty P, Liang KY, Zeger SL. Analysis of Longitudinal Data. 2nd ed. Oxford University Press; 2002 |
| `cd4trial.dta`, `cd4trial.csv` | AIDS trial: log CD4 counts at up to six visits | 1308 patients, 4391 visits | Sections 9.1, 9.2, 9.4 | Henry K, Erice A, Tierney C, et al. J Acquir Immune Defic Syndr Hum Retrovirol (ACTG 193A trial) |
| `schizo.dta`, `schizo.csv` | Schizophrenia trial: weekly severity of illness | 437 patients, 1603 ratings | Sections 9.6, 9.7 | Hedeker D, Gibbons RD. Longitudinal Data Analysis. Wiley; 2006 (written from the R package `lme4`, `schizophrenia`) |
| `muscatine.dta`, `muscatine.csv` | Obesity in schoolchildren at three surveys | 4856 children, 14,568 rows | Section 9.6 | Woolson RF, Clarke WR. J R Stat Soc A. 1984;147(1):87-99 (written from the R package `geepack`) |
| `epilepsy.dta`, `epilepsy.csv` | Seizure counts in a trial of progabide | 59 patients, 295 rows | Sections 9.6, 9.7 | Thall PF, Vail SC. Biometrics. 1990;46(3):657-671; Leppik IE, et al. Neurology. 1987;37(6):963-968 |

Appendix B of the book describes every variable.

## Data the software fetches itself

Some examples use data that ship with STATA or with R packages, so they are not in this
repository: STATA's example datasets (`webuse lbw`, `auto`, `catheter`, `diet`,
`dollhill3`, `epilepsy`, `fuel`, `hanley`, `iris`, `rate2`, `stan3`, from Stata Press)
and R package datasets such as `MASS::birthwt`.

## Citing and using the data

These files are shared for learning with the book. Please cite the book, and the
original source listed above when you use a published dataset; the published datasets
remain subject to their original sources' terms.

Stata and Stata Press are registered trademarks of StataCorp LLC. R is free software
from the R Foundation for Statistical Computing. This repository and the book are
independent and are not endorsed by StataCorp LLC or the R Foundation.
