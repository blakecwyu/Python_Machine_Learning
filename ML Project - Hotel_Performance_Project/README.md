This project is a practice to train different models and predict hotel performances.  
The dataset is an one year long hotel performance data that mimicing the real world situation with random number adjustments. (Currency: NT$)  
Models using in this project: Multiple Linear Regression, Random Forest Regression, Decision Tree Classifier, K-mean, GridSearchCV  
這個專案使用一個模仿現實飯店營運的每日數據資料，來練習及預測飯店績效，數據長度為一年共365天。  
使用模型: Multiple Linear Regression, Random Forest Regression, Decision Tree Classifier, K-mean, GridSearchCV  

Machine Learning Project  
Hotel Performance Analysis using Regression and Classification  
  
This project uses a synthetic 365-day dataset to explore and model hotel performance using machine learning techniques. It is divided into three parts:  
- **Regression** – Predict hotel revenue
- **Classification** – Predict whether occupancy is high (>60%) or low (≤60%)
- **Classification** – Classify the number of day types based on revenue and ADR to support price tiering
  
---  
Project Overview  
1. Regression: Predicting Daily Revenue  
   Use multiple regression models to predict **total daily revenue** using:   
   
   **Features used**:
   - Room nights sold by market: FIT, GIT, Corp
   - Occupancy rate
   - Day of week (Monday–Sunday)
  
   **Models**:
   - Multiple Linear Regression
   - Random Forest Regression
  
   **Goal**: Estimate expected revenue based on operational and calendar variables.  
---  
2. Classification: Predicting Occupancy Levels
   Classify whether a day will have **high occupancy (>60%)** or **low occupancy (≤60%)** using:

   **Features**:
   - Day of the month (1st–31st)
   - Day of week (Monday–Sunday)
   - Day type: Weekday, Weekend, Holiday
   - Special event impact: Negative / None / Positive

   **Model**:
   - Decision Tree Classifier

   **Goal**: Identify key factors influencing occupancy fluctuations.
---
3. Classification: Grouping Day Types for Pricing Tiers
   Use clustering to determine how many **distinct day types** (e.g., low-, mid-, high-tier) should exist based on:

   **Features**:
   - Room nights sold by market: FIT, GIT, Corp
   - Revenue by market: FIT, GIT, Corp

   **Model**:
   - K-Means Clustering
  
   **Goal**: Support pricing strategy by grouping similar performance days.
   
