#  Supply Chain Shipment Delay Prediction

![License](https://img.shields.io/badge/license-MIT-blue)

### Project Overview

This repository contains a comprehensive machine learning pipeline and supply-chain analysis for predicting delays in supply chain shipments. The focus is on health commodities, specifically Antiretroviral (ARV) and HIV lab shipments. The project aims to improve the efficiency and reliability of supply chains by accurately predicting potential delays and understanding the associated pricing and supply chain expenses.

___

<div align="center">
  <h3>Project Pipeline</h1>
  <img src="https://github.com/user-attachments/assets/0c61128f-babc-43f7-9568-819b26cb66c9" alt="Supply Chain Shipment Delay Prediction" width="600"/>
</div>

___

Key features of this project include:
- **Data Preprocessing:** Cleaning and preparing the data for analysis, including handling missing values and outliers.
- **Modeling:** Developing and training machine learning models to predict shipment delays.
- **Evaluation:** Assessing the performance of the models and optimizing them for better accuracy.
- **Visualization:** Providing insightful visualizations to understand the factors contributing to delays and their impact on costs.
- **Supply Chain Analysis:** In-depth analysis of the supply chain to identify bottlenecks and inefficiencies.

## Table of Contents
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Model Training](#model-training)
- [Model Evaluation & Selection](#model-evaluation--selection)
- [Key Findings](#key-findings)
- [Future Improvements](#future-improvements)
- [Contact](#contact)

## Dataset
The SCMS Delivery History Dataset is a comprehensive record of health commodity shipments managed by the Supply Chain Management System (SCMS) under the U.S. President's Emergency Plan for AIDS Relief (PEPFAR). This dataset encompasses procurement and distribution details of Antiretroviral (ARV) drugs and HIV laboratory supplies to various supported countries.

### Key Features:
- Shipment Mode: Method of transportation (e.g., Air, Sea, Land).
- Weight (Kilograms): Total weight of the shipment.
- Freight Cost (USD): Transportation cost in U.S. dollars.
- Scheduled and Actual Delivery Dates: Planned and actual dates of delivery.
- Vendor and Country Information: Details about suppliers and recipient countries.
- Product Category: Classification of commodities (e.g., ARVs, Lab Supplies).
- Delayed Shipment: Indicator of whether the shipment was delayed (1) or on-time (0).
  
Dataset Source: USAID SCMS Delivery History Dataset

# Methodology

This project leverages machine learning techniques to predict shipment delays within the supply chain. The methodology is structured into the following key phases:

## Data Exploration & Understanding
- Conducted Exploratory Data Analysis (EDA) to understand dataset structure, distributions, and patterns.
- Assessed missing values.
- Performed correlation analysis to identify relationships between features and delays.
- Engineered the Delayed Shipment target variable (1 = Delayed, 0 = On-Time).

### Target Distribution (Delayed)

![image](https://github.com/user-attachments/assets/77ea664a-2a84-4931-9ab7-d59250274514)

## Data Preprocessing

### Handling Missing Data
- Imputed missing numerical values.
- Filled missing categorical values using the most frequent category.

### Feature Encoding
- Converted categorical variables (e.g., shipment mode, Country) using one-hot encoding to maintain model interpretability.
- Applied Frequency Encoding to Vendor due to high cardinality.

### Feature Engineering
- Processing Time = PO Sent to Vendor Date - PQ First Sent to Client Date.
- Freight Cost per KG.

## Model Training
- Split the dataset into training (70%) and testing (30%) sets.

### Addressing Class Imbalance
- The dataset was highly imbalanced, with delayed shipments being a minority class.
- Applied SMOTE (Synthetic Minority Over-sampling Technique) to balance the dataset and prevent model bias towards on-time shipments.

### Implemented Machine Learning Models
- Random Forest Classifier
- XGBoost Classifier
- CatBoost Classifier
  
### Hyperparameter Tuning
- Applied Hyperparameter Tuning using RandomizedSearchCV to optimize model performance.
- Used Stratified K-Fold Cross-Validation to ensure unbiased evaluation and reduce variance.

## Model Evaluation & Selection
Assessed models based on multiple performance metrics:
- Accuracy, Precision, Recall, F1-score for balanced evaluation.
- AUC-ROC Score to measure model discriminatory power.
- Cohen’s Kappa & Matthews Correlation Coefficient for classification strength.

### SHAP (SHapley Additive Explanations) Analysis
SHAP analysis was used to interpret model predictions and assess feature importance:

![image](https://github.com/user-attachments/assets/85814511-0953-4524-a055-2f6f5927a71a)

### Test Set Results

| Model            |Test Accuracy |Test Precision | Test Recall |Test F1 Score |
|------------------|--------------|---------------|-------------|--------------|
| **Random Forest**| 86.7%        | 80.6%         | 85.0%       | 82.7%        |
| **XGBoost**      | 86.4%        | 80.6%         | 84.0%       | 82.3%        |
| **CatBoost**     | **87.6%**    | **82.2%**     | **85.5%**   | **83.8%**    |

Confusion Matrix Heatmaps:

![image](https://github.com/user-attachments/assets/51f30356-7b52-4ef1-b9be-b04471b1bb4f)
![image](https://github.com/user-attachments/assets/a56b500c-33e9-41e1-b2d9-aaefc37ddcdb)
![image](https://github.com/user-attachments/assets/aacf13a1-7afe-456d-920f-d361151aa572)

AUROC Curve & Precision-Recall Curve:

![image](https://github.com/user-attachments/assets/7a523bf6-f691-4f54-bdb5-11623633fe62)

### Best Model:
CatBoost Classifier

## Supply-Chain Analysis & Key Findings

### Delay Drivers & Risk Factors
- Shipment Mode, Vendor, Processing Times, Country, and the time of year were the most influential predictors of delays.
- Freight Cost (USD) and Weight (Kilograms) showed moderate impact, with higher-cost shipments being more prone to delays, possibly due to their complexity or urgency.

### Seasonal Impact on Delays
- Q4 (Oct-Dec) has the highest delay rate (12.8%), likely due to peak-season demand and supplier backlogs.
- Q2 (Apr-Jun) follows with 12.4% delays, suggesting mid-year procurement challenges.
- Seasonal forecasting could help predict high-delay periods and optimize shipment planning.

### Cost Implications of Delays
Delayed Shipments Incur Higher Costs:
- On-Time Shipments: $8,826 average freight cost.
- Delayed Shipments: $10,440 average freight cost (+18%).
- Higher costs may stem from expedited shipping, penalties, or additional storage fees.

### Freight Cost Varies Based On Country:
![newplot](https://github.com/user-attachments/assets/772c14c4-1340-4eed-9776-e82e50efe0f4)

### Shipment Mode Cost Implications
- Truck-based shipments are cheaper ($7,644) but have higher delays (16.1%).
- Air and Ocean shipments reduce delays but increase costs.
- Direct Drop fulfillment significantly reduces delays.

**Cost Breakdown by Shipment Mode**
|    | Shipment Mode   |   Freight Cost (USD) |   Unit Price |   Line Item Insurance (USD) |
|---:|:----------------|---------------------:|-------------:|----------------------------:|
|  0 | Air             |              8958.97 |     0.81666  |                     158.986 |
|  1 | Air Charter     |             15773.3  |     0.1874   |                     543.557 |
|  2 | Ocean           |             11086.6  |     0.15248  |                     567.809 |
|  3 | Truck           |              7644.1  |     0.251201 |                     294.259 |

## Future Improvements
- **Real-Time Data Integration:** Incorporate live tracking data for dynamic delay predictions.
- **Advanced Feature Engineering:** Explore time-series modeling for delay forecasting.
- **Deep Learning Approaches:** Investigate LSTM-based models for sequential shipment data analysis.
  
## Contact

- **Email:** [thecolbyrobinson@gmail.com](mailto:thecolbyrobinson@gmail.com)
- **LinkedIn:** [Colby Robinson](https://linkedin.com/in/colby-robinson-869148172)
