# Credit Risk Classification

_April 2025 | Dotan Barak_

## Table of Contents

- [Repo Contents](#repo-contents)
- [Overview of the Analysis](#overview-of-the-analysis)
- [Results](#results)
- [Summary](#summary)
- [Recommendations](#recommendations)
- [Resources](#resources)

---

## Repo Contents

This repository contains the full documentation and code for a supervised learning model developed to classify credit risk in peer-to-peer loan data. The contents include:

- A `README.md` detailing the project methodology, implementation, and evaluation
- A `Credit_Risk/` folder containing:
  - A Jupyter Notebook for preprocessing, model training, and testing
  - A `Resources/` folder with the original dataset (`lending_data.csv`)

---

## Overview of the Analysis

The objective of this analysis was to develop and evaluate a binary classification model that predicts the creditworthiness of loan applicants using historical lending data.

### Step 1: Data Ingestion and Exploration

The dataset was sourced from a peer-to-peer lending platform and consists of 77,000+ records with key financial indicators:

- Loan size, interest rate, borrower income
- Debt-to-income ratio, number of open credit lines
- Derogatory marks (e.g., missed payments, bankruptcies)
- Total debt
- Loan status (0 = healthy, 1 = high risk)

Initial exploration revealed a strong class imbalance, with most borrowers exhibiting no derogatory marks—a likely reflection of institutional risk aversion.

### Step 2: Feature and Target Preparation

- The target variable `loan_status` was extracted as `y`, while all other columns were designated as features `X`.
- This aligns with the supervised learning framework, where labeled outcomes guide the training process.

### Step 3: Train-Test Split

- Using `train_test_split` from `sklearn.model_selection`, the data was partitioned into 75% training and 25% testing sets with a fixed `random_state` for reproducibility.

### Step 4: Model Selection and Training

- A logistic regression model (`LogisticRegression` from `sklearn.linear_model`) was chosen due to its suitability for binary classification tasks.
- The model was fit using the training data (`X_train`, `y_train`).

### Step 5: Predictions and Validation

- The trained model was used to predict loan statuses on the test set (`X_test`).
- Predictions were evaluated using a confusion matrix and classification report to measure model performance.

---

## Results

**Confusion Matrix Output:**

| Actual / Predicted | Healthy (0) | Risky (1) |
| ------------------ | ----------- | --------- |
| Healthy (0)        | 18,663      | 102       |
| Risky (1)          | 56          | 563       |

### Key Metrics:

- **Accuracy:** 0.99  
  While impressive, this metric is inflated by the class imbalance (majority of loans are healthy).
- **Precision (for risky loans):** 0.85  
  Indicates that 15% of loans classified as risky were actually healthy — a meaningful false positive rate.
- **Recall (for risky loans):** 0.91  
  Suggests the model captured most of the truly risky loans, but still missed some.

---

## Summary

Although the model achieves high overall accuracy, the precision metric reveals a risk of denying loans to creditworthy applicants—a potentially costly tradeoff. The real-world impact of false positives (i.e., declining good loans) must be carefully weighed against false negatives (i.e., approving bad loans).

---

## Recommendations

To enhance both performance and fairness of the model:

- **Conduct a model audit** by a third-party data science team or risk analytics unit
- **Benchmark against industry standards** for credit risk models in peer-to-peer or consumer lending
- **Run financial simulations** to estimate the impact of false positives on revenue and customer retention
- **Expand and diversify the training data** to reduce class imbalance and improve generalizability
- **Implement a secondary review** process for loans rejected by the model to catch possible false positives

---

## Ethical Considerations

This model should not be deployed in a fully automated decision pipeline without safeguards. Denying access to credit has serious socioeconomic implications, especially when misclassifications occur. Extra scrutiny and ethical oversight are vital to ensure that biases embedded in the training data do not perpetuate harm. Any rejected applications should undergo further review to ensure fairness and minimize harm.

---

## Resources

- Original dataset: `Resources/lending_data.csv`
- Model development notebook: `Credit_Risk/credit_risk_model.ipynb`
