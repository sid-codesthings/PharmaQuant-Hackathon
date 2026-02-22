# Predicting Avoidable Readmissions in U.S. Hospitals facing re-admission penalties (Diabetes Dataset)
*(U.S. Diabetes Dataset – 30-Day Readmission Prediction)*

---

## Project Details
<br>

Hospital readmissions within 30 days of discharge significantly impact healthcare costs and hospital reimbursement policies in the United States. Under the Hospital Readmissions Reduction Program(HRRP) Act, hospitals in the US face financial penalties for violating a certain threshold of such readmissions.

This project builds predictive models to identify high-risk diabetic patients likely to be readmitted within 30 days, using clinical, demographic, and treatment-related features.

**The goal is to:**

* **Predict which patients are highly likely to have readmission within 30 days:** Develop a binary classification model to forecast which patients are likely to return.
* **Identify key risk factors enabling such re-admissions:** Use feature importance to determine which clinical and demographic variables most influence readmission rates.
* **Provide actionable insights to hospitals to avoid such re-admissions:** Offer data-driven insights to help hospitals mitigate penalties under the HRRP.

# Dataset

The dataset used is the U.S. Diabetes 130-Hospitals Dataset provided by Pharmaquant Pvt. Ltd. It contains over 100,000 hospital encounters of diabetic patients and 47 features.

**Clinical Features**
* num_lab_procedures
* num_procedures
* num_medications
* number_outpatient
* number_emergency
* number_inpatient
* number_diagnoses

**Treatment Related Features**
* admission_type_id
* discharge_disposition_id
* admission_source_id
* time_in_hospital
* change
* diabetesMed 24 medication-related features (metformin to metformin.pioglitazone)

**Demographic Features**
* race
* gender
* age
* weight

# Objective
To determine the key features that best predict whether a diabetic patient will be readmitted within 30 days or not.<br>
This is formulated as a binary classification problem:<br>

**0 → No readmission within 30 days** <br>
**1 → Readmission within 30 days**

# EDA
Exploratory Data Analysis was conducted using:
**Python (Pandas, Matplotlib, Seaborn) for statistical exploration.**
**Power BI for interactive dashboard development and demographic segmentation.**

The objective was to uncover patterns influencing 30-day hospital readmission among diabetic patients and identify high-risk segments before model building.

**Key Findings from Correlation Heatmap:**
* time_in_hospital and num_medications show a strong positive correlation (~0.6)
* num_lab_procedures moderately correlates with num_medications (~0.34)
* num_lab_procedures has a weak negative correlation with number_inpatient (-0.17)
* Readmission itself shows very weak linear correlation with individual variables:
    * time_in_hospital (~0.048)
    * num_lab_procedures (~0.052)
    * num_medications (~0.037)
    * number_inpatient (~0.04)
 
**Interpretations:** <br>
* No single feature linearly explains the readmission.<br>
* Readmission is likely driven by complex, non-linear interactions.

This pointed to the fact that we should experiment more by using ensemble models like Random Forest and XGBoost aside Logistic Regression.
 
**Observations on Readmission Count by Age:**<br>
* Readmission counts increase significantly from age 45 onwards.
* Peak readmission appears in the 65–75 age group.
* Very low readmission among younger groups (5–35).
* Slight decline in extreme elderly (85+), likely due to smaller sample size.

**Interpretation:**

* Older diabetic patients have higher readmission vulnerability.
* Age acts as a risk amplifier, likely interacting with:
   * Number of medications
   * Inpatient history
   * Comorbidities
 
Age seems an important key variable for prediction.

**Observations based on Race and Gender:**<br>
* Caucasian patients show the highest absolute readmission count (due to larger representation in dataset).
* African American patients also show substantial readmission counts.
* Other racial groups have lower absolute counts.
* Readmission counts are relatively balanced across male and female.
* Slight variation exists but gender alone is not a dominant predictor.

**Interpretation:**

Demographic variables alone are not absolute or strong predictors. But some targeted care coordination workflows can be improved based on socio-economic factors of certain races. These variables are useful when combined with clinical features.

**Observations based on Readmission by Weight:**

* Highest readmission counts observed in:
   * 75–100 lbs range
   * 50–75 lbs range
* Extremely high weight ranges show lower counts (likely fewer observations).
* Weight distribution was skewed with significant missing values.

**Interpretation:**

* Weight alone does not strongly determine readmission. It likely interacts with:
* Diabetes severity
* Medication count
* Hospital stay duration
* Missing values were handled via cluster-based median imputation, preserving distribution characteristics.

**Observations on Top 5 Medications by Readmission Rate:**

* Repaglinide (Up) → Highest readmission proportion (~54%)
* Glyburide (Up) → Second highest (~27%)
* Insulin variations contribute smaller proportions
* Medication adjustments (Up/Down/Steady) appear influential

**Interpretation:**

* Medication escalation (“Up”) is strongly associated with readmission. This may indicate:
   * Poor glycemic control
   * Worsening condition
   * Treatment instability
* Medication change is a clinically meaningful predictor.

# Data Cleaning & Pre-processing

The following columns were removed due to irrelevance or excessive missing values:

* encounter_id
* patient_nbr
* payer_code
* medical_specialty
* max_glu_serum
* A1Cresult

**Handling Missing Values:**

The weight column contained significant missing values but was important for analysis. Instead of using KNN (not ideal due to high dimensionality), we clustered patients based on similar demographic features. Imputed missing weight values using the median weight of the respective cluster. This preserved distribution characteristics while avoiding overfitting.

# Models Implemented
We trained and evaluated:

* Logistic Regression
* Random Forest
* XGBoost

Evaluation Metrics:

* Accuracy
* ROC-AUC Score
* Confusion Matrix

# Results

| Model | Accuracy | ROC-AUC |
| :--- | :---: | :---: |
| **Logistic Regression** | Comparable | Moderate |
| **Random Forest** | Comparable | Moderate |
| **XGBoost** 🚀 | Comparable | **Highest** 🏆 |

XGBoost Performed Best beacuse it: <br>
* Captures non-linear relationships
* Handles high-dimensional data well
* Uses L1 & L2 regularization
* Robust against overfitting

**Key Predictors of Readmission (according to the feature importances given by XGBoost)**<br>

**Important features included:**<br>
* time_in_hospital
* number_inpatient
* num_medications
* discharge_disposition_id
* number_emergency
* change
* diabetesMed<br>

These variables significantly influenced readmission probability.



























