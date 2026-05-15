<h1 align="center">
   Data Analytics Group 4 ✴︎
</h1>

<h2 align="center" style="margin-bottom: 5px;">
  <b>Data Collection ⸙</b>
</h2>
 
- **Dataset Name:** Comprehensive Diabetes Clinical Dataset
- **Contains:** 100,000 records
- **Description:** This dataset comprises health and demographic data of 100,000 individuals, including gender, age, race, lifestyle factors, and key clinical markers aimed at supporting diabetes research and predictive modeling.
- **Link:** https://www.kaggle.com/datasets/priyamchoksi/100000-diabetes-clinical-dataset

<br><br>
<h2 align="center" style="margin-bottom: 5px;">
  <b>Data Preprocessing ⸙</b>
</h2>

<p align="center" style="margin-top: 0;">
  Using the CLEAN framework (Conceptualize, Locate, Evaluate, Augment, Note)
</p>

---

### ╰┈➤ Conceptualize the Data
 
**What does each row represent?**
 
Each row represents a unique clinical encounter or medical profile of an individual within a specific year. It captures a snapshot of their demographic background, lifestyle choices (smoking), and vital clinical markers used to assess the presence of diabetes.
 
---
 
### ╰┈➤ Locate Solvable Problems
 
#### 1. Duplicates found
 
- Removed 14 duplicates
#### 2. Inconsistent casing format
 
- Used PROPER formula to 35806 rows for proper casing
#### 3. Less than or equal to 5 years old having "No Info" values (5505 rows)
 
- Imputation; I interpreted the smoking history column as only targeted on first hand smoking, so I based my understanding on this premise. Based on that premise, I considered that 5 years old and under do not have the capacity to be smoking, so I just changed the values to "Never"
#### 4. Less than or equal to 5 years old having "Not Currently", "Ever", and "Current" smoking history values (103 rows)
 
- Imputation; Just like the previous issue, I considered that children aged 5 years old and under are unlikely to have a smoking history or to have smoked previously. Therefore, any smoking history values ("Not Current", "Ever", and "Current") for this age group were changed as "Never"
---
 
### ╰┈➤ Evaluate Unsolvable Issues
 
#### 1. BMI of > 80
 
- I kept the outliers since they might be real events. 
#### 2. Ambiguity between "Former" and "Not Current" values (15713 rows)
 
- Smoking history had both "Former" and "Not Current" categories, which seem similar but may not mean exactly the same thing. To avoid mixing unclear data, they were kept as separate categories. I assumed "Former" means a clear past smoker, while "Not Current" only means the person is not smoking at the moment, but it does not clearly confirm whether they ever smoked before.
---
 
### ╰┈➤ Augment the Data
 
#### 1. Created `age_group` column for grouping ages into categories (like Child, Adult, and Senior) to see how diabetes risks change at different stages of life

| age          | age_group   |
|--------------|-------------|
| Below 13     | Child       |
| 13 – 19      | Teen        |
| 20 – 39      | Young Adult |
| 40 – 59      | Middle-Aged |
| 60 – 79      | Senior      |
| 80 and above | Elderly     |

#### 2. Created a new column called `race` to combine the 5 separate race columns into one `race` label to make the data easier to read. After that, I deleted the columns "race:AfricanAmerican", "race:Asian", "race:Caucasian", "race:Hispanic", "race:Other" since they are not needed because of the race column.

<img width="597" height="38" alt="image" src="https://github.com/user-attachments/assets/e3c956e1-0adb-4867-bc7b-017f701e1073" />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img width="128" height="118" alt="image" src="https://github.com/user-attachments/assets/26928f53-1119-4e06-96cd-32844b9107ff" />

#### 3. Added `patient_id` to uniquely identify each patient and `race_id` to keep race categories organized and consistent for analysis
 
| race_id | Race             |
|---------|------------------|
| r-1     | African American |
| r-2     | Asian            |
| r-3     | Caucasian        |
| r-4     | Hispanic         |
| r-5     | Other            |
 
- patient_id: p-1, p-2, p-3, p-4, … p-99986
---

