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
Define problem
Draw timeline
Explain preprocessing steps
Explain startified sampling
Show each model performance
Discussion:
* Discuss feature importance
* Limitations
* Possible improvements