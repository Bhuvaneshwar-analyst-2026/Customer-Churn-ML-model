# Customer Churn Prediction — Machine Learning Final Project

**Course:** BAN 614 — Machine Learning <br>
**Institution:** University of Dayton <br>
**Author:** Bhuvaneshwar Sannappareddy <br>
**Language:** R <br>
**Libraries:** tidyverse · caret · pROC · e1071 · MASS · rpart · rpart.plot

---

## Project Overview

Built and evaluated five machine learning classification models to predict customer churn for a telecom company. Analyzed customer behavior patterns, identified key churn drivers, compared model performance, and developed a data-driven business recommendation to reduce revenue loss.

---

## Dataset

| Dataset | Purpose | Records |
|---|---|---|
| `Model_Building_Data.rda` | Model training and testing | Split 80% train / 20% test |
| `Implementation_Data.rda` | Final implementation predictions | 500 customers |

**Key Variables:**

| Variable | Description |
|---|---|
| `tenure` | Months customer has been with company |
| `monthlycharges` | Monthly billing amount |
| `totalcharges` | Total amount charged to date |
| `internetservice` | DSL, Fiber optic, or None |
| `contract` | Month-to-month, One year, Two year |
| `paymentmethod` | Electronic check, Bank transfer, Credit card |
| `seniorcitizen` | Whether customer is a senior citizen |
| `status` | Target variable — Current or Left |

---

## Data Preparation

- Loaded and standardized column names to lowercase
- Imputed missing `totalcharges` values using group-wise median by status group
- Applied log transformation `log1p()` to normalize `totalcharges`
- Split 80/20 into training and test sets using stratified sampling with `createDataPartition()`
- Confirmed zero missing values after cleaning

---

## Exploratory Data Analysis

**Key Churn Drivers Identified:**

| Variable | Finding |
|---|---|
| Contract Type | Month-to-month customers churn significantly more |
| Internet Service | Fiber optic users have highest churn rate |
| Senior Citizen | Senior citizens more likely to churn |
| Payment Method | Electronic check users have highest churn rate |
| Online Security | Customers without online security churn more |
| Partner Status | Customers without partners are more likely to leave |
| Tenure | Shorter tenure customers churn more frequently |
| Paperless Billing | Paperless billing customers show slightly higher churn |

---

## Models Built & Evaluated

### 1. Logistic Regression
- Built full model and optimized using variable selection
- Threshold optimization across range 0.3 to 0.7
- **Best AUC: 0.8567** — strongest discriminatory power
- **Best Accuracy: 82.45%** at threshold 0.50
- Key predictors: seniorcitizen, tenure, phoneservice, internetservice, contract, paymentmethod, paperlessbilling

### 2. Naive Bayes
- Built using `naiveBayes()` from `e1071` package
- Evaluated multiple variable combinations to maximize AUC
- **Best Accuracy: 81.14%** at threshold 0.70

### 3. Linear Discriminant Analysis (LDA)
- Built using `lda()` from `MASS` package
- Tested 4 different model formulas systematically
- **Best AUC: 0.8511** — Model 4 was highest performer
- **Best Accuracy: 81.30%** at threshold 0.70

### 4. Quadratic Discriminant Analysis (QDA)
- Built using `qda()` from `MASS` package
- Tested multiple variable combinations
- **Best AUC: 0.8419** — Model 3 was highest performer
- **Best Accuracy: 77.14%**

### 5. Decision Tree
- Built using `rpart()` with tree visualization via `rpart.plot`
- Tuned using cross-validation
- **Best Accuracy: 79.60%**

---

## Final Model Comparison

| Model | Best AUC | Best Accuracy |
|---|---|---|
| **Logistic Regression** | **0.8567** | **82.45%** |
| LDA | 0.8511 | 81.30% |
| Naive Bayes | — | 81.14% |
| QDA | 0.8419 | 77.14% |
| Decision Tree | — | 79.60% |

**Winner: Logistic Regression** — highest AUC (0.8567) AND highest accuracy (82.45%)

---

## Business Implementation

Applied the best Logistic Regression model to 500 customers in the Implementation Dataset:

| Metric | Value |
|---|---|
| Customers predicted to leave | **104 out of 500** |
| Estimated monthly revenue at risk | **$8,483.70** |
| Average monthly charge per at-risk customer | $81.57 |

---

## Business Recommendations

### Top Churn Factors by Coefficient Importance

| Predictor | Importance | Direction |
|---|---|---|
| Contract — Two Year | 1.8574 | Reduces churn |
| Internet — Fiber Optic | 0.9905 | Increases churn |
| Contract — One Year | 0.8226 | Reduces churn |
| Internet — No Service | 0.7334 | Reduces churn |
| Phone Service | 0.6802 | Reduces churn |
| Paperless Billing | 0.3927 | Increases churn |
| Senior Citizen | 0.3462 | Increases churn |

### Proposed Incentive Scheme

**Strategy:** Offer $10 monthly discount to the 104 at-risk customers for 6 months

| Metric | Value |
|---|---|
| Customers targeted | 104 |
| Expected retention rate | 50% → 52 customers |
| Monthly incentive cost | 52 × $10 = $520 |
| Monthly revenue retained | 52 × $81.57 = $4,241.64 |
| Net monthly benefit | $3,721.64 |
| **Net 6-month benefit** | **$22,329.84** |

**ROI:** Investing $3,120 over 6 months prevents over $25,449 in lost revenue.

---

## Key Findings

- **Logistic Regression** is the best model — AUC 0.8567, Accuracy 82.45%
- **Contract type** is the strongest churn predictor — long-term contracts significantly reduce churn
- **104 out of 500** current customers are predicted to leave
- **$8,483.70** monthly revenue is at risk if no action is taken
- A targeted **$10 discount incentive** generates **$22,329 net benefit** over 6 months

---

## Files in This Repository

| File | Description |
|---|---|
| `customer_churn_analysis.Rmd` | Full R Markdown source code |
| `customer_churn_analysis.html` | Rendered analysis with all charts and results |
| `Model_Building_Data.rda` | Training and test dataset |
| `Implementation_Data.rda` | Implementation holdout dataset — 500 customers |

---

## Skills Demonstrated

- **R Programming** — tidyverse, caret, pROC, ggplot2, rpart
- **Machine Learning** — Logistic Regression, Naive Bayes, LDA, QDA, Decision Tree
- **Model Evaluation** — ROC curves, AUC, confusion matrix, threshold optimization
- **EDA** — Distribution analysis, correlation analysis, churn driver identification
- **Business Analysis** — Revenue impact analysis, incentive scheme design, cost-benefit evaluation
- **Data Cleaning** — Missing value imputation, feature engineering, log transformation

---

> **Data Source:** BAN 614 Machine Learning course dataset — University of Dayton
