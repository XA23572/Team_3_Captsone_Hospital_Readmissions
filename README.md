## Introduction:

Hospital readmission occurs when a patient is readmitted shortly after discharge, often due to complications, poor recovery, or inadequate post-discharge care. 
This issue not only burdens healthcare systems but also costs the U.S. over $17 billion annually in preventable readmissions, highlighting gaps in care quality. 
By leveraging predictive models, this project aims to identify high-risk patients, enabling efficient resource allocation, personalized care plans, and extended support to improve outcomes. 
Through the integration of machine learning and advanced techniques, this project addresses a critical real-world problem, demonstrating the transformative power of 
data-driven insights in healthcare.


## Research Questions:

1) Can we develop a predictive model to identify patients at high risk of readmission?

   This focuses on using predictive modeling to identify at-risk patients, enabling efficient resource allocation, reducing costs, and improving overall healthcare quality.

2) Can we predict the reason for the readmission?

   This aims to uncover specific reasons for readmissions, supporting targeted interventions, better discharge planning, and enhanced patient care coordination.

## Key Differentiators of Our Hospital Readmission Prediction Model   

1) Integration of Clinical Notes with Structured Data
   Unlike many existing models that rely solely on structured data, our product incorporates unstructured data such as clinical notes.

2) Prediction of Readmission Reasons
   While most products focus on binary readmission prediction (yes/no), your model goes further by predicting specific readmission reasons through multi-label classification. This added layer of granularity provides actionable insights for healthcare providers to address underlying causes.

   
## Dataset:

For this project, we have used the MIMIC-III Clinical Dataset. It is a publicly available dataset containing de-identified health information from over 40,000 critical care patients at 
Beth Israel Deaconess Medical Center. It includes demographics, vital signs, diagnoses, medications, lab results, and clinical notes, enabling research in healthcare and machine learning.
Researchers are required to formally request access via a process documented on the MIMIC website.
https://physionet.org/content/mimiciii/1.4/

There are two key steps that must be completed before access is granted:
1) The researcher must complete a recognized course in protecting human research participants that includes Health Insurance Portability and Accountability Act (HIPAA) requirements.
2) The researcher must sign a data use agreement, which outlines appropriate data usage and security standards, and forbids efforts to identify individual patients.

This Approval requires at least a week. Once an application has been approved the researcher will receive emails containing instructions for downloading the database from PhysioNetWorks, 
a restricted access component of PhysioNet.

#### Data Flow

