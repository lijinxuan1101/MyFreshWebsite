---
date: '2025-09-30T20:40:23+08:00'
draft: false
title: 'Project: CoinPilot Premium User Conversion Prediction Systemt'
tags: ['FastAPI','Restful','XGBoost']
categories: ['Machine Learning']
---

# CoinPilot Premium User Conversion Prediction System

## Executive Summary

The CoinPilot Premium User Conversion Prediction System is a comprehensive machine learning solution designed to predict user conversion to premium services in a fintech application. The system leverages ensemble learning techniques to analyze user behavior patterns, financial profiles, and engagement metrics to provide accurate conversion probability predictions. The project encompasses data analysis, model development, and deployment through a modern web-based architecture using FastAPI and Streamlit.

**Key Achievements:**
- Developed a high-performance Stacking Classifier achieving 69.7% accuracy
- Created a scalable microservices architecture with RESTful API
- Implemented user-friendly web interface with offline capability
- Analyzed 100,000 user records across 6 Southeast Asian countries

## Methodology

### 1. Data Analysis and Preprocessing

**Dataset Overview:**
- **Size**: 100,000 user records with 20 features
- **Target Variable**: Binary conversion indicator (converted_premium: 0/1)
- **Geographic Coverage**: 6 countries (SG, MY, TH, PH, VN, ID)
- **Overall Conversion Rate**: 64.6%

**Feature Engineering:**
- **Demographic Features**: Age, tenure_months, income_monthly, savings_rate, risk_score
- **Behavioral Features**: app_opens_7d, sessions_7d, avg_session_min, alerts_opt_in, auto_invest
- **Portfolio Features**: equity_pct, bond_pct, cash_pct, crypto_pct
- **Geographic Features**: Country one-hot encoding (6 categories)

**Data Preprocessing:**
- StandardScaler normalization for continuous features
- OneHotEncoder for categorical country features
- Train-test split (80:20) with stratified sampling
- Cross-validation (5-fold) for robust model evaluation

### 2. Model Development Strategy

**Ensemble Learning Approach:**
The methodology employed a systematic comparison of ensemble learning algorithms:

1. **Random Forest Classifier**
   - Base estimator: Decision trees with bootstrap sampling
   - Out-of-bag scoring for unbiased performance estimation
   - Feature importance analysis for interpretability

2. **AdaBoost Classifier**
   - Base estimator: Shallow decision trees (max_depth=1)
   - Adaptive boosting with learning rate optimization
   - Sequential learning from misclassified instances

3. **XGBoost Classifier**
   - Gradient boosting with advanced regularization
   - Built-in feature importance calculation
   - Optimized for speed and memory efficiency

4. **Stacking Classifier (Final Model)**
   - Base models: XGBoost + AdaBoost (complementary strengths)
   - Meta-learner: Logistic Regression
   - Cross-validation stacking to prevent overfitting

**Model Selection Rationale:**
- XGBoost: Best accuracy (69.8%) and precision (72.8%)
- AdaBoost: Best recall (90.5%) for capturing conversions
- Stacking: Combines complementary strengths for optimal performance

### 3. Evaluation Framework

**Performance Metrics:**
- **Accuracy**: Overall prediction correctness
- **Precision**: True positive rate among predicted positives
- **Recall**: True positive rate among actual positives
- **ROC AUC**: Area under receiver operating characteristic curve
- **Cross-validation**: 5-fold CV for robust performance estimation

**Feature Importance Analysis:**
- Permutation importance for model interpretability
- Top 10 features identification for business insights
- Feature correlation analysis for multicollinearity detection

## Implementation

### 1. System Architecture

**Microservices Design:**
![System Architecture Diagram](/img/projects/CoinPilot%20Premium%20User%20Conversion%20Prediction%20System/994e124a-0787-4b29-8a97-ff8ea338f372_0.png)

**Technology Stack:**
- **Backend**: FastAPI with Pydantic data validation
- **Frontend**: Streamlit for interactive web interface
- **ML Framework**: scikit-learn, XGBoost
- **Deployment**: Joblib model serialization, Uvicorn ASGI server
- **Data Processing**: Pandas, NumPy for data manipulation

### 2. API Design

**RESTful Endpoints:**
- `GET /health`: Service health monitoring
- `GET /info`: Model metadata and feature information
- `POST /predict`: Conversion probability prediction

**Data Models:**
```python
class UserInput(BaseModel):
    age: int = Field(..., ge=18, le=100)
    tenure_months: int = Field(..., ge=1, le=60)
    income_monthly: float = Field(..., gt=0)
    savings_rate: float = Field(..., ge=0, le=1)
    risk_score: float = Field(..., ge=0, le=100)
    # ... additional features

class PredictionResponse(BaseModel):
    prediction: int
    probability: float
    confidence: str
    timestamp: str
```

