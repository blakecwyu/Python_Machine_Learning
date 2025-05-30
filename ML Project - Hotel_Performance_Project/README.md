# 🏨Machine Learning Project - Hotel Performance Analysis using Regression and Classification   
  
This project uses a synthetic 365-day dataset to explore and model hotel performance using machine learning techniques. It is divided into three parts:  
- **Regression** – Predict hotel revenue
- **Classification** – Predict whether occupancy is high (≥60%) or low (<60%)
- **Classification** – Classify the number of day types based on revenue and ADR to support price tiering
  
---  
## 📊Project Overview  
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
   Classify whether a day will have **high occupancy (≥60%)** or **low occupancy (<60%)** using:

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
   Use clustering to assess whether the **traditional day types**, weekday, weekend, holiday, are sufficient, or if **more refined day types** should be created to better support pricing strategies.  

   **Features**:
   - Room nights sold by market: FIT, GIT, Corp
   - Revenue by market: FIT, GIT, Corp

   **Model**:
   - K-Means Clustering
  
   **Goal**: Identify potential new day types (e.g., peak-season weekday, Saturday, event-driven weekend) based on performance patterns, to support more effective pricing tiers beyond the standard 3-category system.  

## 📁 Project Structure  
ML Project - Hotel_Performance_project/
├── Hotel Performance Prediction.ipynb # Jupyter notebook with full project (EDA, models, results)
├── Mock_Hotel_daily.csv # Synthetic dataset (365 days)
└── README.md # Project overview and usage
