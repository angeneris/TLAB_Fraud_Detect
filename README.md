# Fraud Detection Model

## Overview

This project focuses on detecting fraudulent transactions using machine learning techniques. The dataset contains various transaction details, including account balances before and after transactions, transaction types, and timestamps. The goal is to identify fraudulent transactions based on patterns in the data.

<br>

## Dataset Description

The dataset includes the following features: <br>

**Step:** Represents time in hours since the start of data collection. <br>

**Type:** Type of transaction (e.g., CASH-IN, CASH-OUT, TRANSFER, etc.). <br>

**Amount:** Transaction amount. <br>

**NameOrig:** The ID of the origin account. <br> 

**OldBalanceOrg:** Balance of the origin account before the transaction. <br> 

**NewBalanceOrg:** Balance of the origin account after the transaction. <br> 

**NameDest** The ID of the destination account. <br> 

**OldBalanceDest:** Balance of the destination account before the transaction. <br> 

**NewBalanceDest:** Balance of the destination account after the transaction. <br> 

**IsFlaggedFraud:** A rule-based flag for transactions greater than 200,000. <br> 
 
**IsFraud:** Indicates whether the transaction was actually fraudulent. <br> 

<br>
<br>

## Objectives

**Understand Key Features:** Explore the relationships between transaction details and fraud occurrences to create better fraud detection<br>

**Feature Engineering:** Generate new features such as balance discrepancies and transaction frequency('step') <br>

**Data Visualization:** Use plots to identify key relevant features and patterns in fraudulent transactions <br>

**Machine Learning Modeling:** Address class imbalance, train and evaluate models to predict fraud more accurately <br> 

<br>
<br>

### Key Indicators of Fraud <br>

**Transaction Type:**
- Fraud is mostly found in "TRANSFER" and "CASH_OUT" transactions involving moving money between accounts.
- Transactions like "DEBIT", "PAYMENT", and "CASH_IN" are most likely not malignant.<br>

**Balance Changes:**
- The sender's (NameOrig) OldBalanceOrg is higher, but the NewBalanceOrg is suspiciously 0, meaning they transferred all their funds out
- The receiver's (NameDest) OldBalanceDest is 0 or unusually low, meaning it could be a newly created fraudulent account <br>

**Large Amounts:**
- Fraudulent transactions often involve large amounts being transferred quickly (step)
- The IsFlaggedFraud column may flag a transaction if it exceeds 200,000, but actual fraud can occur below this threshold- it's not clear what currency this is solely from the data so context is important <br>

**Destination Account Behavior:**
- If the destination account (NameDest) is frequently receiving large sums and quickly cashing out, it might be part of a fraud network
- May see the same accounts used multiple times or completely new accounts ($0 balance) to launder money <br>

**Repeated Transactions in a Short Time:**
- If multiple transactions occur within a short time from the same NameOrig, it could indicate an account being drained <br>

<br>
<br>


**Preprocessing:** <br>
- Handle missing values and data inconsistencies.<br> 

- Encode categorical variables (e.g., transaction types). <br>

- Handle Class Imbalance (Fraudulent Cases are minority class)
![alt text](image.png)


## Feature Engineering 

**Balance Discrepancy:**

- Compute Expected New Balance and compare it to NewBalanceOrg and NewBalanceDest.

- Formula: Expected New Balance = Old Balance - Amount.<br>

**Transaction Frequency:**

Count transactions per account within a given time window.<br>

**Anomaly Detection:**

Identify unusually large or frequent transactions. <br>

**Exploratory Data Analysis (EDA)** 

Correlation Analysis: Check relationships between numerical features and fraud occurrence. <br>

Pair Plots: Visualize interactions between multiple numerical features.<br>

Box Plots & Histograms: Examine distributions of transaction amounts and balances.<br>
<br>
## Model Development


## **Model Selection**
- Evaluate logistic regression, decision trees, random forests <br>

- **Evaluation Metrics:** Precision, recall, F1-score, and AUC-ROC to assess model performance.

![alt text](image-1.png)




Fraud Detection Model: Hypothesis, EDA, Preprocessing & Model Building

Project Overview

This project aims to develop a fraud detection model using a dataset of financial transactions. The goal is to analyze fraud patterns, clean and preprocess the data, and build multiple machine learning models to accurately detect fraudulent transactions while minimizing false positives and false negatives.

## 1. Hypothesis Formulation & Exploratory Data Analysis (EDA)

### Hypothesis:
- Fraudulent transactions show distinct patterns related to amount, balance changes, and transaction type ( e.g large transfers outside of the origin)
- The destination account balance may behave differently in fraud cases (e.g more frequently across multiple origins)
- Certain transaction types (e.g., cash-outs, transfers) may be more fraud-prone.
- Large transactions might be flagged as fraud more frequently, but not all large transactions are fraudulent

### EDA & Initial Insights
- Box Plots & Log Scale Transformations
The dataset contains a wide range of transaction amounts, making it necessary to use log transformation for better visualization.
Outliers are prevalent in legitimate transactions, as expected.

- Feature Correlation
Variables like OldbalanceDest and NewbalanceDest may contain fraud-specific patterns.
Fraudulent transactions often involve unexpected balance shifts after a transaction.

## 2. Data Cleaning & Preprocessing

Key Preprocessing Steps
✅ Categorical variables encoded using One-Hot Encoding
✅ Dropped redundant features to prevent multicollinearity

### Addressing Class Imbalance
The dataset has a severe imbalance:
552,439 legitimate transactions (Class 0)
1,643 fraud transactions (Class 1)
The model is at risk of favoring non-fraud predictions, missing actual fraud cases.
Resampling techniques (Oversampling fraud cases via SMOTE and undersampling the majority class) were applied.

## 3. Model Generation & Evaluation

**Logistic Regression Model (Baseline)***
✅ Precision (Fraud = 0.93) → The model correctly predicts fraud 93% of the time.
✅ Recall (Fraud = 0.60) → The model only catches 60% of real fraud cases, meaning 40% of fraud cases are missed.
✅ F1-score (Fraud = 0.73) → The imbalance affects recall, lowering the F1-score.

🔴 False Negatives (missed fraud cases) = 665 → A major issue.
🟢 False Positives (legitimate transactions wrongly flagged) = 72 → Relatively low.

**Confusion Matrix (Logistic Regression)**

![alt text](image-2.png)

Goal: Improve fraud detection using a non-linear decision boundary.
Evaluation Plan:
Precision, Recall, F1-score comparison with Logistic Regression.
ROC-AUC Curve to assess model performance.

SVM may not be ideal- runs too slow and can not finish computing in time 

### Planned: Random Forest Model
- Handles class imbalance well.
- Can model complex relationships between features.
- Provides feature importance insights.

### Next Steps:
- Train a Random Forest model and compare its precision, recall, and F1-score to previous models
- Evaluate feature importance to identify the most critical fraud indicators

## 4. Conclusion & Next Steps

✅ EDA confirmed key fraud patterns, especially in transaction type and balance shifts.
✅ Logistic Regression performed well in precision but struggled with recall.
- SVM model is pending evaluation – expected to improve fraud detection
- Random Forest will be tested for feature importance & better fraud detection

**Future Work:**
Optimize threshold tuning to balance precision and recall
Experimenting with ensemble methods (stacking models for better performance)