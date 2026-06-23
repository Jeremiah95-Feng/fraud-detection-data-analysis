# 🔍 Fraud Detection Data Analysis System

**Course:** Business Data Analytics (MGT174) — COMSATS University Islamabad  
**Submitted to:** Sir Ali Usama  
**Team:** Alisha Malik | Jeremiah Huang | Minahil Javed  
**Date:** March 29, 2026

---

## 📌 Project Overview

This project analyzes 51,000 financial transactions from a Kaggle dataset to identify 
suspicious patterns using statistical techniques in Python. The pipeline covers the full 
data analysis workflow: loading, cleaning, outlier detection, behavioral grouping, 
feature engineering, risk scoring, and visualization.

---

## 📂 Dataset

- **Source:** Kaggle — Fraud Detection Dataset  
- **File:** `Fraud_Detection_Dataset.csv`  
- **Shape:** 51,000 rows × 12 columns  
- **Key columns:** Transaction_Amount, Transaction_Type, Time_of_Transaction, 
  Device_Used, Location, Previous_Fraudulent_Transactions, Account_Age, 
  Number_of_Transactions_Last_24H, Payment_Method, Fraudulent

---

## 🛠️ Libraries Used

| Library | Purpose |
|---|---|
| Pandas | Data loading, cleaning, grouping |
| NumPy | Z-score calculation, statistical measures |
| Matplotlib | Data visualization |

---

## 📋 Pipeline Summary

### 1. Loading & Exploring the Dataset
- Loaded CSV into a Pandas DataFrame
- Explored structure using `.head()`, `.tail()`, `.info()`, `.describe()`, `.shape`

### 2. Handling Missing Values
- Identified 5 columns with missing data (2,469–2,552 nulls each)
- Numeric columns (Transaction_Amount, Time_of_Transaction) → filled with **mean**
- Categorical columns (Device_Used, Location, Payment_Method) → filled with **mode**
- Removed duplicate rows with `.drop_duplicates()`

### 3. Outlier Detection (Z-Score)
- Computed Z-scores for `Transaction_Amount` and `Time_of_Transaction`
- Flagged transactions with |Z| > 3 as outliers
- **Result:** 508 outliers detected in Transaction_Amount; 0 in Time_of_Transaction

### 4. Grouping & Spending Behavior
- Grouped by `User_ID` → computed Avg_Spend, Max_Spend, Total_Transactions, Total_Spend
- Grouped by `Transaction_Type` → computed mean and count per type

### 5. Feature Engineering & Fraud Risk Score
Four new binary/continuous features engineered:

| Feature | Logic |
|---|---|
| `amount_zscore` | Z-score of Transaction_Amount (continuous) |
| `is_night` | 1 if transaction between 10 PM–6 AM |
| `has_prior_fraud` | 1 if Previous_Fraudulent_Transactions > 0 |
| `high_activity` | 1 if Number_of_Transactions_Last_24H > 10 |

Weighted fraud risk score formula:
