**中文版本請往下滑動查看**｜[Scroll down for Mandarin version]  
  
# Project - Hotel Performance   
  
## Project Overview  
This project includes two sub-projects applying statistical analysis and machine learning techniques to support better operational and pricing decisions by revealing patterns in demand, occupancy, and revenue across different day types and market segments.  
- Statistical Analysis:  
  - **Hypothesis** - Seasonal ADR differences  
  - **Hypothesis** - Occupancy difference between spring and summer  
  - **Correlation** - Relationship between prices and occupancy in seasons  
- ML Regression and Classification:  
  - **Regression** – Predict hotel performance  
  - **Classification** – Predicting occupancy levels  
  - **Classification** – Grouping day types for pricing tiers  
  
The analysis is based on a synthetic dataset simulating realistic hotel performance over a full year (365 days).  
  
---  
## Dataset  
- The dataset is **synthetic**, generated to simulate realistic hotel performance across 365 days.  
- Fields include:  
  - `date`: Calender date in 2023 (used to derive day and month values)  
  - `dayofweek`: Day name (e.g., Monday–Sunday)  
  - `daytype`: Weekday, Peak, or Holiday  
    - *Peak* includes Fridays to Sundays, the day before a holiday, the last day of a holiday, and one-day holiday.  
    - *Holiday* refers to holidays that span **more than one day**, typically combining with a weekend. One-day holidays are not labeled as "Holiday" in this field.  
  - `special_event`: Indicates whether a special event occurs (negative, none, or positive)  
  - `rn_fit, rn_git, rn_corp`: Room nights sold in **FIT**(Free Independent Traveler), **GIT**(Group Inclusive Tour), **Corporate** market segments   
  - `adr_fit, adr_git, adr_corp`: Average Daily Rate (ADR) in each market segments  
  - `rev_fit, rev_git, rev_corp`: Revenue generated in each market segments  
  - `occ`: Occupancy rate (percentage)  
  - `rn_ttl, adr_ttl, rev_ttl`: Total values across all market segments  
  
*Note:  
ADR = Revenue / Room Nights Sold  
RevPAR = ADR × Occupancy*  
  
--- 
## Project Sections  
[Project Flow](project_flow/Hotel Project Flow Diagram.png)
### Statistical Analysis  
1. **Hypothesis 1 – Seasonal ADR Differences**  
   *Null Hypothesis (H0): There is no significant difference in prices (ADR) between seasons.  
   Alternative Hypothesis (Ha): At least one season's prices (ADR) differs.*  
  
   **Features**:  
   - Seasons (Spring, Summer, Fall, Winter)  
   - ADR  
  
   **Models**:  
   - One-way ANOVA  
   - Tukey's Range Test  
  
   **Goal**: To prove seasonality in the hospitality industry and support pricing strategy.  
  
2. **Hypothesis 2 – Occupancy Difference Between Spring and Summer**  
   *Null Hypothesis (H0): There is no significant difference in occupancy between Spring and Summer.  
   Alternative Hypothesis (Ha): There is a significant difference in occupancy between Spring and Summer.*  
  
   **Features**:  
   - Seasons (Spring, Summer)  
   - Occupancy rate  
  
   **Models**:  
   - two-sample t-test  
  
   **Goal**: Since Hypothesis 1 found no significant difference in ADR between spring and summer, despite domain expectations that summer should be higher, a follow-up hypothesis was tested to compare occupancy instead, to explore if spring's prices may be too high.  
  
3. **Correlation – Relationship Between Prices and Occupancy in Seasons**  
   A scatter plot was created for ADR vs. occupancy within the spring season. Pearson correlation coefficients were calculated for each season.  
  
   **Features**:  
   - Seasons (Spring, Summer, Fall, Winter)  
   - ADR  
   - Occupancy rate  
  
   **Models**:  
   - Pearson correlation coefficients  
  
   **Goal**: To explore whether high spring ADR leads to lower occupancy, and to reveal the strength of the relationship between ADR and occupancy in each season.  
  
