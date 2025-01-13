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
The accurate prediction of length of hospital stay is a critical task in healthcare systems. The MIMIC-IV dataset, a comprehensive clinical database, provides a wealth of information such as demographics, vital signs, lab measurements, and medications, making it a valuable resource for building predictive models.

### Objective
The objective of this project is to develop a machine learning model to predict **hospital length of stay** within the first 3 hours of admission using the data available in the MIMIC-IV dataset. 

### Problem Scope
The project focuses on leveraging structured data, including:
- **Demographics**: Age, gender, ethnicity, etc.
- **Admission Details**: Admission type, admission location, and during the first 3 hours of admission.


### Key Questions
1. Can we predict length of stay after the first 3 hours of admissions using routinely collected clinical data?
2. What are the most important features influencing length of stay in the MIMIC-IV dataset?
3. How does the predictive performance of different machine learning models (e.g., Logistic Regression, Random Forest, LightGBM, Neural Networks) compare in this context?


### Significance
The significance of a hospital length of stay (LOS) project lies in its ability to provide insights and drive improvements across various dimensions of healthcare delivery, including patient outcomes, operational efficiency, and cost management.

Reducing the average LOS can save a hospital millions annually while improving patient outcomes.Also, a better understanding of LOS drivers can lead to innovations in care, such as enhanced recovery after surgery or better discharge planning systems.

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


## Model performances

The classification report reveals a notable imbalance in performance across the classes. The "dead" class exhibits significantly lower precision and recall, reflecting challenges in accurately detecting and classifying patients who fall into this category.In contrast, the "dead" class exhibits significantly lower precision and recall, reflecting challenges in accurately detecting and classifying patients who fall into this category.

### RMSE Values

Root Mean Squared Error (RMSE) is a widely used metric for evaluating the performance of regression models.
-**Definition** : RMSE measures the average magnitude of the error between predicted values and actual values in a regression model.
It is calculated as the square root of the average of the squared differences (errors) between predictions and true values.
A smaller RMSE value indicates better model performance, as predictions are closer to the actual values.


For the project, following RMSE values were calculated for different models
- Linear Regression RMSE: 166.79281728071933
- Random Forest RMSE: 169.8457711104025
- LightGBM RMSE: 166.10652711444334
- Neural Network RMSE: 

In this project,all regression models predict RMSE values between 166-169 hours for patient length of stay. This means that, on average, all these models predictions are off by about 166-169 hours.


### Predictions vs Actual graphs 

The first and the second graphs are scatter plots comparing the actual hospital stay durations (on the x-axis) with the predicted hospital stay durations (on the y-axis) made by the linear regression model and Random Forest regression model respectively. 

- Diagonal Red Line:
The red dashed line represents the "ideal" scenario where the predictions exactly match the actual values. For example, if a point lies on this line, the model has perfectly predicted the hospital stay duration for that instance.

- Scatter Points:
Each blue dot represents a single patient. The x-coordinate of a dot shows the actual hospital stay duration, and the y-coordinate shows the predicted value for that patient.

- Concentration Near the Origin:
Most points are clustered near the origin (low values for both actual and predicted durations), indicating that the majority of hospital stays are relatively short.

- Prediction Underestimation:
For larger hospital stay durations (on the right-hand side of the graphs), many points are far below the red line. This indicates that the models tend to underestimate hospital stay durations, particularly for long stays.

- Wide Spread:
There’s a significant spread of points below the red line, which suggests the models struggle with accurately predicting longer hospital stays. 


## Discussion

### Feature importance
Feature importance is a technique used to assess the impact of each feature (or variable) in a dataset on the predictions made by a machine learning model. Understanding feature importance enhances model interpretability, facilitates feature selection, and supports improved decision-making.

In this project, feature importance analysis were conducted for Random Forest model. The most significant feature is the "age" influencing predictions.

For the Random Forest model, additional features with high importance include:

-  admission_location_TRANSFER FROM HOSPITAL
- admission_location_INTERNAL TRANSFER TO OR FROM PSYCH
- gender


### Limitations
The project primarily utilized admissions and patient data. Incorporating additional datasets, such as transfers, lab results, procedures, and prescriptions, could significantly enhance the model's performance and overall results.

Other recommendations for improving the models include:

- Applying logarithmic or square-root transformations to the target variable (time_in_hospital) to reduce the influence of outliers and normalize its distribution.
- Analyzing and addressing extreme outliers to minimize their impact on model accuracy and reliability.
