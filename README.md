# NBA Player Efficiency Rating | Econometric Analysis 🏀

**An applied econometrics project using R to investigate the association between NBA player characteristics, career performance statistics, and career Player Efficiency Rating (PER).**

## Project at a glance

| | |
|---|---|
| **Research question** | Which observable player attributes and career statistics are associated with career PER? |
| **Outcome** | Career Player Efficiency Rating (`career_PER`) |
| **Study design** | Cross-sectional, multivariate regression |
| **Analysis sample** | 1,696 players (as reported in the course paper) |
| **Reported final R² / adjusted R²** | **0.8149 / 0.8113** |
| **Tools** | R, R Markdown, Excel |
| **Econometric methods** | OLS, interaction & polynomial terms, heteroskedasticity diagnostics, feasible GLS / weighted least squares, heteroskedasticity-robust standard errors |

> **Results are quoted from the accompanying course report.** They have not been independently reproduced or re-estimated for this repository. Statistical association should not be interpreted as a causal effect.

## Research motivation

Player Efficiency Rating (PER) summarizes aspects of a basketball player's productivity. This project examines how physical characteristics (such as height and weight), career totals, shooting efficiency, and playing position relate to variation in career PER.

## Methodology

1. **Data preparation:** inspect and transform highly skewed career statistics using `log1p` or inverse hyperbolic sine transformations; apply clipped logit transformations to bounded shooting percentages.
2. **Model specification:** build multivariate OLS specifications with nonlinear terms and interactions.
3. **Hypothesis testing:** evaluate coefficients using *t*-tests, joint significance using *F*-tests, and functional-form adequacy using the Ramsey RESET test.
4. **Heteroskedasticity:** examine a White-type auxiliary regression; the report rejects constant error variance.
5. **Final inference:** estimate feasible generalized least squares (FGLS) implemented through weighted least squares (WLS), and report robust standard errors.

### Reported results

| Statistic | Value |
|---|---:|
| Final model R² | 0.8149 |
| Adjusted R² | 0.8113 |
| Overall F-statistic | 221.8 |
| Overall F-test p-value | < 2.2 × 10⁻¹⁶ |

In the report, the White-type test finds evidence of heteroskedasticity (LM ≈ 56.89), motivating variance-adjusted estimation. The model explains approximately 81% of *in-sample variation* in PER in the reported analysis; this is **not** an out-of-sample prediction or a causal estimate.

## Repository structure

```text
NBA-Player-Efficiency-Econometrics/
├── README.md
├── .gitignore
├── data/
│   ├── ie_final.xlsx               # Analysis workbook used by R
│   ├── players.csv                 # Supplied player-level source data
│   ├── salaries_1985to2018.csv    # Supplied historical salary data
│   └── summary_statistics.csv      # Supplied descriptive statistics
├── analysis/
│   ├── NBA_PER_Analysis.Rmd        # Version with portable project paths
│   └── IEproject2025final_original.Rmd
├── report/
│   └── 2025group1_ie_report.pdf   # Original course research report
└── outputs/                       # Generated files (ignored by Git)
```

## Running the analysis

1. Install **R** and **RStudio**.
2. Open this repository folder as your working directory (the folder containing `README.md`).
3. Install the R packages:

```r
install.packages(c(
  "readxl", "stringr", "dplyr", "stargazer", "lmtest",
  "sandwich", "psych", "corrplot", "reshape2",
  "ggplot2", "car", "writexl", "rmarkdown"
))
```

4. Open `analysis/NBA_PER_Analysis.Rmd` in RStudio and run its chunks from the repository root. The updated script reads `data/ie_final.xlsx` and writes generated data to `outputs/ie_df.xlsx`.

**Reproducibility note:** the supplied notebook is exploratory course research, not a fully verified end-to-end pipeline. Some parts are draft commentary or model-search experiments; package availability and data definitions may affect execution. The original notebook is preserved for transparency. The original referenced a local clipboard image that was not supplied; this missing reference is replaced with a note in the portable version.

## Data and limitations

- The accompanying paper reports a final analysis sample of 1,696 players; the raw source tables may cover different populations or time periods.
- PER and career statistics can be mechanically related. The regression is primarily an explanation of *associations*, not evidence of causal drivers.
- The salary CSV is provided as source material, but **salary is not the dependent variable** in the reported PER model.
- Please verify the **ownership, licensing and redistribution permissions** of data before publishing publicly.
- The report credits multiple project contributors. Confirm all contributors are comfortable with public release before making this repository public.

## Report

See [`report/2025group1_ie_report.pdf`](report/2025group1_ie_report.pdf) for the full motivation, equations, diagnostic tests, estimates and discussion.

## Skills demonstrated

`Econometrics` · `R` · `OLS` · `FGLS` · `Weighted Least Squares` · `Robust Standard Errors` · `Hypothesis Testing` · `Data Transformation` · `Model Diagnostics` · `Sports Analytics`

---

*Academic group course project, 2025. See the accompanying report for author credits.*
