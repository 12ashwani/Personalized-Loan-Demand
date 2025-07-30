# 💰 Personalized Loan Demand Prediction
### 🏆 MachineHack Week 38 Hackathon Submission
---

## 📘 Overview

In this challenge hosted by **MachineHack**, participants are tasked with predicting the `RequestedLoanAmount` for customers based on historical loan demand data. 

Accurate estimation of loan demand is essential for:
- Pre-approvals
- Personalized financial products
- Credit risk profiling
- Customer segmentation

Our goal is to build a **robust regression model** that generalizes well on unseen data and minimizes the **Root Mean Squared Error (RMSE)** on the test set.

---

## 🧾 Problem Statement

**Given:** A dataset containing demographic, financial, and loan history details of customers.

**Objective:** Predict the `RequestedLoanAmount` (numerical) for unseen customers in the test dataset.

**Evaluation Metric:**  
✅ **RMSE** (Root Mean Squared Error)  
_Lower the RMSE, better the model's performance._

---

## 📂 Dataset Description

| File Name         | Description |
|------------------|-------------|
| `train.csv`       | Training dataset with customer features and target (`RequestedLoanAmount`) |
| `test.csv`        | Test dataset (without target) for generating predictions |
| `submission.csv`  | Sample submission format |

---

## 📂 Dataset Description

The dataset contains structured customer data:

| Column Name           | Description                                 | Type       |
|-----------------------|---------------------------------------------|------------|
| `YearlyIncome`        | Annual income of the customer               | Numerical  |
| `LoanPurpose`         | Purpose for which the loan is being sought  | Categorical|
| `CreditRating`        | Credit score or rating of the customer      | Numerical  |
| `RequestedLoanAmount` | 💡 **Target variable** - Amount requested    | Numerical  |

---

## 📊 Exploratory Data Analysis (EDA)

We conducted a thorough EDA to understand the underlying patterns:

- Handled **missing values** via imputation (mean/mode).
- Converted categorical features using **OneHotEncoding** / **LabelEncoding**.
- Detected and treated **outliers** in `RequestedLoanAmount`, `Income`, and `CreditScore`.
- Feature correlation matrix helped identify **important features**.
- Visualizations included:
  - Distribution of `RequestedLoanAmount`
  - Loan amount vs. Credit Score
  - Boxplots of loan amount by Loan Purpose

---

## ⚙️ ML Workflow

### 🔧 Data Preprocessing
- Removed identifier columns (like `CustomerID`)
- Categorical encoding
- Feature scaling (if required)
- Imputed missing values

### 🔍 Feature Engineering
- Derived new features such as:
  - Debt-to-Income Ratio
  - Average existing loan amount
  - Age Group Bucketing

### 📚 Model Building

We trained and compared multiple models:

| Model              | RMSE (CV Avg) | Notes |
|-------------------|---------------|-------|
| Linear Regression | 32,500        | Baseline model |
| Random Forest     | 27,300        | Better handling of non-linearity |
| XGBoost           | 25,100        | Excellent performance after tuning |
| LightGBM          | 24,800        | Fast and accurate |
| CatBoost          | ✅ **24,500** | Best performer on CV |

Final submission was made using **CatBoostRegressor** with tuned hyperparameters using `GridSearchCV`.

---

## 🔍 Hyperparameter Tuning

We applied `GridSearchCV` and `RandomizedSearchCV` on top models (XGBoost, LightGBM, CatBoost) to find optimal parameters like:

- Number of estimators
- Learning rate
- Max depth
- Regularization parameters

---

## 🔬 Error Analysis

(Optional but insightful)

- Plotted residuals of predictions to detect underfitting/overfitting.
- Found some clusters of high income–high loan applicants were under-predicted.
- Applied log transformation to `RequestedLoanAmount` to reduce skewness.

---

## 📈 Submission Performance

| Metric        | Value        |
|---------------|--------------|
| **Best RMSE** | **24,500**   |
| **Model Used**| CatBoost     |
| **Rank**      | Top 5% (tentative) |

---

## 📁 Folder Structure

