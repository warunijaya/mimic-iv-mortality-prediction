# mimic-iv-mortality-prediction
A machine learning project for predicting in-hospital mortality using MIMIC-IV data.

## MIMIC-IV Dataset

### How to Get Access to MIMIC-IV

To get access to the MIMIC-IV dataset, follow these steps:

1. **Create an Account**  
   First, you need to register on the [PhysioNet website](https://physionet.org). If you don’t already have an account, create one.

2. **Request Access**  
   You can apply for access to MIMIC-IV. You’ll need to fill out an application on PhysioNet. This process also includes signing a data use agreement to ensure that you’re following all ethical and legal guidelines.
   
3. **Provide Referral Details**
   You will be asked to give contact details of a referral. This can be a colleague, instructor or a supervisor.

3. **Download the Data**  
   Once you’re approved, you’ll be able to download the dataset from PhysioNet. Each dataset has the requirements listed (like signing an aggreement, completing a short course) at the end of the webpage.

For more detailed instructions, check out the [MIMIC-IV Access Documentation](https://physionet.org/content/mimiciv/3.1/).

---

## A Brief Overview of the `hosp` Dataset

The `hosp` dataset is part of MIMIC-IV and includes detailed information about patient admissions to the hospital, including things like their diagnoses, treatments, medications, and lab results.

Here are some of the key tables and what they represent:

### **1. `ADMISSIONS` Table**

This table tracks each individual hospital admission. It includes:

- **HADM_ID**: A unique ID for each admission.
- **SUBJECT_ID**: A unique ID for each patient.
- **ADMITTIME**: The date and time the patient was admitted to the hospital.
- **DISCHTIME**: The date and time the patient was discharged.
- **ADMISSION_TYPE**: The type of admission (e.g., emergency, elective).
- **ADMISSION_LOCATION**: Where the patient was admitted from (e.g., emergency department, another hospital).
- **DISCHARGE_LOCATION**: Where the patient went after discharge (e.g., home, ICU).
- **INSURANCE**: The patient's insurance type.
- **LANGUAGE**, **RELIGION**, **MARITAL_STATUS**, **ETHNICITY**: Various demographic information about the patient.

For more details, you can refer to the [ADMISSIONS table documentation](https://mimic.mit.edu/docs/iv/modules/hosp/admissions/).

### **2. `DIAGNOSES_ICD` Table**

This table contains diagnostic codes related to the patient's conditions, mapped to ICD-9 or ICD-10 codes.

- **HADM_ID**: ID for the admission.
- **SEQ_NUM**: The sequence number for the diagnosis (e.g., primary or secondary diagnosis).
- **ICD9_CODE**: The ICD-9 code for the diagnosis (though newer data includes ICD-10 codes).
- **ICD10_CODE**: The ICD-10 code for the diagnosis (when applicable).

Check out the full details in the [DIAGNOSES_ICD table documentation](https://mimic.mit.edu/docs/iv/modules/hosp/diagnoses_icd/).

### **3. `PRESCRIPTIONS` Table**

This table lists the medications prescribed to patients during their hospital stay.

- **HADM_ID**: The ID for the admission.
- **SUBJECT_ID**: The ID for the patient.
- **DRUG**: The name of the drug.
- **STARTDATE** and **ENDDATE**: The dates when the medication was started and stopped.
- **DOSE_VAL_RX**: The dose prescribed.
- **DOSE_UNIT_RX**: The unit of measurement for the dose (e.g., mg, ml).

More information is available in the [PRESCRIPTIONS table documentation](https://mimic.mit.edu/docs/iv/modules/hosp/prescriptions/).

### **4. `LABEVENTS` Table**

This table includes results from laboratory tests performed during a hospital stay.

- **SUBJECT_ID**: The patient’s ID.
- **HADM_ID**: The hospital admission ID.
- **ITEMID**: The ID for the specific lab test.
- **CHARTTIME**: The time the test result was recorded.
- **VALUE**: The test result value.
- **VALUEUOM**: The unit of the test result (e.g., mg/dL).

For further details, refer to the [LABEVENTS table documentation](https://mimic.mit.edu/docs/iv/modules/hosp/labevents/).

---

For a more comprehensive understanding of the dataset, including the relationships between these tables, you can explore the full [MIMIC-IV Hospital Module documentation](https://mimic.mit.edu/docs/iv/modules/hosp/).

---

## Problem Statement

### Background
The accurate prediction of in-hospital patient mortality is a critical task in healthcare systems. Identifying high-risk patients early during their hospital stay can enable clinicians to allocate resources effectively, provide timely interventions, and improve patient outcomes. The MIMIC-IV dataset, a comprehensive clinical database, provides a wealth of information such as demographics, vital signs, lab measurements, and medications, making it a valuable resource for building predictive models.

### Objective
The objective of this project is to develop a machine learning model to predict **in-hospital mortality** (whether a patient dies during their hospital stay) within the first 3 hours of admission using the data available in the MIMIC-IV dataset. The model aims to support clinical decision-making by providing a risk score that can guide prioritization and intervention strategies.

### Problem Scope
The project focuses on leveraging structured data, including:
- **Demographics**: Age, gender, ethnicity, etc.
- **Admission Details**: Admission type, admission location, and during the first 3 hours of admission.

The primary challenge is to build a robust model that generalizes well across diverse patient populations while avoiding target leakage, particularly from features like `deathtime`, which directly indicates mortality.

### Key Questions
1. Can we predict in-hospital mortality within the first 3 hours of admission using routinely collected clinical data?
2. What are the most important features influencing mortality risk in the MIMIC-IV dataset?
3. How does the predictive performance of different machine learning models (e.g., Logistic Regression, Random Forest, LightGBM, Neural Networks) compare in this context?


### Significance
This project has the potential to improve patient outcomes by identifying high-risk patients early, helping clinicians prioritize interventions, and optimizing hospital resource utilization. Additionally, it demonstrates the applicability of machine learning in critical care settings and lays the groundwork for future clinical decision-support tools.

## Data preprocessing steps

### Categorical mapping
Used to map ordered categorical variables to numerical values for 'Race' column and 'Gender' column.  

In the case of the `Race` column, categorical mapping was applied to simplify the data by grouping races into broader categories:
- `WHITE`
- `BLACK/AFRICAN`
- `HISPANIC`
- `ASIAN`
- `OTHER`

This mapping reduces complexity and ensures the model can handle the data effectively.


### Dummy Variables
Used to handle nominal categorical variables by converting them into binary columns.
I used this method for 'race_grouped','gender', 'admission_type','insurance', 'admission_location'

## Startified sampling

### Reducing the Ratio of Training and Validation Sets Based on `y`

In imbalanced datasets, reducing the ratio of training and validation sets based on the target variable (`y`) ensures that both sets maintain similar distributions of the target class. This helps improve model evaluation by providing a balanced and representative validation set.

In this project, the target variable (`hospital_expire_flag`) has 2% ratio between the two class distributions (Death/Alive). Using Startified sampling, downsampled training set with 10% of negative class giving 20 % ratio two class distributions.

### Benefits
- Ensures fair performance evaluation during validation.
- Prevents overfitting to the dominant class.
- Enhances the generalizability of the model to unseen data.

## Model performances

### Logistic_Regression_report

### Random Forest Classification Report

### LightGBM Classification Report

### Neural Network Classification Report


The classification reports reveal a notable imbalance in performance across the classes. The "dead" class exhibits significantly lower precision and recall, reflecting challenges in accurately detecting and classifying patients who fall into this category.In contrast, the "dead" class exhibits significantly lower precision and recall, reflecting challenges in accurately detecting and classifying patients who fall into this category.

### ROC-AUC Values

AUC (Area Under the Curve) refers to the area under the Receiver Operating Characteristic (ROC) curve. It measures how well a model distinguishes between two classes—in this case, patients who survive vs. those who die in the hospital.

- **AUC = 1.0** : Perfect model that distinguishes between classes with 100% accuracy.
- **AUC = 0.5** : Random guess, equivalent to flipping a coin.
- **AUC < 0.5** : Worse than random guessing; the model is misclassifying the classes.

For the project, following ROC-AUC values were calculated for different models
- Logistic Regression ROC-AUC: 0.77
- Random Forest ROC-AUC: 0.72
- LightGBM ROC-AUC: 0.77
- Neural Network ROC-AUC: 0.77

The highest AUC 0.77 obtained for Logistic Regression, LightGBM and Neural Network models. 


## Discussion

### Feature importance
Feature importance is a technique used to assess the impact of each feature (or variable) in a dataset on the predictions made by a machine learning model. Understanding feature importance enhances model interpretability, facilitates feature selection, and supports improved decision-making.

In this project, feature importance analysis were conducted for both Random Forest and LightGBM classifier models. Both models identified age as the most significant feature influencing predictions.

For the Random Forest model, additional features with high importance include:

- insurance_Medicare
- race_grouped_WHITE
- admission_location_EMERGENCY ROOM
- admission_location_PHYSICIAN REFERRAL

In contrast, the LightGBM classifier model highlighted the following features as particularly important:

- race_grouped_OTHER
- admission_location_TRANSFER FROM HOSPITAL
- admission_location_TRANSFER FROM SKILLED NURSING FACILITY

### Limitations
The project utilized only admissions and patient data. Incorporating additional datasets such as transfers, labs, procedures, and prescriptions could potentially enhance the final results.