### ╰┈➤ Note and Document

<img width="1290" height="704" alt="image" src="https://github.com/user-attachments/assets/bcd9e5f4-30e3-49bd-a618-a613c2c02d0a" />

<br><br><br>

<h2 align="center" style="margin-bottom: 5px;">
  <b>Exploratory Data Analysis ⸙</b>
</h2>
<p align="center" style="margin-top: 0;">
  Using PYRAMID FRAMEWORK: Key Metrics and Measures
</p>
<hr>

<img width="1129" height="622" alt="image" src="https://github.com/user-attachments/assets/8fd76ba4-405c-4100-9efd-de35f8b6013a" />

<img width="1092" height="695" alt="image" src="https://github.com/user-attachments/assets/2b23a637-b1b7-4750-8ef4-7b6f6bfed520" />

### ╰┈➤ Conceptualize the Dashboard
 
**What is the purpose of the dashboard?**
 
The dashboard was created to perform Exploratory Data Analysis (EDA) using a diabetes dataset in Power BI. Its main purpose is to analyze diabetes-related health information and present insights through interactive visualizations and KPI measures.
 
The dashboard helps users understand patterns and relationships between BMI, blood glucose level, smoking history, age group, and diabetes status.

 
**What are the key metrics?**
 
- Total Patients
- Total Diabetes Cases
- Diabetes Rate
- Average Glucose
- Average BMI
- Average HbA1c
- Average Age
---
 
### ╰┈➤ Visualizations Used
 
#### 1. KPI Cards
- Used to display important summary metrics such as Total Patients, Diabetes Cases, Diabetes Rate, and Average Glucose.
#### 2. Bar Chart
- Used to visualize diabetes cases by age group to identify which age category has higher diabetes occurrences.
#### 3. Line Graph
- Used to analyze diabetes trends by year and observe changes over time.
#### 4. Pie Chart
- Used to display the distribution of smoking history categories among patients.
#### 5. Scatter Plot
- Used to analyze the relationship between BMI and Blood Glucose Level. Each point in the scatter plot represents one patient.
#### 6. Patient Details Table
- Used to display detailed patient information such as patient ID, age group, gender, BMI, blood glucose level, and diabetes status.
#### 7. Slicers and Filters
- Added to allow interactive filtering by year, gender, age group, and smoking history.
---
 
### ╰┈➤ DAX Measures Created
 
#### 1. Total Patients
```
Total Patients = COUNT(diabetes_cleaned[patient_id])
```
 
#### 2. Total Diabetes Cases
```
Total Diabetes Cases = SUM(diabetes_cleaned[diabetes])
```
 
#### 3. Average Glucose
```
Average Glucose = AVERAGE(diabetes_cleaned[blood_glucose_level])
```
 
#### 4. Diabetes Rate
```
Diabetes Rate = DIVIDE(SUM(diabetes_cleaned[diabetes]), COUNT(diabetes_cleaned[patient_id]))
```
 
---
 
### ╰┈➤ Dashboard Layout Using Pyramid Framework
 
#### Top Level — KPI
- Total Patients
- Total Diabetes Cases
- Diabetes Rate
- Average Glucose
#### Middle Level — Analysis
- Diabetes Cases by Age Group
- Diabetes Cases by Year
- Diabetes Cases by Smoking History
#### Detailed Level — Analysis
- BMI vs Blood Glucose Scatter Plot
- Patient Details Table
- Interactive Filters and Slicers
---
 
### ╰┈➤ Model View Organization
 
A separate KPI Measures table was created to organize all DAX measures used in the dashboard. The `diabetes_cleaned` table contains the raw dataset, while the `KPI Measures` table contains calculated measures such as Total Patients, Diabetes Rate, and Average Glucose.
 
---
 
### ╰┈➤ Insights Gathered
 
- Senior and Middle-Aged groups have higher diabetes cases.
- Patients with higher BMI tend to have higher blood glucose levels.
- Smoking history categories such as "Never" and "No Info" contain the largest patient counts.
- The dashboard allows users to explore the dataset interactively through slicers and filters.
---
 
