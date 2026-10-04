# Obesity Detection Model 

Assessing the Influence of Height and Weight on Machine Learning Based Obesity Classification.

---
## 1. Project Overview

This project compares several machine learning algorithms for classifying obesity levels into seven categories. The objective is not only to determine which models will obtain the highest performance, but also to investigate whether strong performance depends on information that is closely related to the definition of the target label. 

Body Mass Index is calculated using Height and Weight; models may use these two variables to reconstruct obesity categories instead of learning meaningful relationships from lifestyle information.  

We are comparing five algorithms using the complete feature set and then performing a controlled feature-removal ablation in which only height and weight are removed. The records, data splits, random seeds, preprocessing, model settings, and evaluation procedures remain unchanged. 

---
## 2. Background

Obesity is a multiclass prediction problem in which eating habits, physical activity, demographic characteristics, and physical measurements are used to classify an individual into one of seven weight-status categories. The selected dataset is widely used for introductory machine learning because it includes both numerical and categorical variables and has a clearly defined target label. 

However, obesity categories are strongly related to the Body Mass Index (BMI), which is calculated using height and weight. As a result, models may achieve high accuracy mainly by relying on these two measurements rather than learning meaningful patterns from lifestyle-related features. This project tests that concern through a controlled ablation experiment. 

---

## 3. Research Question

How do height and weight affect the performance and ranking of ML algorithms for seven-class obesity classification? 


---
## 4. Hypothesis
Removing height and weight is expected to reduce model performance because these variables closely encode BMI-based obesity classes. Tree-based ensemble models may lose more performance than Logistic Regression if their advantage depends on nonlinear relationships between height and weight.

---
## 5. Dataset

