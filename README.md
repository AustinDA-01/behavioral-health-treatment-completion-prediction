# Behavioral Health Treatment Completion Prediction

## Overview

Behavioral health organizations face significant challenges related to treatment disengagement and premature program termination. Patients who fail to complete treatment often experience poorer outcomes, increased relapse risk, and higher healthcare utilization costs.

This project analyzes over 1.47 million behavioral health treatment records to identify factors associated with successful treatment completion and develop predictive models capable of identifying high-risk patients at the time of admission.

The objective is to support data-driven interventions that improve treatment retention, patient engagement, and program effectiveness.

---

## Business Problem

Behavioral health providers invest substantial resources in treatment planning, case management, and patient engagement. However, many patients discontinue treatment before achieving program goals.

The goal of this project was to answer the following question:

> Can treatment completion be predicted using information available at admission?

Successfully identifying patients at risk of treatment discontinuation would enable providers to deliver targeted outreach, enhanced support services, and proactive retention interventions.

---

## Dataset

Source: Substance Abuse and Mental Health Services Administration (SAMHSA) Treatment Episode Data Set (TEDS-D)

Dataset Characteristics:

* 1,474,025 treatment discharge records
* 61 predictive features after data cleaning
* National behavioral health treatment population
* Demographic, clinical, socioeconomic, geographic, and treatment-related variables

Target Variable:

* TreatmentCompleted = 1 (Treatment Completed)
* TreatmentCompleted = 0 (Did Not Complete Treatment)

---

## Data Quality Assessment

Several data quality issues were identified and addressed prior to modeling.

### Data Leakage Prevention

Variables only available after treatment completion were removed, including:

* Length of Stay (LOS)
* Discharge Service Variables
* Discharge Employment Status
* Discharge Housing Status
* Other discharge-only features

This ensured the final model used only information available at treatment admission.

### Missing Data Handling

The dataset contained multiple variables using -9 as a coded missing value.

Actions performed:

* Converted coded missing values to null values
* Created missing-value indicator variables
* Removed variables with greater than 75% missingness
* Applied mode-based imputation for remaining missing values

---

## Exploratory Data Analysis

### Finding #1: Employment Status

Treatment completion varied substantially by employment status.

| Employment Status    | Completion Rate |
| -------------------- | --------------- |
| Full-Time Employment | 45.0%           |
| Unemployed           | 29.3%           |

Difference: 15.7 percentage points

### Finding #2: Co-Occurring Mental Health Disorders

Patients with co-occurring mental health disorders completed treatment at significantly lower rates.

| Group                    | Completion Rate |
| ------------------------ | --------------- |
| No Co-Occurring Disorder | 48.5%           |
| Co-Occurring Disorder    | 33.8%           |

Difference: 14.7 percentage points

### Finding #3: Insurance Coverage

Insurance status demonstrated a meaningful relationship with treatment completion.

| Insurance Type | Completion Rate |
| -------------- | --------------- |
| Medicaid       | 56.4%           |
| Uninsured      | 44.7%           |

Difference: 11.7 percentage points

### Finding #4: Treatment Access Delays

Longer wait times before treatment admission were associated with lower treatment completion rates.

| Admission Delay    | Completion Rate |
| ------------------ | --------------- |
| Same-Day Admission | 42.4%           |
| 31+ Day Wait       | 33.2%           |

Difference: 9.2 percentage points

---

## Statistical Analysis

Chi-Square testing identified statistically significant relationships between treatment completion outcomes and several key variables.

Example:

### Co-Occurring Mental Health Disorders

* Chi-Square Statistic: 35,938.41
* p-value: < 0.001

Result:

Patients with co-occurring mental health disorders were significantly less likely to complete treatment.

---

## Feature Engineering

Feature engineering included:

* Missing-value indicators
* Admission-based risk features
* Treatment-access variables
* Substance use indicators
* Socioeconomic risk variables

Final modeling dataset:

* 1.47 million records
* 61 predictive features

---

## Machine Learning Models

Three classification models were evaluated.

| Model               | ROC-AUC |
| ------------------- | ------- |
| Logistic Regression | 0.804   |
| Random Forest       | 0.883   |
| XGBoost             | 0.884   |

### Final Model

Random Forest was selected as the preferred model due to its strong performance and interpretability.

Performance:

* Accuracy: 79%
* Precision: 82%
* Recall: 66%
* F1 Score: 73%
* ROC-AUC: 0.883

---

## Feature Importance

The strongest predictors of treatment completion included:

| Feature                       | Importance |
| ----------------------------- | ---------- |
| State (STFIPS)                | 0.123      |
| Treatment Service Type        | 0.103      |
| Region                        | 0.077      |
| Division                      | 0.075      |
| Housing Information Missing   | 0.072      |
| Education Information Missing | 0.065      |
| Alcohol/Drug Use Category     | 0.038      |
| Primary Substance             | 0.033      |
| Method of Substance Use       | 0.029      |

Key insight:

Treatment completion was influenced by a combination of treatment modality, geographic factors, substance use characteristics, and socioeconomic indicators.

---

## Business Recommendations

Based on the analysis, behavioral health organizations should consider:

### Improve Access to Care

Reduce treatment admission delays and expand rapid-access treatment programs.

### Target High-Risk Populations

Provide enhanced engagement strategies for:

* Unemployed individuals
* Patients with co-occurring mental health disorders
* Uninsured patients

### Strengthen Retention Programs

Develop retention interventions focused on patients with elevated treatment discontinuation risk.

### Monitor Geographic Performance

Investigate regional and state-level differences in treatment outcomes to identify operational best practices.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-Learn
* XGBoost
* SciPy
* Matplotlib
* Seaborn
* Jupyter Notebook

---

## Author

Austin Blunt

MBA, Data Analytics

Data Scientist specializing in machine learning, predictive analytics, healthcare analytics, statistical modeling, and business intelligence.
