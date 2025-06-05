📘 **中文版本請往下滑動查看**｜[Scroll down for Mandarin version]  
  
# 🏨ML Project - Hotel Performance Analysis using Regression and Classification   
  
## 📊Project Overview  
This notebook-based project applies machine learning techniques to support better operational and pricing decisions by revealing patterns in demand, occupancy, and revenue across different day types and market segments. It is divided into three parts:  
- **Regression** – Predict hotel revenue  
- **Classification** – Predict whether occupancy is high (≥60%) or low (<60%)  
- **Classification** – Classify the number of day types based on revenue and ADR to support price tiering.

The analysis is based on a synthetic dataset simulating realistic hotel performance over a full year (365 days).  
  
---  
## 🧪 Dataset  
- The dataset is **synthetic**, generated to simulate realistic hotel performance across 365 days.  
- Fields include:  
  - `date`: Calender date in 2023 (used to derive day and month values)  
  - `dayofweek`: Day name (e.g., Monday–Sunday)
  - `daytype`: Weekday, Peak, or Holiday  
    - *Peak* includes Fridays to Sundays, the day before a holiday, and the last day of a holiday  
    - *Holiday* refers to holidays that span **more than one day**, typically combining with a weekend. One-day holidays are not labeled as "Holiday" in this field.  
  - `special_event`: Indicates whether a special event occurs (negative, none, or positive)  
  - `rn_fit, rn_git, rn_corp`: Room nights sold in **FIT**(Free Independent Traveler), **GIT**(Group Inclusive Tour), **Corporate** market segments  
  - `adr_fit, adr_git, adr_corp`: Average Daily Rate (ADR) in each market segments  
  - `rev_fit, rev_git, rev_corp`: Revenue generated in each market segments  
  - `occ`: Occupancy rate (percentage)  
  - `rn_ttl, adr_ttl, rev_ttl`: Total values across all market segments  

*Note: ADR (Average Daily Rate) = Revenue / Room Nights Sold*  

--- 
## 🔬 Project Sections
1. Regression: Predicting Hotel Performance  
   Use multiple regression models to predict **total daily revenue**   
   
   **Features**:
   - Room nights sold by market: FIT, GIT, Corp
   - Occupancy rate
   - Day of week (Monday–Sunday)
  
   **Models**:
   - Multiple Linear Regression
   - Random Forest Regression
  
   **Goal**: Estimate expected revenue based on operational and calendar variables.  
---  
2. Classification: Predicting Occupancy Levels  
   Classify whether a day will have **high occupancy (≥60%)** or **low occupancy (<60%)**  

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
- Correlation heatmap shows that total revenue has a **positive relationship** with FIT room nights, occupancy rate, Saturdays, and Holidays. Although GIT and Corporate room nights help fill low-demand days, they are **negatively correlated** with total revenue, likely due to lower average rates in those segments.  
  **This insight may support future strategies for room distribution across different market segments.**  
- Section 1: **Regression - Predicting Daily Revenue**  
  - Both **Linear Regression** and **Random Forest Regression** were used to predict revenue and average daily rate for future dates, providing insight to support pricing strategies.
- Section 2: **Classification - Predicting Occupancy Levels**  
  - The initial **Decision Tree** for occupancy classification showed overfitting. After pruning and tuning, the model improved. Based on the final tree, we should pay closer attention to **Tuesdays during the beginning and end of each month**.  
  - However, the tree didn’t reveal highly informative patterns overall. This suggests that **day of month, day of week, day type, and special event** may not be sufficient or strongly correlated with occupancy. Based on **domain experience and the correlation heatmap**, adding the **month** as a feature may improve classification, as **seasonality** plays a significant role in hospitality and tourism.  
  - Currently, the occupancy classification includes **all segments**, but in practice, **GIT and Corporate bookings** are used to fill low-demand days and do not follow a consistent weekly pattern. Since GIT availability is seasonal and irregular, it may introduce noise into the model. A future version could classify based on **FIT-only occupancy or revenue**, providing a clearer signal for organic demand and helping to determine when **GIT/Corp support** is needed.
