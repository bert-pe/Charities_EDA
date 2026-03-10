# Charity Deficit Prediction Model

Predicting whether an Australian registered charity will report a financial deficit based on annual financial statement data from the Australian Charities and Not-for-profits Commission (ACNC).

## Overview

This project investigates whether machine learning can identify charities at risk of running a deficit (negative net surplus/deficit) using publicly available government data. The notebook covers a full pipeline from exploratory data analysis through to a baseline logistic regression model, with detailed observations and next steps for a capstone project.

## Data

The dataset comes from the Australian Government's open data portal:
https://www.data.gov.au/data/organization/acnc

- **Source file:** `datadotgov_ais21.xlsx`
- **Size:** 51,747 entries across 93 columns
- **Contents:** Annual Information Statement (AIS) financial data for registered Australian charities and not-for-profits

## Target Variable

A binary column `is_deficit` derived from the `net surplus/deficit` field:

| Value | Meaning |
|-------|---------|
| 1 | Deficit (negative net surplus/deficit) |
| 0 | No deficit (zero or positive) |

The dataset is imbalanced — roughly 25–30% of charities report a deficit.

## Notebook Structure

| Section | Description |
|---------|-------------|
| **1. Importing** | Libraries and display settings |
| **2. Data Loading** | Reading the ACNC Excel file |
| **3. Exploratory Data Analysis** | Duplicate checks, missing values, descriptive statistics, distribution plots (including signed-log histograms), correlation heatmaps, categorical distributions, boxplots by deficit status, interactive scatter plots, outlier analysis via IQR, and financial ratio analysis |
| **4. Feature Engineering** | Target column creation, dropping leakage/irrelevant columns |
| **5. Preprocessing** | Train/test split (80/20 stratified), median imputation for numeric columns, one-hot encoding for categoricals, StandardScaler feature scaling |
| **6. Baseline Model** | Logistic Regression (lbfgs solver, max_iter=1000) |
| **7. Model Evaluation** | Accuracy, ROC-AUC, classification report, confusion matrix, ROC curve, top feature coefficients, detailed interpretation |
| **8. Conclusion** | Key findings and limitations |
| **9. Capstone Next Steps** | Plans for further development |

## Key Findings

- **Accuracy:** 75.56% — only marginally better than always predicting "no deficit"
- **ROC-AUC:** 0.8492 — the model can rank deficit charities higher in probability, but the default decision boundary misses almost all of them
- **Recall for deficit class:** ~3% — the model catches very few actual deficit cases
- Financial features (revenue, expenses, assets, liabilities) dominate the top model coefficients
- Revenue and expenses scale closely together across charities; deficit status depends on small deviations from that proportional relationship

Install dependencies with:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn plotly
```

## Usage

1. Place the data file at `data/datadotgov_ais21.xlsx`
2. Open and run `charity.ipynb` in Jupyter Notebook or JupyterLab

```bash
jupyter notebook charity.ipynb
```

## Project Status

This is an initial investigation and baseline model. Planned next steps include exploring tree-based models (Random Forest) or engineering additional features from non-financial columns, and evaluating whether non-financial characteristics can meaningfully predict deficit risk.


## License

This project is for educational and research purposes. The data is a Creative Commons Attribution 2.5 Australia. https://creativecommons.org/licenses/by/2.5/au/
