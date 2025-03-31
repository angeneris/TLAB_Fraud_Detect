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

## Feature Engineering Ideas

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

**Preprocessing:** <br>
- Handle missing values and data inconsistencies.<br> 

- Encode categorical variables (e.g., transaction types). <br>

**Model Selection:** Evaluate logistic regression, decision trees, random forests <br>

**Evaluation Metrics:** Precision, recall, F1-score, and AUC-ROC to assess model performance.