- Section 3: **Classification - Grouping Day Types for Pricing Tiers**  
  - **K-Means clustering** suggests there may be **6–8 distinct day types**, beyond the current weekday/peak/holiday categorization, supporting the idea of more granular pricing tiers.
  - Based on **domain experience**, we may consider separating **Saturdays** from other peak days, or defining **special weekday/peak patterns** during **seasonal breaks** (e.g., summer or winter holidays). This refined day type classification could also provide **a new perspective** that may help improve the accuracy of both regression and occupancy classification models.  
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
This project uses synthetic data generated solely for educational and demonstration purposes. It does not reflect real hotel operations or confidential business information.  
All analysis and code are intended for non-commercial academic use.  

---
   
   
   
# 🏨機器學習專案 - 使用迴歸模型與分群模型分析飯店營運績效  
## 📊專案概述  
本專案使用 Jupyter Notebook，透過機器學習分析不同日別與市場區隔下的需求、住房率與營收趨勢，協助改善營運與訂價策略。專案分為三個部分：  
- **迴歸模型** - 使用線性迴歸與隨機森林預測每日營收與平均房價。  
- **分群模型** – 使用決策樹分類每日住房率為高（≥60%）或低（<60%）。  
- **分群模型** – 使用 K-Means 分群找出不同「日類型」的數量，以支援更細緻的定價分層策略。  

本分析使用模擬飯店一整年的營運情形（365天）的合成資料，具備接近實際營運邏輯的結構與變異。  
  
---
## 🧪 資料集  
- 資料為合成資料，模擬 2023 年度 365 天的飯店營運表現。  
- 欄位包含：  
  - `date`: 2023年日期(用以推導月份與日期)  
  - `dayofweek`: 星期幾(例如：星期一～星期日)  
  - `daytype`: 日別，平日、旺日、假日  
    - *旺日* 包含星期五至星期日、假日前一天、假期最後一天、單日假日  
    - *假日* 指連續假期(不包含只有一天的國定假日)  
  - `special_event`: 是否有特殊事件(負面、無、正面)  
  - `rn_fit, rn_git, rn_corp`: 各市場**FIT**(散客)、**GIT**(團客)、**Corp**(商務)房晚數  
  - `adr_fit, adr_git, adr_corp`: 各市場平均房價(ADR)  
  - `rev_fit, rev_git, rev_corp`: 各市場營收  
  - `occ`: 住房率(百分比)  
  - `rn_ttl, adr_ttl, rev_ttl`: 各市場總和  

*註：平均房價 = 營收 / 房晚數*  

--- 
## 🔬 專案內容
1. 迴歸分析：預測飯店績效  
   使用兩種迴歸分析來預測**每日營收**   
   
   **Features**:
   - `rn_fit, rn_git, rn_corp` 各市場房晚數: FIT, GIT, Corp
   - `occ` 住房率
   - `dayofweek` 星期幾 (星期一～星期日)
  
   **模型**:
   - Multiple Linear Regression
   - Random Forest Regression
  
   **目的**: 以日期及住房率特徵，預測未來日期之營收，協助訂價決策  
---  
2. 分群分析：預測住房率高低  
   判斷某日是否會成為**高住房日（≥60%）**或**低住房日（<60%）**  

   **Features**:
   - `day` 日期 (1日至31日)
   - `dayofweek` 星期幾 (星期一～星期日)
   - `daytype` 日別: 平日, 旺日, 假日
   - `special_event` 特殊事件: Negative / None / Positive

   **模型**:
   - Decision Tree Classifier

   **目的**: 識別影響入住率的關鍵因素
---  
3. 分群分析：日別劃分以做為訂價層級參考  
   使用分群分析來判斷現有的日別類型（平日、旺日、假日）是否足夠，或是否應該建立更細緻的日別類型，以更有效地支援定價策略   

   **Features**:
   - `rn_fit, rn_git, rn_corp` 各市場房晚數: FIT, GIT, Corp  
   - `rev_fit, rev_git, rev_corp` 各市場營收: FIT, GIT, Corp  

   **模型**:
   - K-Means Clustering
  
   **目的**: 根據飯店績效趨勢進行劃分，尋找潛在的新日別類型（例如：旺季平日、星期六、有活動的週末），以建立比原始三分類系統（平日、旺日、假日）更有效的定價級距。  

