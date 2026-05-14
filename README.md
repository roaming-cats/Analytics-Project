# ✴︎ Data Cleaning & Preparation Documentation ✴︎
Using the CLEAN framework (Conceptualize, Locate, Evaluate, Augment, Note)
---
 
## ╰┈➤ Conceptualize the Data
 
**What does each row represent?**
 
Each row represents a unique clinical encounter or medical profile of an individual within a specific year. It captures a snapshot of their demographic background, lifestyle choices (smoking), and vital clinical markers used to assess the presence of diabetes.
 
---
 
## ╰┈➤ Locate Solvable Problems
 
### 1. Duplicates found
 
- Removed 14 duplicates
### 2. Inconsistent casing format
 
- Used PROPER formula to 35806 rows for proper casing
### 3. Less than or equal to 5 years old having "No Info" values (5505 rows)
 
- Imputation; I interpreted the smoking history column as only targeted on first hand smoking, so I based my understanding on this premise. Based on that premise, I considered that 5 years old and under do not have the capacity to be smoking, so I just changed the values to "Never"
### 4. Less than or equal to 5 years old having "Not Currently", "Ever", and "Current" smoking history values (103 rows)
 
- Imputation; Just like the previous issue, I considered that children aged 5 years old and under are unlikely to have a smoking history or to have smoked previously. Therefore, any smoking history values ("Not Current", "Ever", and "Current") for this age group were changed as "Never"
---
 
## ╰┈➤ Evaluate Unsolvable Issues
 
### 1. BMI of > 80
 
- I kept the outliers since they might be real events. 
### 2. Ambiguity between "Former" and "Not Current" values (15713 rows)
 
- Smoking history had both "Former" and "Not Current" categories, which seem similar but may not mean exactly the same thing. To avoid mixing unclear data, they were kept as separate categories. I assumed "Former" means a clear past smoker, while "Not Current" only means the person is not smoking at the moment, but it does not clearly confirm whether they ever smoked before.
---
 
## ╰┈➤ Augment the Data
 
### 1. Created `age_group` column for grouping ages into categories (like Child, Adult, and Senior) to see how diabetes risks change at different stages of life
 
- If age is below 13, classify as "Child."
- If age is below 20, classify as "Teen."
- If age is below 40, classify as "Young Adult."
- If age is below 60, classify as "Middle-Aged."
- If age is below 80, classify as "Senior."
- If age is 80 or above, classify as "Elderly."
### 2. Created a new column called `race` to combine the 5 separate race columns into one `race` label to make the data easier to read. After that, I deleted the columns "race:AfricanAmerican", "race:Asian", "race:Caucasian", "race:Hispanic", "race:Other" since they are not needed because of the race column.

<img width="597" height="38" alt="image" src="https://github.com/user-attachments/assets/e3c956e1-0adb-4867-bc7b-017f701e1073" />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img width="128" height="118" alt="image" src="https://github.com/user-attachments/assets/26928f53-1119-4e06-96cd-32844b9107ff" />

### 3. Added `patient_id` to uniquely identify each patient and `race_id` to keep race categories organized and consistent for analysis
 
| race_id | Race             |
|---------|------------------|
| r-1     | African American |
| r-2     | Asian            |
| r-3     | Caucasian        |
| r-4     | Hispanic         |
| r-5     | Other            |
 
- patient_id: p-1, p-2, p-3, p-4, … p-99986
---
 
## ╰┈➤ Note and Document

<img width="1290" height="704" alt="image" src="https://github.com/user-attachments/assets/bcd9e5f4-30e3-49bd-a618-a613c2c02d0a" />
