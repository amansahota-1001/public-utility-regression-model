# public-utility-regression-model
# Hotazel Steam Revenue Forecasting — Regression Model Comparison

## Overview
This project, prepared for **Hotazel Steam** by **QuantFolio Solutions**, compares two simple linear regression models to determine which one more accurately forecasts monthly revenue:

- **Model 1** — predicts `revenue` using `production`
- **Model 2** — predicts `revenue` using Cooling Degree Days (`coolDD`)

Both models are trained on historical data and evaluated on held-out testing data using **Mean Absolute Percentage Error (MAPE)**.

## Data
The dataset (`AICPA_regressionAnalysisData.csv`) contains 48 monthly observations (2011–2014) with the following columns:

| Column | Description |
|---|---|
| `type` | Indicates whether the row is used for training (`dt4training`) or testing (`dt4testing`) |
| `date` | Month-end date |
| `revenue` | Monthly revenue |
| `production` | Monthly production volume |
| `coolDD` | Cooling Degree Days |
| `heatDD` | Heating Degree Days |

- **Training set:** Jan 2011 – Dec 2013 (36 months)
- **Testing set:** Jan 2014 – Dec 2014 (12 months)

## Workflow
1. **Import the dataset** and inspect structure/types with `pandas`.
2. **Prepare the data** — convert `date` to a proper `datetime` object.
3. **Explore the data** — summary statistics (`describe()`) and a correlation matrix among `revenue`, `production`, `coolDD`, and `heatDD`.
4. **Visualize revenue** over time with `matplotlib`.
5. **Split into training and testing sets** based on the `type` column.
6. **Fit Model 1** (`revenue ~ production`) using `statsmodels.OLS` on the training data, then forecast the testing period.
7. **Fit Model 2** (`revenue ~ coolDD`) the same way.
8. **Compare accuracy** of both models on the testing set using percentage error and MAPE, with a final chart overlaying actual vs. predicted revenue for each model.

## Results (from the notebook)

**Model 1 — Revenue ~ Production**
- R-squared: 0.397
- Coefficient on `production`: ≈18.99 (p < 0.001, statistically significant)
- Test-set MAPE: **≈25.4%**

**Model 2 — Revenue ~ coolDD**
- R-squared: 0.017 (very weak fit)
- Coefficient on `coolDD`: not statistically significant (p = 0.448)
- Test-set MAPE: I am not fully certain of this exact figure — the notebook doesn't display a computed mean for Model 2's percentage error the way it does for Model 1. Based on the individual `model2_pctError` values shown in the output table, the average works out to **approximately 29.5%**, but you may want to verify this by re-running `model2_assessment['model2_pctError'].mean()` in the notebook.

### Conclusion
**Model 1 (production-based)** has a higher R-squared, a statistically significant predictor, and a lower MAPE on the testing data than **Model 2 (coolDD-based)**. This suggests production is a materially better predictor of Hotazel Steam's monthly revenue than cooling degree days.

## Tech Stack
- Python
- `pandas`, `numpy`
- `matplotlib` (visualization)
- `statsmodels` (OLS regression)

## Repository Structure (suggested)
```
├── AICPA_regressionAnalysisData.csv   # source data
├── Quiz_Week_8_9.ipynb                # analysis notebook
└── README.md                          # this file
```
