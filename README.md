# SIL Project – Diabetes Prediction

**Author:** Victoria Grosu  
**Date:** May 2025  

## Overview
This project develops a **machine learning pipeline** to predict whether an adult has been diagnosed with diabetes using data from the **2023 National Health Interview Survey (NHIS)**.  
It integrates **statistical modeling**, **regularization techniques**, and **comparative evaluation** of classifiers to ensure both **high predictive performance** and **interpretability**.

---

## Dataset
- **Source:** [National Health Interview Survey 2023 (NHIS)](https://www.cdc.gov/nchs/nhis/documentation/2023-nhis.html)  
- **Initial size:** 29,522 rows × 647 columns  
- **Final cleaned dataset:** 23,826 adults × 128 variables (no missing values)

### Key Cleaning Steps
- Filtered adults aged **18–84**
- Converted **weight (lbs → kg)** and **height (in → m)**
- Removed top-coded income-to-poverty ratios  
- Handled **survey logic missingness** (mother/daughter structure)
- Unified “unknown” categorical values (7, 8, 9)
- Dropped variables with >10% unknown responses  
- Removed redundant features using **Pearson** and **Cramér’s V** correlations  
- Created binary target: `has_diabetes` (1 = Yes, 0 = No)

---

## Exploratory Data Analysis
- Explored **age**, **weight**, **height**, and **poverty ratio** distributions by diabetes status.  
- Applied **log-transformation** to reduce skewness in weight and poverty ratio, improving model robustness.

---

## Modeling Pipeline
The study evaluates several **regularized and classical classification methods**.

### 1. **LASSO Regression**
- Used to select the most relevant predictors via cross-validation.  
- Achieved **AUC = 0.86**, maintaining interpretability.  
- Selected `lambda.1se` for a more parsimonious model.

### 2. **Logistic Regression (GLM)**
Three logistic models were tested:
- **Full Model:** all LASSO-selected variables  
- **Log-Transformed:** includes log-weight and log-poverty ratio  
- **Reduced Model:** 9 interpretable predictors with clinical and social relevance  

**Best Model:** Reduced GLM  
- **AUC:** 0.85  
- **Accuracy:** 0.76  
- **Sensitivity:** 0.83  
- **Specificity:** 0.75  

#### Key Predictors
- **Age**
- **Log(Weight)**
- **Self-rated Health**
- **Recent Eye Exam**
- **Coronary Disease, Cholesterol, Hypertension**
- **Log(Poverty Ratio)**
- **Ethnicity**

---

## Model Comparison

| Model | AUC | Accuracy | Sensitivity | Specificity |
|-------|------|-----------|--------------|--------------|
| Logistic Regression (GLM) | 0.86 | 0.76 | 0.83 | 0.75 |
| LDA | 0.85 | 0.73 | 0.84 | 0.72 |
| Naive Bayes | 0.85 | 0.75 | 0.82 | 0.74 |
| KNN (k=20) | 0.81 | 0.70 | 0.80 | 0.69 |
| Ridge Regression | 0.86 | 0.75 | 0.86 | 0.73 |

 **Conclusion:** Logistic Regression provides the best trade-off between accuracy and interpretability, confirming its suitability for clinical diagnostic applications.

---

## Technologies Used
- **R** (tidyverse, glmnet, MASS, caret)
- **Python** (optional, for visualization or automation)
- **Statistical methods:** LASSO, Ridge, GLM, LDA, Naive Bayes, KNN
---