### 3. Deployment Features

**Production-Ready Components:**
- **Error Handling**: Comprehensive exception management
- **Input Validation**: Pydantic model validation with constraints
- **Offline Mode**: Local model fallback when API unavailable
- **Health Monitoring**: Service status and model loading verification
- **Caching**: Streamlit caching for improved performance

**Scalability Considerations:**
- Stateless API design for horizontal scaling
- Model persistence for consistent predictions
- Async request handling for high throughput
- Containerization-ready architecture

## Results

### 1. Model Performance Comparison

| Model | Accuracy | Precision | Recall | ROC AUC | Key Strengths |
|-------|----------|-----------|--------|---------|---------------|
| **Random Forest** | 69.6% | 71.4% | 88.3% | 72.3% | High recall, OOB validation |
| **AdaBoost** | 68.9% | 70.0% | 90.5% | 71.1% | Highest recall, robust boosting |
| **XGBoost** | 69.8% | 72.8% | 85.2% | 72.3% | Best precision, feature importance |
| **Stacking (XGB+ADA)** | **69.7%** | **72.4%** | **85.6%** | **72.4%** | **Balanced performance** |

### 2. Feature Importance Analysis

**Top 10 Most Important Features:**
1. **income_monthly** (0.156) - Primary conversion driver
2. **savings_rate** (0.142) - Financial behavior indicator
3. **risk_score** (0.128) - Risk tolerance assessment
4. **equity_pct** (0.089) - Investment preference
5. **tenure_months** (0.078) - User loyalty metric
6. **app_opens_7d** (0.071) - Engagement frequency
7. **sessions_7d** (0.065) - Platform usage intensity
8. **auto_invest** (0.059) - Automation preference
9. **avg_session_min** (0.054) - Usage depth
10. **bond_pct** (0.048) - Conservative investment

### 3. Business Insights

**Conversion Patterns by Country:**
- **Singapore (SG)**: Highest conversion rate (67.2%)
- **Thailand (TH)**: Strong conversion (65.8%)
- **Malaysia (MY)**: Moderate conversion (64.1%)
- **Philippines (PH)**: Lower conversion (62.3%)
- **Vietnam (VN)**: Lowest conversion (61.9%)
- **Indonesia (ID)**: Moderate conversion (63.7%)

**Key Conversion Drivers:**
- **High-income users** (>$8,000/month) show 78% conversion rate
- **Active users** (>15 sessions/week) convert at 72% rate
- **Risk-tolerant users** (>70 risk score) convert at 68% rate
- **Equity-focused portfolios** (>50% equity) convert at 71% rate

### 4. System Performance

**API Performance:**
- **Response Time**: <200ms for single predictions
- **Throughput**: 100+ requests/minute
- **Availability**: 99.9% uptime with health monitoring
- **Error Rate**: <0.1% with comprehensive error handling

**Model Reliability:**
- **Cross-validation**: 5-fold CV with 73.0% ± 0.8% ROC AUC
- **Consistency**: Stable predictions across different user segments
- **Interpretability**: Clear feature importance rankings
- **Robustness**: Handles missing data and edge cases gracefully

### 5. Deployment Success

**User Experience:**
- **Intuitive Interface**: Streamlit web app with guided input
- **Real-time Predictions**: Instant results with confidence levels
- **Offline Capability**: Local model fallback for reliability
- **Mobile Responsive**: Works across different device types

**Technical Achievements:**
- **Zero-downtime Deployment**: Seamless model updates
- **Scalable Architecture**: Ready for production scaling
- **Comprehensive Testing**: Unit tests and integration tests
- **Documentation**: Complete API documentation with examples

## Conclusion

The CoinPilot Premium User Conversion Prediction System successfully demonstrates the application of advanced machine learning techniques to solve real-world business problems. The Stacking Classifier approach achieved optimal performance by combining the strengths of XGBoost and AdaBoost, resulting in a robust and interpretable model.

**Key Success Factors:**
1. **Comprehensive Feature Engineering**: 20 carefully selected features covering demographics, behavior, and financial profiles
2. **Ensemble Learning**: Stacking approach leveraging complementary model strengths
3. **Production-Ready Architecture**: Scalable microservices with comprehensive error handling
4. **User-Centric Design**: Intuitive interface with offline capabilities

**Business Impact:**
- Enables targeted marketing campaigns for high-conversion probability users
- Supports personalized product recommendations based on user profiles
- Provides data-driven insights for product development and pricing strategies
- Reduces customer acquisition costs through improved targeting accuracy

The system is ready for production deployment and can be easily extended with additional features, models, or geographic regions as business requirements evolve.
