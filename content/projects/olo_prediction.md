---
date: '2025-08-01T20:40:23+08:00'
draft: false
title: 'Project: O2O Coupon Usage Prediction'
tags: ['XGBoost']
categories: ['Machine Learning']
---
# O2O Coupon Usage Prediction

### Project Summary

In this project, I developed a machine learning model to predict whether customers would redeem coupons on an O2O (Online-to-Offline) platform. By engineering over 30 features from user and merchant behavior and employing a LightGBM classifier, the model provides valuable insights into the key drivers of coupon redemption, enabling more targeted and effective marketing strategies.

---

### The Business Challenge

O2O platforms frequently issue coupons to attract customers and drive sales. However, untargeted coupon distribution can be costly and inefficient. The core challenge is to accurately predict which users are most likely to use a given coupon, enabling more effective marketing campaigns and maximizing return on investment.

---

### My Approach & Methodology

#### 1. Data Preprocessing & Feature Engineering

The project's success hinged on transforming raw transactional data into meaningful features. My process included:

*   **Data Cleaning:** Standardized date formats and converted complex discount information (e.g., "20:1") into numerical rates.
*   **Feature Creation:** Engineered a comprehensive set of over 30 features to capture behavioral patterns, including:
    *   **User Features:** Purchase frequency, average discount rate preference, and activity level.
    *   **Merchant Features:** Popularity, overall coupon redemption rate, and average distance to customers.
    *   **User-Merchant Interaction Features:** A user's specific history with a particular merchant.
*   **Time-Window Strategy:** To prevent data leakage and simulate a real-world prediction scenario, I implemented a time-window approach, calculating features on historical data to predict future behavior.

#### 2. Modeling and Evaluation

*   **Model Selection:** I chose **LightGBM**, a powerful and efficient gradient boosting framework, for the binary classification task due to its speed and ability to handle large datasets and missing values.
*   **Training & Validation:** The model was trained and validated using a time-series split, ensuring it generalizes well over time. The primary evaluation metric was **AUC (Area Under the ROC Curve)**, which is well-suited for imbalanced classification problems like this one.

---

### Results and Key Insights

The final model demonstrated strong predictive power. Analysis of the model's feature importances revealed several key insights into customer behavior:

*   **Distance is Critical:** The distance between a user and a merchant was one of the most significant predictors.
*   **Merchant Popularity Matters:** The merchant's overall coupon redemption rate and the total number of coupons they've issued were highly influential.
*   **Discount Attractiveness:** The coupon's discount rate and the threshold for redemption (e.g., the 'spend X to save Y' value) were also key drivers.

These insights can directly inform business strategy by helping to target users who are geographically close to merchants offering attractive and popular deals.

### Technologies Used

*   **Programming Language:** Python
*   **Libraries:** Pandas, NumPy, Scikit-learn, LightGBM, Matplotlib, Seaborn


## Project Link
https://github.com/lijinxuan1101/ml_o2o_prediction