---  
## 📁 專案結構  
ML Project - Hotel_Performance_project/  
├── Hotel Performance Prediction.ipynb # Jupyter Notebook完整專案內容  
├── Mock_Hotel_daily.csv # 模擬資料 (365天)  
├── README.md # 本說明文件  
└── requirements.txt # Python 套件需求檔  

---  
## 🔧 安裝方式  
### 使用 pip  
```bash  
pip install -r requirements.txt  
```
### Option 2: 使用 conda  
您可以手動建立 Conda 環境並安裝 requirements.txt 中列出的套件:  
```
conda create -n hotel-ml python=3.10  
conda activate hotel-ml  
pip install -r requirements.txt
```
⚠️ 注意：建議使用 Python 3.10 以確保相容性，但您也可以根據需要更換版本。  
此外，hotel-ml僅為示範用的環境名稱，您可以自由替換為您偏好的名稱。  
  
---
## 📷 結果摘要  
- 從Crrelation Heatmap得出，總營收與 FIT 間夜、住房率、週六與假日有**正相關**；GIT 與 Corp 有**負相關**，可能因其平均房價較低。  
  **這有助於未來分配各市場房間策略。**   
- 第1部分: **迴歸分析 - 預測飯店績效**  
  - 透過**線性回歸**與**隨機森林回歸**預測營收與平均房價，可用於做為未來訂價策略參考。  
- 第2部分: **分群分析 - 預測住房率高低**  
  - 初始**Decision Tree**出現過度擬合，經pruning和tuning調整後改善。結果顯示**月初與月底的星期二**需特別關注。  
  - 模型未呈現高度可解釋性，顯示**日期、星期幾、日別與事件**等變數可能無法有效預測住房率高低。基於**領域經驗與Correlation heatmap**，建議加入**月份**作為特徵，以反映飯店業及旅遊業獨特的**季節性**。  
  - 目前此預測住房率高低的分群分析包含**所有市場類別**，但實際上飯店常利用**團客與商務客**來填補淡日空房，並不一定有固定的每週趨勢，且團客數量更易因季節而不穩定，這些因素可能為模型帶來雜訊。未來可考慮**單純以散客**為目標進行分類，以排除團客與商務客的不穩定性，提升模型效率，並在淡日需要**團客和商務客**協助時，提供更可靠的參考。  
- 第3部分: **分群分析 - 日別劃分以做為訂價層級參考**  
  - **K-Means**顯示，相較於原始的3個日別分類，**6–8個日別**是比較適合的，可用於未來訂價層級的參考。  
  - 基於**領域經驗**，可考慮將**週六**自旺日獨立出來，或是根據**旺季(暑假及寒假)**進行更細緻分類，調整後的分類或許也可以改善專案前兩個部分的準確性。    
- 視覺化包括 **correlation heatmaps**, **decision tree diagrams**, and **cluster visualizations** (請見 notebook).
  
---
## 🚀 未來改進方向  
- **擴充資料** 加入更多年份的歷史資料，以更全面反映季節性與異常波動。  
- **使用真實資料進行訓練與驗證** 以提升準確度與泛化能力.  
- **重新定義日別類型** 以更精準反映出飯店價格與績效趨勢，並提升模型準確度。  
- **納入外部因素** 例如氣候或大型活動可能會對住房率和營收有重要的影響。  
- **參考歷史競爭對手資料** 以更進一步探索價格及市場趨勢。    
  *註: 需使用真實世界資料，不適用於本合成資料*  
- **重新定義分群目標** 以**單純散客**為主進行分群，排除團客及商務客不穩定所帶來的雜訊，以更準確判斷低需求日。    
- **建立互動式儀表板** 以供經營管理團隊參考趨勢及預測。  
- **應用於未來整年度資料** 以模型預測結果來做為營運與定價策略的參考。  
  
---
## 📄 授權聲明    
本專案為個人實作用途，所使用資料為合成模擬資料，無任何實際飯店營運數據。未經允許請勿任意使用、發佈或再製此專案內容。  

