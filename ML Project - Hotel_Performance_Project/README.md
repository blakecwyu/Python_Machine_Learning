# 🏨ML Project - Hotel Performance Analysis using Regression and Classification   
  
## 📊Project Overview 
This project uses a synthetic 365-day dataset to explore and model hotel performance using machine learning techniques. It is divided into three parts:  
- **Regression** – Predict hotel revenue
- **Classification** – Predict whether occupancy is high (≥60%) or low (<60%)
- **Classification** – Classify the number of day types based on revenue and ADR to support price tiering
  
---  
## 🧪 Dataset  
- The dataset is **synthetic**, generated to simulate realistic hotel performance across 365 days.
- Fields include:
  - **Date** column (used to derive day in month)
  - **Day of week** column (explicitly provided)  
  - **Room nights sold** by market segment:  
    - **FIT**, **GIT**, **Corporate**  
    - Plus a **Total** column (sum of all segments) — **not used in modeling**  
  - **Revenue** by market segment:  
    - **FIT**, **GIT**, **Corporate**  
    - Plus a **Total** column — **not used in modeling**  
  - **Occupancy rate**  
  - **Day type**: weekday, weekend, or holiday    
  - **Special events** with negative, none, or positive impact  

--- 
## 🔬 Project Sections
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

---  
## 📁 Project Structure  
ML Project - Hotel_Performance_project/  
├── Hotel Performance Prediction.ipynb # Jupyter notebook with full project (EDA, models, results)  
├── Mock_Hotel_daily.csv # Synthetic dataset (365 days)  
├── README.md # Project overview and usage  
└── requirements.txt # Python dependencies for pip installation  

---  
## 🔧 Installation  
### Option 1: With pip  
```bash  
pip install -r requirements.txt  
```
### Option 2: With Conda  
You can manually create a conda environment and install packages listed in requirements.txt:  
```
conda create -n hotel-ml python=3.10  
conda activate hotel-ml  
pip install -r requirements.txt
```
⚠️ Note: Python 3.10 is recommended to ensure compatibility,
but you can change the version if needed.
Also, you can replace hotel-ml with any environment name you prefer.
