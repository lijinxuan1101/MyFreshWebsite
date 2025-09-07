---
date: '2024-02-04T20:40:23+08:00'
draft: false
# 2024MCN
title: 'Competition: 2023 Huashu Cup Model Construction Competition'
description: 'Model Construction Competition'
tags: []
categories: []
---
# A Machine Learning and Evaluation Framework for Analyzing the Impact of Maternal Health on Infant Development

## Summary
This study establishes machine learning models to analyze correlations between **infant behavior characteristics**, **maternal physical and mental health indicators**, and **infant sleep quality**, and proposes treatment strategies.

### Problem 1
- Preprocessed infant behavior features and maternal health indicators.  
- Designed hierarchical statistics for multiple variables: **ANOVA** for continuous variables and **logistic regression** for categorical variables.  
- Conducted **correlation analysis** and **multifactor ANOVA**, finding significant relationships:  
  - Maternal age ↔ infant sleep patterns & behavior features  
  - Maternal gestation period ↔ infant wake-up frequency  
  - Maternal HADS score ↔ infant wake-up frequency, total sleep time, behavior features  
  - Maternal EPDS score ↔ infant wake-up frequency, total sleep time  
- No significant effects were found for other indicators.

### Problem 2
- Trained models using **logistic regression, Random Forest, Neural Networks, and XGBoost**.  
- Selected **XGBoost** as the best-performing model (**highest accuracy**).  
- Optimized model parameters using **loss function minimization** and **cross-validation**.  
- Predicted the behavior types for the last 20 infant samples using the trained XGBoost model.

### Problem 3
- Combined **genetic algorithms** with the XGBoost model from Problem 2 to generate treatment plans.  
- Final treatment costs:  
  - Moderate type: **695 CNY**  
  - Quiet type: **10,448 CNY**

### Problem 4
- Evaluated infant sleep quality using the **CRITIC method**.  
- Established a **comprehensive sleep quality ranking system** using **rank-sum ratio evaluation**, classifying sleep quality as excellent, good, medium, or poor.  
- Determined indicator weights with the CRITIC method.  
- Trained a **Random Forest model** to associate comprehensive infant sleep quality with maternal health indicators, predicting sleep quality for the last 20 infant samples.

### Problem 5
- Based on the evaluation and association models from Problem 4, calculated the initial sleep quality of **infant #238**.  
- Applied the same approach as Problem 3, updating maternal indicators in the association model to generate a **new treatment plan**:  
  - Moderate type (sleep quality: excellent), **minimum cost: 8,699 CNY**
---
**Keywords:** XGBoost, Genetic Algorithm, CRITIC Method, Rank-Sum Ratio Evaluation, Random Forest, Association Model

# View Full Paper
[A Machine Learning and Evaluation Framework for Analyzing the Impact of Maternal Health on Infant Development](/papers/2024huashucup.pdf)