### ML Regression & Classification  
1. **Regression – Predicting Hotel Performance**  
   Use regression models, both linear and non-linear, to predict **total daily revenue** and derive ADR and RevPAR.  
  
   **Features**:  
   - Room nights sold by market (FIT, GIT, Corp)  
   - Occupancy rate  
   - Day of week (Monday–Sunday)  
   - Day type (Weekday, Peak, Holiday)  
  
   **Models**:  
   - Multiple Linear Regression  
   - Random Forest Regression  
  
   **Goal**: Estimate expected revenue based on operational and calendar variables to support future pricing strategies.  
  
2. **Classification – Predicting Occupancy Levels**  
   Classify whether a day will have **high occupancy (≥60%)** or **low occupancy (<60%)**.    
  
   **Features**:  
   - Day of the month (1st–31st)  
   - Day of week (Monday–Sunday)  
   - Day type (Weekday, Peak, Holiday)  
   - Special event impact (Negative / None / Positive)  
  
   **Model**:  
   - Decision Tree Classifier  
  
   **Goal**: Identify days likely to have low occupancy, enabling targeted promotions or pricing strategies.  
  
3. Clustering – Grouping Day Types for Pricing Tiers  
   Use clustering to explore whether the existing day types (Weekday, Peak, Holiday) are sufficient or if more granular categories are needed.  
  
   **Features**:  
   - Room nights sold by market (FIT, GIT, Corp)  
   - Revenue by market (FIT, GIT, Corp)  
  
   **Model**:  
   - K-Means Clustering  
  
   **Goal**: Discover new pricing tiers (e.g., event weekends, peak-season weekdays) based on performance, supporting more nuanced pricing strategies.  
  
---  
## Project Structure  
Project - Hotel Performance/  
├── data/  
│   └── Mock_Hotel_daily.csv  
├── notebooks/  
│   └── 01 - Hotel Performance - Statistical Analysis.ipynb  
│   └── 02 - Hotel Performance - ML Regression and Classification.ipynb  
├── project_flow/  
│   └── Hotel Project Flow Diagram.png  
├── .gitignore  
├── README.md  
└── requirements.txt  
  
---  
## Installation  
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
*Note: Python 3.10 is recommended to ensure compatibility, but you can change the version if needed.  
Also, you can replace hotel-ml with any environment name you prefer.*  
  
---
## Results  
### Statistical Analysis  
- **Hypothesis 1 - Seasonal ADR Differences**  
  - Null Hypothesis (H0) rejected; significant ADR differences exist between seasons.  
  - Tukey’s test shows significant differences between Fall–Summer, Fall–Winter, and Spring–Winter.  
  - ADR difference between Spring and Summer is not statistically significant, contradicting domain knowledge that summer should be the peak season. This raised the question of whether spring’s ADR was set too high.  
- **Hypothesis 2 - Occupancy Difference Between Spring and Summer**  
  - Null Hypothesis (H0) rejected; significant occupancy difference found.  
  - Suggests high ADR in spring may be suppressing demand.  
  - However, ADR and occupancy in spring still show a positive correlation.  
- **Correlation - Relationship Between ADR and Occupancy**  
  - Winter has the weakest correlation (r = 0.26), while other seasons range from 0.34–0.41.  
  - Boxplots show a **wider distribution in both ADR and occupancy** during winter, indicating higher variability.  
  - Domain experience: This is likely due to a mix of **strong demand in December** and **low demand in January and February**, except during Chinese New Year.  
  - This seasonal inconsistency weakens linear relationships and may indicate price inelasticity during winter.  
  
### Hotel Performance - ML Regression and Classification  
- A correlation heatmap shows that total revenue has a **positive relationship** with FIT room nights, occupancy rate, Saturdays, and Holidays. Although GIT and Corporate room nights help fill low-demand days, they are **negatively correlated** with total revenue, likely due to lower ADR in those segments.  
  **This insight supports strategic room allocation across market segments.**  
- **Regression – Predicting Daily Revenue**  
  - Both Linear Regression and Random Forest Regression successfully predict total revenue, ADR, and RevPAR.
  - Results help in forecasting and optimizing pricing.  
