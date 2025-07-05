# PSID-Panel-Data-Processing

---

````yaml
# README.Rmd

title: "PSID Panel Data Processing"
author: "Your Name"
date: "`r Sys.Date()`"
output:
  github_document:
    toc: true
    toc_depth: 3
    df_print: paged
---

# Overview
This repository provides a complete, reproducible workflow to harmonize, document, and analyze family‑level PSID (Panel Study of Income Dynamics) data across five survey waves (2015, 2017, 2019, 2021, 2023). By the end of this pipeline, you will have:

- A **panel‑long** dataset: one row per family (`ID`) per wave (`year`), with all key variables as columns.
- Clear documentation of **why** each variable was chosen, including links to their PSID Data Center ER‑codes and conceptual definitions.
- An R script (`analysis/prepare_data.R`) that reads raw PSID files, selects and renames variables, merges waves, and outputs both wide and long CSVs for analysis.

This setup ensures transparency, reproducibility, and ease of collaboration, whether you’re pushing to GitHub or sharing with your PI.

# Variables: Selection & Rationale
Each variable below was chosen to capture core demographic, wealth, debt, and socioeconomic dimensions at the family level. Whenever an imputed (“IMP …”) version was available, we selected it to maximize completeness and reduce missingness.

## 1. Identification & Demographics

| Friendly name        | ER‑code      | Description                                   |
|:---------------------|:-------------|:----------------------------------------------|
| **ID**               | ER78002      | Unique family/unit identifier across waves.   |
| **Race**             | L40 (ER81144)| Categorical: White, Black, Asian, Other.      |
| **Hispanic Ethnicity**| L39 (ER81143)| Binary indicator of Hispanic origin.          |
| **Sex**              | ER78018      | Reference person’s gender.                    |
| **Age**              | ER78017      | Reference person’s age in years.              |
| **Marital Status**   | ER78025      | Reference person’s marital status.            |
| **Children Count**   | ER78021      | Number of children in household.              |

## 2. Wealth & Asset Holdings
Assets provide insight into household financial security and potential buffers against shocks.

| Concept                        | Indicator ER‑code | Value ER‑code     | Notes                              |
|:-------------------------------|:------------------|:------------------|:-----------------------------------|
| **Real Estate**                | W1                | IMP W1_VAL        | Home/property ownership & value.   |
| **Farm/Business**              | W10               | IMP W11A, IMP W11B| Business/farm assets & debts.      |
| **Stocks (non‑IRA)**           | W15               | IMP W16           | Indicator + imputed value.         |
| **Other Assets**               | W33               | IMP W34           | Additional asset classes.          |
| **Annuities / IRAs**           | W21               | IMP W22           | Pension-like instruments.          |
| **Wealth Summary**             | —                 | WEALTH1/WEALTH2   | Net worth excl./incl. home equity. |

## 3. Debt Measures (Imputed Only)
Debts capture financial liabilities. We always select the **imputed** amount (*IMP …*) over raw or accumulated versions.

| Debt Type         | Indicator    | Imputed Value    |
|:------------------|:-------------|:-----------------|
| **Credit Card**   | W38A         | IMP W39A          |
| **Student Loans** | W38B1        | IMP W39B1         |
| **Medical Debt**  | W38B2        | IMP W39B2         |
| **Legal Debt**    | W38B3        | IMP W39B3         |
| **Other Debt**    | W38B7        | IMP W39B7         |

## 4. Liquid Assets & Savings

| Concept                  | ER‑code                | Description                                   |
|:-------------------------|:-----------------------|:----------------------------------------------|
| **Checking/Savings**     | W27A, W28A             | Indicator + imputed year‑end balance.         |
| **CDs/Bonds/T‑Bills**    | W27, W28               | Indicator + imputed value of time deposits.   |

## 5. Business & Self‑Employment

| Concept                   | ER‑code   | Description                             |
|:--------------------------|:----------|:----------------------------------------|
| **Industry Code**         | BC21      | 2-digit SIC industry of main job.       |
| **Self‑Employment**       | BC22      | Indicator of self-employment status.    |

## 6. Stimulus & PPP Variables

| Program           | ER‑code                    | Description                               |
|:------------------|:---------------------------|:------------------------------------------|
| **Stimulus Payment**| G44B2 (ind), G45B2 (amt) | 2020 CARES Act stimulus received.         |
| **PPP Loans**       | G44B3 (ind), G45B3 (amt) | Paycheck Protection Program loans.        |

## 7. Time‑Use / Education Module

| Concept                      | ER‑code   | Description                                    |
|:-----------------------------|:----------|:-----------------------------------------------|
| **Educational Activity Hours**| F1F       | Hours spent on learning/training by head.      |

## 8. Geography

| Concept                   | ER‑code   | Description                                 |
|:--------------------------|:----------|:---------------------------------------------|
| **Metro vs. Nonmetro**    | METRO     | Metro area indicator.                        |
| **Beale Rural‑Urban Code**| BEALE     | Rural-urban classification.                  |

# Repository Structure
```bash
psid-panel-data/
├── analysis/                   # Data prep & analysis scripts
│   └── prepare_data.R          # Main R script to build panel
├── data/                       # Raw PSID downloads (gitignored)
├── outputs/                    # Processed outputs
├── README.Rmd                  # This file
└── .gitignore                  # Exclude raw data & temp files
````

# Getting Started

1. **Clone the repository**:

```bash
git clone https://github.com/yourusername/psid-panel-data.git
cd psid-panel-data
```

2. **Place raw data** (`.sas7bdat` & `.xlsx`) in `/data`.

3. **Install dependencies** in R:

```r
install.packages(c("sas7bdat","readxl","haven","dplyr","tidyr","purrr"))
```

4. **Run the prep script**:

```bash
Rscript analysis/prepare_data.R
```

5. **Inspect outputs** in `/outputs`:

* `panel_wide.csv`: one row per family per year.
* `panel_long.csv`: tidy format (`ID`,`year`,`variable`,`value`).

# Next Steps & Analysis

* Use `panel_wide.csv` for panel regressions.
* Use `panel_long.csv` for dynamic event-study plots.

# License & Contact

**Author:** Your Name (`elena.ajayi19l@stjohns.edu`)
**License:** CC BY-NC 4.0