### ╰┈➤ Conclusion
 
The EDA Dashboard successfully presented important diabetes-related insights using Power BI visualizations and KPI measures. The project demonstrated how Exploratory Data Analysis can help analyze healthcare data and identify trends and relationships among different variables.

<br><br><br>

<h2 align="center" style="margin-bottom: 5px;"> <b>Data Modeling / Analytics ⸙</b> </h2>
<p align="center" style="margin-top: 0;"> Following the DASH Framework for Dashboard Development </p>

---

<img width="1280" height="719" alt="image" src="https://github.com/user-attachments/assets/ed88247c-2abd-4d43-bdae-9e4cc5b60cce" />

<img width="1022" height="706" alt="image" src="https://github.com/user-attachments/assets/70dc387a-13ce-4e18-abe4-f3683bde210b" />

### ╰┈➤ 1. Project Overview

**What does this dashboard analyze?**

The dashboard analyzes diabetes prevalence across the United States using a single cleaned dataset containing **100,000 patient records from 2015 to 2022**, covering all US states.

---

### ╰┈➤ 2. Data Model

The data model in this Power BI file is built on a single flat table named `diabetes_cleaned`, loaded and transformed directly from the source Excel dataset. This approach uses a **flat/denormalized model** rather than a fully normalized Star Schema, making it straightforward to implement while still supporting all required analytical queries.

#### 2.1 DAX Measures

The following calculated measures were created inside the `diabetes_cleaned` table and are used to power the KPI cards and chart values:

<img width="623" height="232" alt="image" src="https://github.com/user-attachments/assets/50ee7678-98d6-46bd-865f-9db852677073" />

#### 2.2 Data Schema Approach

The model uses a **single-table (flat) schema**, meaning all columns — both dimensions (`age_group`, `gender`, `race`, `location`, `smoking_history`) and facts (`bmi`, `hbA1c_level`, `blood_glucose_level`, `diabetes`) — reside in one table. This approach:

- Eliminates the need for relationship management between multiple tables
- Is suitable for datasets of this size and complexity (100,000 rows, 13 columns)
- Allows Power BI slicers and filters to work directly against all columns
- Supports all descriptive analytics and forecasting requirements without joins