![MIMICIIIDataFlowResizedimage - Copy](https://github.com/user-attachments/assets/4d4fbcd4-f5ca-4e3f-ab40-1ff77cf533ad)


## Project Workflow- 

### Step 1: Data Exploration
The dataset includes information on 47,000 patients. Our analysis revealed that patients admitted under the categories "Emergency" and "Urgent" had the highest rates of readmission, while "Elective" and "Newborn" admissions had significantly fewer readmissions. 
Additionally, the dataset contains various types of clinical notes, such as lab reports, discharge summaries, ECG, Echo, Nursing, and Social Work notes. A detailed analysis showed that every patient had a "Discharge Summary," which provides a comprehensive summary of all these note categories. 
Therefore, we focused our work on these discharge summaries. They include critical patient information such as the reason for admission, services performed, medication and drug details, medical history, and, in most cases, social determinants of health (SDOH) data.

### Step 2: Data Preprocessing
We cleaned the patient data by removing records with missing hospital admission IDs and correcting discharge dates that were earlier than admission dates, which were likely data entry errors. This affected about 150 patient records. 
For the clinical notes, we removed unnecessary special characters, eliminated blank lines, and converted all text to lowercase to ensure uniformity and simplify model processing. Additionally, we applied stop word removal to focus on meaningful words and used TF-IDF vectorization to highlight important terms by assigning higher weights to contextually significant words while reducing the influence of common terms. These steps ensured clean and reliable data for analysis.

### Step 3: Exploratory Data Analysis
We conducted thorough analisys to investigate trends in readmissions over different timespans (30, 60, and 90 days) and compared readmission rates across various admission categories. 
We performed correlation analysis to assess the relationship between continuous features and the target variable "Readmission" and used the chi-square test to evaluate the association between categorical variables and readmissions. 
For predicting the reason for readmission, we applied point-biserial correlation analysis to examine continuous input features against the multi-label target "Diagnosis_Category" and conducted chi-square tests on categorical features to identify significant associations.

### Step 4: Model Training and Evaluation
We trained multiple machine learning algorithms, including traditional methods, various ensemble techniques, and advanced ML models, on the dataset. Also, to optimize performance, we applied hyperparameter tuning to refine the models. 
Evaluated model performance using precision, recall, F1-score.
Performed data visualizations to plot the ROC curves and calculated the AUROC values to compare various models performances.

## Assumptions & Challanges

1) Data Entry Issue
   
   One of the significant challenges encountered during this project was identifying and addressing data entry inconsistencies within the dataset. Specifically, for certain records, the discharge date was recorded as earlier than the admit date, which is logically incorrect. Upon analysis, we found that these discrepancies were primarily observed in outpatient services or one-day admissions, suggesting potential data entry issues with the timestamp fields. Such anomalies posed challenges during the calculation of critical features like length of stay (LOS) or when analyzing patient timelines for predicting readmissions, hence we removed such records (around 150) from our final dataset. 

2) Bias Towards Frequent Classes
   
   The MIMIC-III dataset may have an uneven distribution of readmission cases and also the reasons, with certain categories being underrepresented.
While predicting the readmission reason, the model shows bias in some cases toward classes with higher support in the dataset.

3) Evolving Medical Practices and Data Standards

   Medical practices, coding standards (e.g., transition from ICD-9 to ICD-10), and terminology evolve over time. The model may require frequent updates to stay relevant and aligned with current practices.


## Conclusion

This project highlights the capability of predictive models in identifying patients at risk of hospital readmission and uncovering the primary reasons for readmissions. By leveraging unstructured clinical notes along with structured data like ICD-9 codes for diagnosis and procedures, DRG codes, and sentiment analysis from clinical notes, the analysis provides actionable insights to reduce readmissions and enhance patient care.

1) Readmission Risk Prediction
   
The **GRU model** demonstrated superior performance, achieving an F1-score of 0.98 for non-readmissions and 0.85 for readmissions, outperforming other approaches.
Advanced techniques addressed class imbalance challenges, improving predictions for minority classes and enabling hospitals to target high-risk patients for timely interventions.

3) Identifying Readmission Reasons
   
Multi-label classification models effectively uncovered overlapping diagnostic categories and primary causes of readmissions.
Feature selection techniques, such as Chi-Square and Mutual Information, improved model efficiency and classification performance, providing actionable insightsfor discharge planning and targeted interventions. *FCNN with Attention Mechanism tuned using Keras Tuner* worked best out of all the models that we performed.


## Future Scope

1. Studying Comorbidities and Readmission Risk

    Comorbidities often weakly correlate with readmissions due to limited structured data insights.
    Future Direction: Leverage NLP on clinical notes to identify richer interactions for better risk prediction.

2. Using ICD-10 Instead of ICD-9

    ICD-10 offers greater specificity, enabling more precise diagnostics and predictions.
    Benefit: Refines models with detailed inputs, improving accuracy and risk stratification.

3. Incorporating Social Determinants of Health (SDoH)

    SDoH addresses biases by factoring in external influences like food access and transportation.
    Future Focus: Use domain adaptation to improve generalization and real-world accuracy.

4. Remote Health Devices for Better Predictions

    Devices track recovery metrics in real-time, enabling smarter predictions.
    Future Focus: Integrate device data to enhance model precision and adjust dynamically.
   
