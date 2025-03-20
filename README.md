#  Supply Chain Shipment Delay Prediction

## Dataset
The SCMS Delivery History Dataset is a comprehensive record of health commodity shipments managed by the Supply Chain Management System (SCMS) under the U.S. President's Emergency Plan for AIDS Relief (PEPFAR). This dataset encompasses procurement and distribution details of Antiretroviral (ARV) drugs and HIV laboratory supplies to various supported countries.

Key Features:

-Shipment Mode: Method of transportation (e.g., Air, Sea, Land).
-Weight (Kilograms): Total weight of the shipment.
-Freight Cost (USD): Transportation cost in U.S. dollars.
-Scheduled and Actual Delivery Dates: Planned and actual dates of delivery.
-Vendor and Country Information: Details about suppliers and recipient countries.
-Product Category: Classification of commodities (e.g., ARVs, Lab Supplies).
-Delayed Shipment: Indicator of whether the shipment was delayed (1) or on-time (0).

Dataset Source: USAID SCMS Delivery History Dataset

## Methodology

This project leverages machine learning techniques to predict shipment delays within the supply chain. The methodology is structured into the following key phases:

Data Exploration & Understanding

-Conducted Exploratory Data Analysis (EDA) to understand dataset structure, distributions, and patterns.

-Assessed missing values

-Performed correlation analysis to identify relationships between features and delays.

-Engineered the Delayed Shipment target variable (1 = Delayed, 0 = On-Time)

### Target Distribution (Delayed)

![image](https://github.com/user-attachments/assets/77ea664a-2a84-4931-9ab7-d59250274514)


### Data preprocessing

Handling Missing Data:
-Imputed missing numerical values
-Filled missing categorical values using the most frequent category.

Feature Encoding:
-Converted categorical variables (e.g., shipment mode, Country) using one-hot encoding to maintain model interpretability.
-Frequency Encoding applied to [Vendor] due to high cardinality.

Feature Engineering:
-Processing Time = PO Sent to Vendor Date - PQ First Sent to Client Date.
-Freight Cost per KG

### Addressing Class Imbalance
-The dataset was highly imbalanced, with delayed shipments being a minority class.

-Applied SMOTE (Synthetic Minority Over-sampling Technique) to balance the dataset and prevent model bias towards on-time shipments.

### Model Training
-Split dataset into training (70%) and testing (30%) sets.

Implemented three machine learning models:
  -Random Forest Classifier

  -XGBoost Classifier

  -CatBoost Classifier

-Applied Hyperparameter Tuning using RandomizedSearchCV to optimize model performance.
-Used Stratified K-Fold Cross-Validation to ensure unbiased evaluation and reduce variance.

### Model Evaluation & Selection
Assessed models based on multiple performance metrics:
-Accuracy, Precision, Recall, F1-score for balanced evaluation.
-AUC-ROC Score to measure model discriminatory power.
-Cohen’s Kappa & Matthews Correlation Coefficient for classification strength.

est Set Results for All Models

Model

Test Accuracy

Test Precision

Test Recall

Test F1 Score

Random Forest

86.7%

80.6%

85.0%

82.7%

XGBoost

86.4%

80.6%

84.0%

82.3%

CatBoost

87.6%

82.2%

85.5%

83.8%
