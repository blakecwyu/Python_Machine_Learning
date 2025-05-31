# 🏨ML Project - Hotel Performance Analysis using Regression and Classification   
  
This project uses a synthetic 365-day dataset to explore and model hotel performance using machine learning techniques. It is divided into three parts:  
- **Regression** – Predict hotel revenue
- **Classification** – Predict whether occupancy is high (≥60%) or low (<60%)
- **Classification** – Classify the number of day types based on revenue and ADR to support price tiering

---
## 📊Project Overview 
This notebook-based project applies both regression and classification models to analyze hotel data. It aims to support better operational and pricing decisions by revealing patterns in demand, occupancy, and revenue across different day types and market segments.  

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
  - **Day type**: weekday, peak, or holiday (Peak includes Fridays to Sundays, the day before a holiday, and the last day of a holiday)   
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
   - Day type: Weekday, Peak, Holiday
   - Special event impact: Negative / None / Positive

   **Model**:
   - Decision Tree Classifier

   **Goal**: Identify key factors influencing occupancy fluctuations.
---  
3. Classification: Grouping Day Types for Pricing Tiers
   Use clustering to identify whether the **existing day types**, weekday, peak, holiday, are sufficient, or if more **refined day types** should be created to better support pricing strategies.  

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
⚠️ Note: Python 3.10 is recommended to ensure compatibility, but you can change the version if needed.  
Also, you can replace hotel-ml with any environment name you prefer.  
  
---
## 📷 Results  
- Correlation plots show that total revenue has a **positive relationship** with FIT room nights, occupancy rate, Saturdays, and holidays. Although GIT and Corporate room nights help fill low-demand days, they are **negatively correlated** with total revenue, likely due to lower average rates in those segments.  
  **This may support future strategies for room distribution across different market segments.**  
- Section 1, **Regression: Predicting Daily Revenue**  
  - Both **Linear Regression** and **Random Forest Regression** were used to predict revenue and average daily rate for future dates, providing insight to support pricing strategies.
- Section 2, **Classification: Predicting Occupancy Levels**  
  - The initial **Decision Tree** for occupancy classification was overfitting. After pruning and tuning, the model improved. Based on the final tree, we should pay closer attention to **Tuesdays during the beginning and end of each month**. However, the tree didn’t reveal highly informative patterns overall. This suggests that **day of month, day of week, day type, and special event** may not be sufficient or strongly correlated with occupancy.  
    **Based on domain experience and the correlation heatmap**, adding the **month** as a feature may improve classification, as **seasonality** plays a significant role in hospitality and tourism.
  - Currently, the occupancy classification includes all segments, but in practice, GIT and Corporate bookings are used to fill low-demand days and do not follow a consistent weekly pattern. Since GIT availability is seasonal and irregular, it may introduce noise into the model. A future version could classify based on FIT-only occupancy or revenue, providing a clearer signal for organic demand and helping to determine when GIT/Corp support is needed.
- Section 3, **Classification: Grouping Day Types for Pricing Tiers**  
  - **K-Means clustering** suggests there may be **6–8 distinct day types**, beyond the current weekday/peak/holiday categorization, supporting the idea of more granular pricing tiers.  
  From experience, we may consider separating **Saturdays** from other peak days, or defining **special weekday/peak patterns** during **seasonal breaks** (e.g., summer or winter holidays).  
  This refined day type classification could also provide **a new perspective** that may help improve the accuracy of both regression and occupancy classification models.  
- Visualizations include **correlation heatmaps**, **decision tree diagrams**, and **cluster visualizations** (see notebook).
  
---
## 🚀 Future Improvements  
- **Expand the dataset** by including data from multiple past years to capture seasonal trends and unusual patterns.  
- **Train and validate models with real-world data** to improve performance and generalizability.  
- **Refine the day type classification** to better reflect pricing behavior and occupancy patterns, potentially improving model accuracy.  
- **Incorporate external factors** such as weather conditions or citywide events, which may have a strong influence on occupancy and revenue.  
- **Leverage historical competitor performance data** (e.g., from benchmarking reports) to better position the hotel's pricing and predict market behavior.  
  *Note: This would require real-world data sources and is not applicable to the current synthetic dataset.*
- **Refine classification targets** by focusing on **FIT-only occupancy or revenue**, reducing noise from inconsistent GIT/Corp availability and better identifying truly low-demand days.  
- **Develop an interactive dashboard** to visualize trends, model outputs, and support decision-making by hotel management.  
- **Apply the models to a full future year** for forward-looking predictions to support pricing strategy and resource planning.
  
---
## 📄 License  
This project uses synthetic data for educational purposes and is not based on real operational hotel data.  