**Name:** Estimation of Obesity Levels Based on Eating Habits and Physical Condition  
**Repository:** UCI Machine Learning Repository  
**Dataset ID:** 544  
**DOI:** [10.24432/C5H31Z](https://doi.org/10.24432/C5H31Z)  
**Licence:** CC BY 4.0  
**Download date:** `24/9/2026`  
**Raw file:** `ObesityDataSet_raw_and_data_sinthetic.csv`

### Dataset properties

| Property | Value |
|---|---:|
| Original records | 2,111 |
| Exact duplicate records removed | 24 |
| Cleaned records | 2,087 |
| Predictors | 16 |
| Target column | `NObeyesdad` |
| Target classes | 7 |
| Missing values found | 0 |
| Learning type | Supervised multiclass classification |



---
## 6. Target Classes

“Insufficient Weight” 
“Normal Weight” 
“Overweight-Level-I" 
“Overweight-Level-II" 
“Obesity-Type-I" 
“Obesity-Type-II" 
“Obesity-Type-III" 

### Target classes after duplicate removal

| Class | Records |
|---|---:|
| Obesity Type I | 351 |
| Obesity Type III | 324 |
| Obesity Type II | 297 |
| Overweight Level II | 290 |
| Normal Weight | 282 |
| Overweight Level I | 276 |
| Insufficient Weight | 267 |
| **Total** | **2,087** |

---
## 7. Experiments

To ensure fair comparison, we keep the following unchanged:  

Same records, same training, validation and test splits, one random seed, same preprocessing, same algorithms, same model settings, same primary metric, same execution environment, and same test records. 

## Complete feature set 

All 16 input features are used, including Height and Weight. The four models are trained and evaluated using this full dataset. This gives the baseline accuracy for each model. 

## Feature-removal ablation 

The same models are trained again using the same data split and preprocessing, but Height and Weight are removed. The new accuracy is compared with the baseline accuracy to measure how much those two features affected performance. 

---
## 8. Data Splitting: 

- 70% Training 

- 15% Validation 

- 15% Testing 


---
## 9. Preprocessing

## Numerical variables 

Age, Hight, Weight, FCVC, NCP, CH2O, FAF, TUE 

We will apply:  

1. Median Imputation
2. Standardization 

## Categorical variables 

Gender, SMOKE, CAEC, CALC, MTRANS 

We will apply: 

1. Most-Frequent Imputation. 
2. One-Hot Encoding. 

And all the above preprocessing will be in Pipeline.

---
## 10. Algorithms

1.	Dummy Classifier
2.	Logistic Regression
3.	Decision Tree
4.	Random Forest
5.	Gradient Boosting


These algorithms provide a comparison between a trivial baseline, a linear model, a single nonlinear tree, a bagging ensemble, and a boosting ensemble.

 ---
## 11. Hyperparameter Selection and Freezing

 seed=42

Hyperparameters were selected using Validation Macro-F1. The final test set was not used during model selection.

 

### Candidate settings

| Model | Candidate settings |
|---|---|
| Dummy Classifier | `strategy="most_frequent"` |
| Logistic Regression | `C ∈ {0.1, 1, 10}` |
| Decision Tree | `max_depth ∈ {5, 10, None}` |
| Random Forest | `n_estimators ∈ {100, 300, 500}` |
| Gradient Boosting | `n_estimators ∈ {100, 300, 500}` |

Other parameters were held constant within each model family.

### Selected settings

| Model | Selected setting | Validation Macro-F1 |
|---|---|---:|
| Dummy Classifier | Most frequent | 0.0414 |
| Logistic Regression | `C = 10` | 0.9428 |
| Decision Tree | `max_depth = 10` | 0.9306 |
| Random Forest | `n_estimators = 300` | 0.9191 |
| Gradient Boosting | `n_estimators = 300` | 0.9531 |

 

After selection, these settings were **frozen**. Freezing means that the settings were not changed after viewing the final test results and were reused unchanged in the Height/Weight ablation.

---
## 12. Evaluation Metrics

Primary metric: Macro-F1 

The winner is the model with the highest test of Macro-F1. 

Secondary metrics: 

- Accuracy  
- Precision  
- Recall 
- AUC
- Training time 
- Serialized model size 

Precision and Recall are macro-averaged. AUC is macro one-vs-rest. Macro-F1 is the primary ranking metric.​

---

## 13. Final Full-Feature Results

| Model | Macro-F1 | Accuracy | Macro Precision | Macro Recall | Macro OvR AUC | Training time (s) | Model size (MB) |
|---|---:|---:|---:|---:|---:|---:|---:|
| **Gradient Boosting** | **0.9845** | **0.9841** | **0.9843** | **0.9853** | **0.9994** | 11.7836 | 2.5465 |
| Logistic Regression | 0.9363 | 0.9395 | 0.9372 | 0.9363 | 0.9956 | 0.6247 | **0.0079** |
| Random Forest | 0.9349 | 0.9363 | 0.9393 | 0.9337 | 0.9941 | 2.7265 | 12.8830 |
| Decision Tree | 0.9334 | 0.9363 | 0.9342 | 0.9340 | 0.9875 | **0.0866** | 0.0228 |
| Dummy Classifier | 0.0413 | 0.1688 | 0.0241 | 0.1429 | 0.5000 | 0.0239 | 0.0060 |

### Main result

Gradient Boosting ranked first according to the predefined primary metric, achieving a test Macro-F1 of 0.9845. It also achieved the highest Accuracy, macro Precision, macro Recall, and macro one-vs-rest AUC.

The efficiency results show important trade-offs:

- Decision Tree trained fastest among the learned models.
- Logistic Regression produced the smallest learned model.
- Random Forest produced the largest serialized model.
- Gradient Boosting provided the strongest predictive performance but required the longest training time.


## 14. Height/Weight Ablation

For the ablation, only `Height` and `Weight` were removed. The following remained unchanged:


### Ablation results

| Model | Macro-F1 | Accuracy | Macro Precision | Macro Recall | Macro OvR AUC |
|---|---:|---:|---:|---:|---:|
| **Gradient Boosting** | **0.8562** | **0.8567** | **0.8612** | **0.8547** | 0.9693 |
| Random Forest | 0.8267 | 0.8312 | 0.8266 | 0.8285 | **0.9766** |
| Decision Tree | 0.6758 | 0.6879 | 0.6815 | 0.6794 | 0.8936 |
| Logistic Regression | 0.6123 | 0.6369 | 0.6363 | 0.6278 | 0.8966 |
| Dummy Classifier | 0.0413 | 0.1688 | 0.0241 | 0.1429 | 0.5000 |

### Change in performance

| Model | Δ Macro-F1 | Δ Accuracy | Δ Precision | Δ Recall | Δ AUC |
|---|---:|---:|---:|---:|---:|
| Gradient Boosting | −0.1283 | −0.1274 | −0.1231 | −0.1306 | −0.0301 |
| Logistic Regression | **−0.3240** | **−0.3025** | **−0.3009** | **−0.3085** | −0.0990 |
| Random Forest | −0.1082 | −0.1051 | −0.1126 | −0.1052 | **−0.0175** |
| Decision Tree | −0.2575 | −0.2484 | −0.2528 | −0.2546 | −0.0938 |
| Dummy Classifier | 0.0000 | 0.0000 | 0.0000 | 0.0000 | 0.0000 |

---
## 15. Limitations

The public dataset includes a substantial synthetic component and should be treated as a machine-learning benchmark rather than a representative clinical population. The task is **cross-sectional obesity-level classification**, not prediction of future obesity and not clinical diagnosis. Only one random seed was used, and standard preprocessing was done without advanced feature extraction, and the feature rankings show model importance rather than direct causal effects.

---
## 16. Conclusion

Gradient Boosting achieved the highest full-feature Macro-F1. Weight and Height were the two most influential features, and removing them reduced performance substantially. However, Gradient Boosting remained the best-performing model after the ablation. The hypothesis was therefore partially supported: Height and Weight were highly influential, but they did not fully explain Gradient Boosting’s advantage. 

---

## 17. Reproduction Instructions
### Google Colab

1. Open `obesity_assignment.ipynb` in Google Colab.
2. Upload `ObesityDataSet_raw_and_data_sinthetic.csv` when requested.
3. Select **Runtime → Run all**.
4. Confirm that the notebook produces:
   - `full_results_all_metrics.csv`;
   - `ablation_results_all_metrics.csv`;
   - `comparison_all_metrics.csv`;
   - classification reports;

---

## 18. Group Members and Contributions

All four team members participated in:
- reviewing the final experiment design;
- checking that the code runs from the beginning;
- verifying that no result was copied from a paper or leaderboard;
- preparing and reviewing the five-slide presentation;


| Member | Student ID | 
|---|---|
| **Noureen Shaji** | `700053294` | 
| **Nuha AlMasalmeh** | `201670003` | 
| **Akhila Asgar** | `700038141` | 
| **Rhea Mary Josi** | `700053545` | 


---

## 19. AI-Assistance Disclosure

AI tools were used to assist with the code and improve wording and formatting.

All code was reviewed and executed by the group. Every reported result was generated by the project workflow. No performance result was copied from an AI response, research paper, public notebook, or leaderboard.

