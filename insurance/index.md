---
layout: single
title: "Socio-Demographic Determinants of Health Insurance Costs in the US"
permalink: /insurance/
author_profile: false
---

**Thibault Fieve** · Hult International Business School

[[Paper PDF]](/files/insurance-cost-report(1).pdf) &nbsp;&nbsp; [[GitHub](https://github.com/ton-github/insurance-cost)]

---

## Overview

This study analyzes 1,337 beneficiaries (after deduplication) from the Medical 
Cost Personal Dataset to identify and quantify the socio-demographic factors 
driving medical charge disparities. The target variable is `charges`, the annual 
medical costs billed in USD.

---

## Data

The dataset is publicly available on 
[Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance). 
It contains 1,338 observations with 7 variables, reduced to 1,337 after 
dropping one exact duplicate.

- `age` — age of the beneficiary
- `sex` — gender of the beneficiary
- `bmi` — body mass index
- `children` — number of children covered by the contract
- `smoker` — smoking status
- `region` — geographic region (NE, NW, SE, SW)
- `charges` — annual medical costs billed in USD (target variable)

---

## Objective

Identify the key socio-demographic determinants of health insurance costs and 
build predictive models to estimate individual risk profiles, evaluated on a 
held-out test set stratified by smoker status (80/20 split).

---

## EDA

**Bivariate Analysis with Correlation Matrix**

![bivariate](/images/bivariate_analysis.png)

**Risk Profile Segmentation**

![risk](/images/risk_profile.png)

---

## Models

Three models compared against a constant baseline: OLS on log(charges) with 
HC3 robust standard errors, Gamma GLM with log link, and Random Forest with 
hyperparameters tuned via stratified 5-fold cross-validation.

**OLS Residual Diagnostics**

![residuals](/images/ols_diagnostics.png)

**Random Forest Permutation Importance**

![rf](/images/permutation_importance.png)

**Model Comparison**

![comparison](/images/model_comparison.png)

---

## Results

| Model | R² | MAE ($) | RMSE ($) |
|---|---|---|---|
| Baseline (mean predictor) | -0.00 | 9,081 | 12,013 |
| OLS log(charges) | 0.807 | 2,727 | 5,280 |
| Gamma GLM (log link) | 0.815 | 3,100 | 5,169 |
| Random Forest | 0.926 | 1,637 | 3,269 |

Smoking status and its interaction with BMI explain approximately 90% of 
test-set variance in log(charges). Random Forest achieves a **$1,089 MAE 
advantage** over OLS, statistically significant via paired bootstrap 
(95% CI [$702; $1,513]).

The five-tier risk segmentation delivers an **11.8x cost ratio** between 
the top and bottom tiers.

---

## How to Run

```bash
docker build -t insurance_project .
docker run -p 8888:8888 insurance_project
```

Open `http://localhost:8888` and run `notebooks/analysis_v2.ipynb`.
