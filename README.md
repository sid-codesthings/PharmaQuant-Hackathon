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
To determine the key features that best predict whether a diabetic patient will be readmitted within 30 days or not.

This is formulated as a binary classification problem -

**0 → No readmission within 30 days**

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
 
      





























