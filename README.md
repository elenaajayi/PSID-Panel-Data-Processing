

# Overview

This repository provides a reproducible workflow for preparing and analyzing family-level data from the **Panel Study of Income Dynamics (PSID)** across five waves: **2015, 2017, 2019, 2021, and 2023**. It integrates data cleaning, ER code harmonization, and variable labeling to construct a clean panel dataset in both **long** and **wide** formats.

This project was initiated as part of a research collaboration under Dr. [PI Name], and is now being extended into a formal research study under the **CEB Fellowship Proposal**.

## Project Goals

- Create harmonized panel datasets across multiple PSID waves
- Enable exploratory and descriptive analysis of wealth, debt, and demographic trends
- Support stimulus-related outcome analysis (e.g., CARES/PPP)
- Build toward regression models and hypothesis testing framed by CEB proposal research questions

# Key Outputs

- ✅ `psid_construct_finAL.pdf`: A cleanly rendered document detailing the panel reshaping pipeline
- ✅ `psid_analysis.rds` and `.csv`: Wide-format panel dataset ready for regression and summary analysis
- ✅ Variable-labeled dataset using actual ER codes from PSID labels file
- ✅ Summary statistics by year for wealth, debt, and demographics

# Variable Selection Rationale

Variables were selected to support core research questions related to:

- **Wealth inequality and business ownership**
- **Debt and financial vulnerability**
- **Race, gender, and geography as mediators**
- **Pandemic impact on financial outcomes**
- **PPP access and business resilience (planned extension)**

Priority was given to imputed versions of variables (`WEALTH1`, `WEALTH2`, etc.) for higher completeness.

# Stimulus and PPP Indicators

| Concept                 | ER Codes Used                 | Description                          |
|-------------------------|-------------------------------|--------------------------------------|
| **CARES Act Stimulus**  | G44B2 (indicator), G45B2 (amt)| 2020 payments to families            |
| **PPP Loan Receipt**    | G44B3 (indicator), G45B3 (amt)| Receipt and value of PPP loans       |

# File Structure

```bash
psid-panel-data/
├── analysis/                 # All .Rmd and .R scripts
│   ├── psid_construct.Rmd   # Main panel construction document
│   ├── ceb_analysis.R       # Placeholder for CEB-specific models
├── data/                    # Raw Excel files (e.g., 2015_2023.xlsx)
├── outputs/                 # Cleaned data and PDFs
├── README.Rmd               # This README
├── .gitignore               # Excludes sensitive or large files
```

# How to Reproduce

1. Clone the repo:

```bash
git clone https://github.com/yourusername/psid-panel-data.git
```

2. Install R dependencies:

```r
install.packages(c("dplyr", "tidyr", "readxl", "stringr", "purrr", "scales", "ggplot2"))
```

3. Load your Excel file (named `2015_2017_2019_2021_2023.xlsx`) into the `/data` folder.

4. Knit `psid_construct.Rmd` or run the associated `.R` script to generate:
   - A long-format tibble (`psid_long`)
   - A wide-format dataset (`psid_analysis`)

# Next Steps: CEB Fellowship

The immediate next steps will involve extending this pipeline to:

- 🧮 Answer research questions specified in the Research Proposal
- 📈 Generate race-stratified regression models and Difference-in-Differences (DiD) analyses
- 📊 Integrate visualization and robustness checks for business ownership, PPP effects, and wealth recovery

I will continue committing to this repository as I finalize the analysis and draft the results for the fellowship.

# Contact & Licensing

**Author:** Elena Ajayi  
**Contact:** elena.ajayi19l@stjohns.edu  
**License:** CC BY-NC 4.0  
