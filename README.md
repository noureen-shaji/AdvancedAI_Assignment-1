# Obesity Detection Model 

Evaluating anthropometric shortcut learning in multiclass obesity classification. Assessing the Influence of Height and Weight on Machine Learning Based Obesity Classification. An Ablation Study of Height and Weight in Machine Learning Based Obesity Classification 

## 1. Project Overview

This project compares several machine learning algorithms for classifying obesity levels into seven categories. The objective is not only to determine which models will obtain the highest performance, but also to investigate whether strong performance depends on information that is closely related to the definition of the target label. 

Body Mass Index is calculated using Height and Weight; models may use these two variables to reconstruct obesity categories instead of learning meaningful relationships from lifestyle information.  

We are comparing five algorithms using the complete feature set and then performing a controlled feature-removal ablation in which only height and weight are removed. The records, data splits, random seeds, preprocessing, model settings, and evaluation procedures remain unchanged. 

**Background**

Obesity is a multiclass prediction problem in which eating habits, physical activity, demographic characteristics, and physical measurements are used to classify an individual into one of seven weight-status categories. The selected dataset is widely used for introductory machine learning because it includes both numerical and categorical variables and has a clearly defined target label. 

However, obesity categories are strongly related to the Body Mass Index (BMI), which is calculated using height and weight. As a result, models may achieve high accuracy mainly by relying on these two measurements rather than learning meaningful patterns from lifestyle-related features. This project tests that concern through a controlled ablation experiment. 

**Research Question**

How do height and weight affect the performance and ranking of ML algorithms for seven-class obesity classification? 
**Hypothesis**
Removing height and weight is expected to reduce model performance because these variables closely encode BMI-based obesity classes. Tree-based ensemble models may lose more performance than Logistic Regression if their advantage depends on nonlinear relationships between height and weight.


Dataset:
•	Dataset: Estimation of Obesity Levels Based on Eating Habits and Physical Condition.
•	Source: UCI Machine Learning Repository.
•	UCI ID: 544
•	DOI: 10.24432/C5H31Z
•	License: CC BY 4.0
•	Original records: 2,111
•	Predictors: 16
•	Target: "NObeyesdad"
•	Classes: 7
•	Known limitation: 77% of the released records are reported as synthetically generated, while 23% were collected through a web platform.

Target Classes: 

“Insufficient Weight” 

“Normal Weight” 

“Overweight-Level-I" 

“Overweight-Level-II" 

“Obesity-Type-I" 

“Obesity-Type-II" 

“Obesity-Type-III" 

**Preprocessing:**

Numerical variables 

Age, Hight, Weight, FCVC, NCP, CH2O, FAF, TUE 

We will apply:  

Median Imputation
Standardization 

Categorical variables 

Gender, SMOKE, CAEC, CALC, MTRANS 

We will apply: 

Most-Frequent Imputation. 
One-Hot Encoding. 

And all the above preprocessing will be in Pipeline.

Dataset limitation
The public dataset includes a substantial synthetic component and should be treated as a machine-learning benchmark rather than a representative clinical population. The task is **cross-sectional obesity-level classification**, not prediction of future obesity and not clinical diagnosis.