- **Classification – Predicting Occupancy Levels**  
  - Initial decision tree overfit the data. After pruning and tuning, model performance improved.  
  - Key insight: monitor **Tuesdays at the end of each month** and **Mondays at the beginning**, which tend to be lower occupancy.  
  - Currently, the occupancy classification includes all market segments.
      - Domain experience: In real-world operations, **GIT and Corporate bookings** are often used to fill low-demand days and do not follow a consistent weekly pattern like FIT bookings.
      - Including them may introduce noise into the model and reduce predictive accuracy.
      - A better approach may be to classify based on **FIT-only occupancy or revenue**, which would provide a cleaner signal for organic demand and help determine when **GIT/Corporate support** is truly needed.  
- **Classification - Grouping Day Types for Pricing Tiers**  
  - K-Means suggests **4–8 meaningful clusters** beyond the current weekday/peak/holiday categorization, supporting the idea of more granular pricing tiers.  
  - Based on domain experience, we may consider separating **Saturdays** from other peak days, or defining **special weekday/peak patterns** during **seasonal breaks** (e.g., summer or winter holidays).  
  - This refined day type classification may enhance may enhance pricing strategies and improve ML models accuracy.  
- Visualizations include **correlation heatmaps**, **decision tree diagrams**, and **cluster visualizations** (see notebook).  
  
---
## Future Improvements  
- **Expand the dataset** by including data from multiple past years to capture seasonal trends and unusual patterns.  
- **Train and validate models with real-world data** to improve performance and generalizability.  
- **Refine the day type classification** to better reflect pricing behavior and occupancy patterns, potentially improving model accuracy.  
- **Incorporate external factors** such as weather conditions or local events, which may have a strong influence on occupancy and revenue.  
- **Leverage historical competitor performance data** (e.g., from benchmarking reports) to better position the hotel's pricing and predict market behavior.  
  *Note: This would require real-world data sources and is not applicable to the current synthetic dataset.*
- **Refine classification targets** by focusing on **FIT-only occupancy or revenue**, reducing noise from inconsistent GIT/Corp availability and better identifying truly low-demand days.  
- **Develop an interactive dashboard** to visualize trends, model outputs, and support decision-making by hotel management.  
- **Apply the models to a full future year** for forward-looking predictions to support pricing strategy and resource planning.
  
---
## License  
This project uses synthetic data generated solely for educational and demonstration purposes. It does not reflect real hotel operations or confidential business information.  
All analysis and code are intended for non-commercial academic use.  

---
    
   
# 專案 - 飯店營運績效  
## 專案概述  
本專案結合統計分析與機器學習兩部分，透過分析不同日別與市場區隔下的需求、住房率與營收趨勢，協助做出更有效的營運與定價決策。  
- 統計分析部分:
  - **假設檢定** - 平均房價季節差異
  - **假設檢定** - 春季和夏季間的住房率
  - **相關性分析** - 各季節平均房價與住房率間的關係
- 機器學習回歸與分類部分:  
  - **迴歸分析** - 預測飯店績效  
  - **分類分析** – 預測住房率高低  
  - **分群分析** – 日別劃分以做為訂價層級參考  

本分析使用模擬飯店一整年的營運情形（365天）的合成資料。  
  
---
## 資料集  
- 資料為合成資料，模擬 2023 年度 365 天的飯店營運表現。  
- 欄位包含：  
  - `date`: 2023年日期(用以擷取月份與日期)  
  - `dayofweek`: 星期幾(例如：星期一至星期日)  
  - `daytype`: 日別，平日、旺日、假日  
    - *旺日* 包含星期五至星期日、假日前一天、假期最後一天及單日假日  
    - *假日* 指連續假期(不包含只有一天的國定假日)  
  - `special_event`: 是否有特殊事件(負面、無、正面)  
  - `rn_fit, rn_git, rn_corp`: 各市場**FIT**(散客)、**GIT**(團客)、**Corp**(商務)房晚數  
  - `adr_fit, adr_git, adr_corp`: 各市場平均房價(ADR)  
  - `rev_fit, rev_git, rev_corp`: 各市場營收  
  - `occ`: 住房率(百分比)  
  - `rn_ttl, adr_ttl, rev_ttl`: 各市場總和  

*註：
平均房價(ADR) = 營收 / 房晚數
RevPAR = 平均房價 × 住房率*  

--- 
## 專案內容