> For a more scalable production model, this could be extended to a **Star Schema** by splitting out dimension tables (`dim_Patient`, `dim_Location`, `dim_Ra

<br><br><br>

<h2 align="center" style="margin-bottom: 5px;"> <b>Dashboard Design ⸙</b> </h2>

The dashboard consists of a **single report page** containing **12 visual elements**. All visuals reference the `diabetes_cleaned` table and respond to the four slicers for interactive filtering.

#### 4.1 KPIs

| Measure | DAX Formula |
|---|---|
| Total Records | `COUNTROWS(fact_DiabetesRecords)` |
| Diabetic Cases | `CALCULATE(COUNTROWS(fact_DiabetesRecords), fact_DiabetesRecords[diabetes] = 1)` |
| Diabetes Prevalence % | `DIVIDE([Diabetic Cases], [Total Records]) * 100` |
| Avg HbA1c | `AVERAGE(fact_DiabetesRecords[hbA1c_level])` |
| Avg Blood Glucose | `AVERAGE(fact_DiabetesRecords[blood_glucose_level])` |

#### 4.2 Chart Visuals

The page contains four chart visuals that provide descriptive analytics across different dimensions:

<img width="623" height="256" alt="image" src="https://github.com/user-attachments/assets/66071ab8-634f-4a3e-8ec3-c9dce226a15d" />

#### 4.3 Slicers & Interactivity

Four slicer visuals are positioned along the right side of the report page. They enable **interactive cross-filtering** — selecting any value in a slicer automatically filters all four chart visuals and the KPI cards simultaneously.

<img width="625" height="232" alt="image" src="https://github.com/user-attachments/assets/0b74c808-1f33-469a-95c0-66ea442ba38d" />

>  Cross-filtering is enabled by default (`defaultDrillFilterOtherVisuals = true` in the report config), meaning clicking any data point on a chart also acts as a filter on all other visuals on the page.

---

### ╰┈➤ 5. Key Findings

Based on the visuals and data in the dashboard, the following insights are drawn:

- **Overall diabetes prevalence is 8.5%** — 8,500 out of 100,000 patients are diabetic
- **Older age groups** have significantly higher diabetic case counts, with the steepest rise occurring between the **30–44** and **45–59** brackets
- **Current and former smokers** show consistently higher diabetic case counts compared to patients who have never smoked
- The **year-on-year line chart** shows an upward trend in cases from 2015 to 2022, with the forecast extending this trend through 2024
- **Caucasian patients** represent the largest share of diabetic cases by race, followed by African American and Hispanic patients
- **Average HbA1c of 5.53%** is within the normal range overall, but diabetic patients individually show significantly higher readings
- **Average blood glucose of 138 mg/dL** falls within the pre-diabetic range, suggesting many patients are at elevated risk

<br><br><br>

 <h2 align="center" style="margin-bottom: 5px;">
  <b>Insights and Recommendations ⸙</b>
</h2>
 
### ╰┈➤ Age Group and Diabetes Risk
 
**Insight**
The dashboard showed that senior patients recorded the highest number of diabetes cases at around 3.9K, followed by middle-aged patients with approximately 2.9K cases. Younger age groups such as teens and children had significantly fewer recorded cases. This indicates that diabetes risk becomes more common as age increases.
 
**Real-World Context**
In real healthcare situations, older adults are more vulnerable to diabetes because of reduced physical activity, slower metabolism, and long-term lifestyle habits. As populations continue to age, healthcare facilities may experience an increasing number of diabetes-related cases and complications.
 
**Recommendation**
Healthcare institutions should prioritize regular diabetes screening and health awareness programs for middle-aged and senior individuals. Community clinics and hospitals may also implement preventive wellness programs focused on healthy aging and disease prevention.
 
---
 
### ╰┈➤ BMI and Blood Glucose Relationship
 
**Insight**
The scatter plot showed that many patients with higher blood glucose levels also had moderate to high BMI values. This suggests a possible relationship between body weight and diabetes cases within the dataset.
 
**Real-World Context**
In real-life situations, obesity is commonly associated with higher diabetes risk because excess body fat may affect insulin function and blood sugar regulation. Sedentary lifestyles and unhealthy eating habits may contribute to increasing BMI levels among patients.
 
**Recommendation**
Healthcare providers should promote proper nutrition, regular exercise, and weight management programs. Patients with high BMI levels should also be encouraged to undergo regular blood glucose monitoring for early detection of diabetes.
 
---
 
### ╰┈➤ Smoking History Among Patients
 
**Insight**
The smoking history chart revealed that many diabetes patients were categorized as former smokers and current smokers. Smoking history appeared to be one of the common characteristics observed among patients in the dataset.
 
**Real-World Context**
Smoking may contribute to poor blood circulation and other health complications that can worsen diabetes conditions. In many communities, smoking remains a major public health issue linked to chronic diseases.
 
**Recommendation**
Hospitals and healthcare organizations should strengthen smoking cessation programs and include diabetes education in anti-smoking campaigns. Patients with smoking history may also benefit from regular health monitoring and counseling services.
 
---
 
### ╰┈➤ Yearly Trend of Diabetes Cases
 
**Insight**
The line graph displayed a noticeable increase in diabetes cases around 2019 compared to other years in the dataset. This trend may indicate increased diagnosis, lifestyle changes, or improved health screening activities during that period.
 
**Real-World Context**
Monitoring yearly health trends is important because sudden increases in disease cases may place additional pressure on healthcare services and medical resources. Changes in lifestyle patterns and public health conditions may also influence diabetes rates over time.
 
**Recommendation**
Healthcare institutions should continue using data analytics and dashboards to monitor yearly diabetes trends. Consistent monitoring may help improve healthcare planning, resource allocation, and prevention strategies for future diabetes cases.
