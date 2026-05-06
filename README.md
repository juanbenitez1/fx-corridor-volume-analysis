# FX Corridor Volume Analysis

Time series analysis of daily transfer volumes for a GBP → Emerging Market 
payment corridor (Apr–Dec 2023), completed as part of a technical assessment 
at a leading UK-based Fintech.

## Overview

This analysis addresses five core questions:

1. **Distribution characterization** — identifying the underlying distributional 
   structure of daily transfer volumes, including bimodality analysis.
2. **Real-world drivers** — explaining the business causes behind the observed 
   distribution shape.
3. **Analytical implications** — consequences for statistical modeling and inference 
   given the data's structure.
4. **Structural change testing** — determining whether quarter-to-quarter differences 
   are statistically significant or attributable to background fluctuation.
5. **Volume forecasting** — estimating total October 2023 transfer volume using an 
   ensemble of three complementary methods with confidence intervals.

## Methods

- **Data storage** — in-memory SQLite for structured querying throughout the analysis
- **Missing data imputation** — weekday-stratified approach (quarter × weekday average, 
  falling back to historical weekday average), preserving weekly seasonality
- **Distributional analysis** — regime stratification (Mon–Thu / Friday / Weekend), 
  Hartigan Dip Test for bimodality
- **Structural change** — Kruskal-Wallis + Dunn post-hoc (Bonferroni correction), 
  Mann-Kendall trend test per regime
- **Forecasting ensemble**:
  - Stratified mean by day type (conservative lower bound)
  - OLS with day-type dummies + HC3 robust standard errors
  - Additive Holt-Winters (seasonal period = 7) with 1,500-iteration bootstrap CI

## Key Results

| Method | October 2023 Estimate |
|---|---|
| Stratified Mean | £3.52M |
| OLS (trend + day dummies, HC3) | £5.95M |
| Holt-Winters | £6.79M |
| **Central estimate** | **£5.4M** |
| 95% Bootstrap CI | £5.34M – £7.91M |

## Stack

`Python` `Pandas` `NumPy` `SQLite` `Statsmodels` `SciPy` `Scikit-posthocs` 
`Diptest` `PyMannKendall` `Matplotlib` `Seaborn`

## Files

| File | Description |
|---|---|
| `notebook.ipynb` | Full analysis with code, outputs, and commentary |

> Data not included due to confidentiality.

---
*Methodology and conclusions are entirely my own. Data was provided as part of the assessment.*