### 統計分析  
1. **假設檢定1 - 平均房價季節差異**  
   *虛無假設 H0：各季節沒有顯著平均房價差異  
   對立假設 Ha：至少一個季節的平均房差有顯著差異*  
  
   **Features**:  
   - 季節(春、夏、秋、冬)  
   - 平均房價  
  
   **模型**:  
   - 單因子變異數分析(ANOVA)  
   - 杜凱氏事後多重檢驗(Tukey's Range Test)
  
   **目的**: 驗證飯店業常見的季節性價差是否顯著，提供定價策略依據。       
  
2. **假設檢定2 - 春季和夏季間的住房率**  
   *虛無假設 H0：春季與夏季間沒有顯著住房率差異  
   對立假設 Ha：春季與夏季間存在著顯著住房率差異*  
  
   **Features**:  
   - 季節(春、夏)
   - 住房率  
  
   **模型**:  
   - 雙樣本T檢定(two-sample t-test)  
  
   **目的**: 前一檢定發現春、夏平均房價無顯著差異，根據業界經驗夏季應為價格較高的旺季，因此本檢定進一步比較住房率，檢驗春季是否定價過高造成低住房率。  
  
3. **相關性分析 - 不同季節中價格與住房率的關係**  
   透過散佈圖觀察春季平均房價與住房率的關係，並計算各季節間的皮爾森相關係數。  
  
   **Features**:  
   - 季節(春、夏、秋、冬)
   - 平均房價  
   - 住房率  
  
   **模型**:  
   - 皮爾森相關係數(Pearson correlation coefficients)  
  
   **目的**: 分析春季是否因價格過高導致住房率下降，並比較不同季節價格與住房率間的關聯強度。  

### 機器學習回歸與分類  
1. **迴歸分析：預測飯店績效**  
   使用迴歸模型(包含線性與非線性)來預測每日總營收，並推算出平均房價與RevPAR。  
  
   **Features**:  
   - 各市場房晚數(散客、團客、商務)  
   - 住房率  
   - 星期幾(星期一至星期日)  
   - 日別(平日、旺日、假日)  
  
   **模型**:  
   - 多元線性迴歸(Multiple Linear Regression)  
   - 隨機森林迴歸(Random Forest Regression)
  
   **目的**: 依據營運與日期特徵預測每日營收，支援定價與營運規劃。  
   
2. **分類分析 - 預測住房率高低**  
   預測某日是否為**高住房日(≥60%)**或**低住房日(<60%)**  
  
   **Features**:  
   - 日期(1日至31日)  
   - 星期幾(星期一至星期日)  
   - 日別(平日、旺日、假日)  
   - 特殊事件(負面、無、正面)  
  
   **模型**:  
   - 決策樹模型(Decision Tree Classifier)  
  
   **目的**: 判別可能出現低住房率的日子，作為促銷或價格調整的依據。  
  
3. **分群分析 - 日別劃分以做為訂價層級參考**  
   探討現有的日別類型(平日、旺日、假日)是否足夠，是否應該建立更細緻的日別類型，以更有效地支援定價策略   
  
   **Features**:  
   - 各市場房晚數(散客、團客、商務)  
   - 各市場營收(散客、團客、商務)  
  
   **模型**:  
   - K-Means Clustering  
  
   **目的**: 根據飯店績效趨勢進行劃分，尋找潛在的新日別類型（例如：旺季平日、星期六、有活動的週末），以建立比原始三分類系統（平日、旺日、假日）更有效的定價級距。  
  
---  
## 專案結構  
Project - Hotel Performance/  
├── data/  
│   └── Mock_Hotel_daily.csv  
├── notebooks/  
│   └── 01 - Hotel Performance - Statistical Analysis.ipynb  
│   └── 02 - Hotel Performance - ML Regression and Classification.ipynb  
├── .gitignore  
├── README.md  
└── requirements.txt  
  
---  
## 安裝方式  
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
*注意：建議使用 Python 3.10 以確保相容性，但您也可以根據需要更換版本。  
此外，hotel-ml僅為示範用的環境名稱，您可以自由替換為您偏好的名稱。*  
  
---
## 結果摘要  

### 統計分析  
- **假設1 - 平均房價季節差異**  
  - 虛無假設檢定拒絕，季節間存在顯著平均房價差異。  
  - 秋夏季、秋冬季、春冬季等組合有顯著平均房價差異。  
  - 然而春夏之間平均房價未達到統計上的顯著差異，與夏為旺季的領域經驗不符，可能代表春季定價過高。  
- **假設2 - 春季和夏季間的住房率**  
  - 虛無假設檢定拒絕，春季和夏季間存在顯著住房率差異。  
  - 顯示春季價格高於需求。  
  - 然而春季平均房價與住房率之間仍呈現正向相關。  
- **相關性分析 - 各季節平均房價與住房率間的關係**  
  - 冬季的平均房價與住房率顯示出最低的相關度(r = 0.26), 其他季節則介於0.34至0.41之間。  
  - 盒鬚圖顯示，冬季的房價與住房率皆呈現**較大的分布範圍**。  
  - 根據領域經驗，冬季同時包含了**較旺的12月**，而**1-2月(除農曆春節外)則為最淡的月份**，形成需求有**高峰低谷**的大幅波動情形。
  - 這些季節因素的不穩定性，可能削弱價格與住房率間的線性關係，並降低價格彈性。  
  
### 機器學習回歸與分類  
- 從相關係數熱力圖得出，總營收與散客房晚數、住房率、週六與假日皆有**正相關**。實務上，團客和商務客常用來填補低住房率日期，因其平均房價較低，因此與總熟收有**負相關**。  
  **這有助於未來分配各市場房間策略。**  
- **迴歸分析 - 預測飯店績效**  
  - 透過**線性回歸**與**隨機森林回歸**有效預測每日營收、平均房價與RevPAR。  
  - 可用於做為未來訂價策略參考。  
- **分類分析 - 預測住房率高低**  
  - 初始**決策樹**出現過度擬合，經調整參數與剪枝後改善。  
  - 結果顯示**月底的星期二**與**月初的星期一**可能會有低住房率，需特別注意。  
  - 目前此預測住房率高低的分群分析包含**所有市場類別**  
    - 然而根據領域經驗，**團客與商務客**常被用來填補淡日，因此其數量波動較大，未必呈現明顯的每週趨勢。  
    - 這些因素可能為模型帶來雜訊，進而降低預測準確度。  
    - 未來可考慮**單純以散客**為目標進行分類，以排除團客與商務客的不穩定性，提升模型效率，並在淡日需要**團客和商務客**協助時，提供更可靠的參考。  
- **分群分析 - 日別劃分以做為訂價層級參考**  
  - K-Means顯示，相較於原始的3個日別分類，**4–8個日別**是比較適合的，可用於未來訂價層級的參考。  
  - 基於領域經驗，可考慮將**週六**自旺日獨立出來，或是根據**旺季(暑假及寒假)**進行更細緻分類。  
  - 調整日別分類可以強化價格策略，也可能改善前兩個迴歸分析與分類分析的準確性。  
- 視覺化包括 **correlation heatmaps**, **decision tree diagrams**, and **cluster visualizations** (請見 notebook)。  
  
---
## 未來改進方向  
- **擴充資料** 加入更多年份的歷史資料，以更全面反映季節性與異常波動。  
- **使用真實資料進行訓練與驗證** 以提升準確度與泛化能力。  
- **重新定義日別類型** 以更精準反映出飯店價格與績效趨勢，並提升模型準確度。  
- **納入外部因素** 例如氣候或大型活動可能會對住房率和營收有重要的影響。  
- **參考歷史競爭對手資料** 以更進一步探索價格及市場趨勢。  
  *註: 需使用真實世界資料，不適用於本合成資料*  
- **重新定義分群目標** 以**單純散客**為主進行分群，排除團客及商務客不穩定所帶來的雜訊，以更準確判斷低需求日。  
- **建立互動式儀表板** 以供經營管理團隊參考趨勢及預測。  
- **應用於未來整年度資料** 以模型預測結果來做為營運與定價策略的參考。  
  
---
## 授權聲明    
本專案為個人實作用途，所使用資料為合成模擬資料，無任何實際飯店營運數據。未經允許請勿任意使用、發佈或再製此專案內容。  

