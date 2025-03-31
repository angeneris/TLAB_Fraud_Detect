# Fraud Detection Model

## Overview

This project focuses on detecting fraudulent transactions using machine learning techniques. The dataset contains various transaction details, including account balances before and after transactions, transaction types, and timestamps. The goal is to identify fraudulent transactions based on patterns in the data.
<br>
## Dataset Description

The dataset includes the following features: <br>

Step: Represents time in hours since the start of data collection. <br>

Type: Type of transaction (e.g., CASH-IN, CASH-OUT, TRANSFER, etc.). <br>

Amount: Transaction amount. <br>

NameOrig: The ID of the origin account. <br> 

OldBalanceOrg: Balance of the origin account before the transaction. <br> 

NewBalanceOrg: Balance of the origin account after the transaction. <br> 

NameDest: The ID of the destination account. <br> 

OldBalanceDest: Balance of the destination account before the transaction. <br> 

NewBalanceDest: Balance of the destination account after the transaction. <br> 

IsFlaggedFraud: A rule-based flag for transactions greater than 200,000. <br> 
 
IsFraud: Indicates whether the transaction was actually fraudulent. <br> 

<br>
## Objectives

Understand Key Features: Explore the relationships between transaction details and fraud occurrences.<br>

Feature Engineering: Generate new features such as balance discrepancies and transaction frequency. <br>

Data Visualization: Use plots to identify patterns in fraudulent transactions. <br>

Machine Learning Modeling: Train and evaluate models to predict fraud.<br> 
<br>

## Feature Engineering Ideas

**Balance Discrepancy:**

-Compute Expected New Balance and compare it to NewBalanceOrg and NewBalanceDest.

-Formula: Expected New Balance = Old Balance - Amount.<br>


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

**Model Selection:** Evaluate logistic regression, decision trees, random forests, and gradient boosting models. <br>

**Evaluation Metrics:** Precision, recall, F1-score, and AUC-ROC to assess model performance.
