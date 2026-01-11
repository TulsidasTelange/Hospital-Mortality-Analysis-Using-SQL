# 🏥 Hospital Mortality Analysis Using SQL

## 📌 Project Overview

This project focuses on analyzing **hospital patient survival data**
using **SQL** to identify mortality trends, risk factors, and
patient demographics associated with hospital deaths.

The goal of this project is to demonstrate **SQL-based data cleaning,
aggregation, and analytical querying**, similar to real-world healthcare
analytics work done by consulting and analytics firms.

------------------------------------------------------------------------

## 🎯 Objectives

-   Analyze hospital mortality rates
-   Identify high-risk patient groups
-   Study the impact of **age, ethnicity, ICU admission, and clinical
    indicators**
-   Perform structured data analysis using **only SQL**

------------------------------------------------------------------------

## 🛠 Tools & Technologies

-   **SQL (MySQL / PostgreSQL compatible)**
-   Relational database concepts\
    ✅ *This is a 100% SQL-based analytical project.*

------------------------------------------------------------------------

## 🗂 Dataset Description

**Dataset Name:** Patient Survival Prediction\
**Source:** Kaggle

🔗 **Data Source Link:**\
https://www.kaggle.com/datasets/mitishaagarwal/patient

**Table Name:** `ps_data`\
**Schema:** `patient_survival`

### Key Columns Used

  -----------------------------------------------------------------------
  Column Name                        Description
  ---------------------------------- ------------------------------------
  hospital_death                     Indicates whether the patient died
                                     (1 = Yes, 0 = No)

  age                                Age of patient

  ethnicity                          Patient ethnicity

  icu_admit_source                   Source of ICU admission

  apache_3j_diagnosis                Clinical diagnosis code

  d1_glucose_max                     Maximum glucose level (Day 1)

  d1_sysbp_min                       Minimum systolic BP (Day 1)
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 🔧 Data Cleaning (SQL)

Handled missing and inconsistent values directly using SQL.

``` sql
UPDATE patient_survival.ps_data
SET ethnicity = CASE
    WHEN ethnicity = '' THEN 'Mixed'
    ELSE ethnicity
END;
```

------------------------------------------------------------------------

## 📊 Key SQL Analyses

### 1️⃣ Overall Hospital Mortality Rate

``` sql
SELECT 
    COUNT(CASE WHEN hospital_death = 1 THEN 1 END) AS total_hospital_deaths,
    ROUND(COUNT(CASE WHEN hospital_death = 1 THEN 1 END) * 100 / COUNT(*), 2) AS mortality_rate
FROM patient_survival.ps_data;
```

### 2️⃣ Mortality by Ethnicity

``` sql
SELECT ethnicity, COUNT(*) AS total_deaths
FROM patient_survival.ps_data
WHERE hospital_death = 1
GROUP BY ethnicity
ORDER BY total_deaths DESC;
```

### 3️⃣ Age-wise Mortality Distribution

``` sql
SELECT 
    CASE
        WHEN age < 30 THEN 'Under 30'
        WHEN age BETWEEN 30 AND 50 THEN '30-50'
        WHEN age BETWEEN 51 AND 70 THEN '51-70'
        ELSE 'Above 70'
    END AS age_group,
    COUNT(*) AS death_count
FROM patient_survival.ps_data
WHERE hospital_death = 1
GROUP BY age_group;
```

------------------------------------------------------------------------

## 📈 Insights

-   Higher mortality observed in elderly patients
-   ICU admission source affects survival outcomes
-   Clinical indicators correlate with mortality risk

------------------------------------------------------------------------

## 🚀 How to Run

1.  Download dataset from Kaggle
2.  Import CSV into SQL database
3.  Execute SQL scripts
4.  Analyze query results

------------------------------------------------------------------------

## 🎓 Skills Demonstrated

-   Advanced SQL
-   Data cleaning & transformation
-   Healthcare data analytics
-   Business-oriented insights

