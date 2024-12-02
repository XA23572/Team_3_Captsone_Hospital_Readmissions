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
![image](https://github.com/user-attachments/assets/87c1ba0b-3016-4ebd-9704-cfb1e37ffd3f)


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

## Results

![image](https://github.com/user-attachments/assets/66b2a683-417a-449f-b191-9c348c516dac)   ![image](https://github.com/user-attachments/assets/b8dedb9d-3d92-4d0d-88cf-7dcf5aa6a1e3)



