# Student Performance Analysis

This project is a comprehensive exploratory and predictive analysis of student test scores in math, reading, and writing. It investigates how socioeconomic, demographic, and preparation factors relate to academic outcomes, then uses Decision Tree classifiers with SMOTE oversampling to predict both binary pass/fail results and letter grade classifications.

## Table of Contents
* About the Dataset
* Project Overview
* Model Results
* Summary

---

## About the Dataset

The dataset (`StudentsPerformance.csv`) contains **1,000 student records** with no missing values across 8 columns:

| Column | Type | Values |
|:---|:---|:---|
| gender | categorical | female, male |
| race/ethnicity | categorical (ordered) | group A – group E |
| parental level of education | categorical (ordered) | some high school → master's degree |
| lunch | categorical | standard, free/reduced |
| test preparation course | categorical | none, completed |
| math score | numeric | 0–100 |
| reading score | numeric | 0–100 |
| writing score | numeric | 0–100 |

Score columns are later transformed into binary Pass/Fail labels (threshold: 60) and letter grades (F, D, C, B, A) for classification tasks.

---

## Project Overview

### A. Data Processing

* Categorical columns are cast to ordered `pd.Categorical` types to enable proper sort ordering in visualizations and pivot tables.
* Score columns are binned into **Pass/Fail** (`[-1, 60, 100]`) and **Letter Grades** (`F, D, C, B, A` with thresholds at 60, 70, 80, 90, 100) using `pd.cut`.
* An extended grade scale (`F, D-, D, D+, C-, C, C+, B-, B, B+, A-, A, A+`) is also defined for finer analysis.

### B. Data Analysis

#### Gender and Test Scores
* Females score higher on average in reading (72.6 vs 65.5) and writing (72.5 vs 63.3).
* Males score higher on average in math (68.7 vs 63.6).

#### Ethnicity and Economic Inequality
* A pivot table and percentage chart reveal the proportion of students on free/reduced lunch across ethnic groups, exposing economic disparities by ethnicity.
* Economic status (standard vs free/reduced lunch) is shown to correlate with score distributions across all three subjects.

#### Parental Education
* Students whose parents have higher education levels complete the test preparation course at slightly higher rates.
* Parental education level is analyzed against test score distributions using boxplots, with 3D surface plots showing interaction effects between ethnicity and parental education on reading and writing scores.

#### Test Preparation Course
* Students who completed the preparation course score higher across all three subjects. This effect is visualized through histogram distributions, countplots of pass/fail rates, and grade-level proportions.

### C. Data Analysis by Results (Pass/Fail)

* Score columns are binned into binary Pass/Fail using a threshold of 60.
* Pass/fail counts are visualized by gender, test preparation course, and lunch status across all three subjects.
* Parental education's influence on failure rate is plotted as a bar/point chart showing failure percentages per education level.

### D. Data Analysis by Grades (A–F)

* Score columns are binned into 5 letter grades.
* Grade distributions are visualized by test preparation course completion and lunch type.
* For each categorical variable, the percentage achieving each grade is plotted across score types.
* 3D surface plots show combined effects of parental education level and race/ethnicity on mean reading and writing scores.

### E. Modeling — Feature Importance for Pass/Fail

* A **Decision Tree Classifier** is fitted separately for each score subject to identify the most important features for predicting pass/fail.
* **SMOTE oversampling** is applied to address class imbalance in the binary labels.
* All categorical features are encoded numerically (ordinal codes) before fitting.
* Feature importances are visualized as horizontal bar charts ranked by contribution.

### F. Modeling — Feature Importance for Grade Classification

* The same Decision Tree + SMOTE approach is applied for the 5-class grade prediction task (F, D, C, B, A).
* Separate models are trained per score subject (math, reading, writing), with SMOTE balancing applied per class.
* Feature importances are visualized per subject.

---

## Model Results

### Pass/Fail Classification (Decision Tree + SMOTE, evaluated on oversampled training set)

| Subject | Accuracy | Macro F1 | Support (per class) |
|:---|:---:|:---:|:---:|
| Math Score | 0.76 | 0.76 | 661 |
| Reading Score | 0.78 | 0.77 | 725 |
| Writing Score | 0.79 | 0.79 | 699 |

#### Per-class breakdown — Math Score

| Class | Precision | Recall | F1 |
|:---|:---:|:---:|:---:|
| Fail | 0.72 | 0.85 | 0.78 |
| Pass | 0.82 | 0.66 | 0.73 |

#### Per-class breakdown — Reading Score

| Class | Precision | Recall | F1 |
|:---|:---:|:---:|:---:|
| Fail | 0.75 | 0.84 | 0.79 |
| Pass | 0.82 | 0.71 | 0.76 |

#### Per-class breakdown — Writing Score

| Class | Precision | Recall | F1 |
|:---|:---:|:---:|:---:|
| Fail | 0.75 | 0.86 | 0.80 |
| Pass | 0.83 | 0.72 | 0.77 |

### Grade Classification — A to F (Decision Tree + SMOTE)

| Subject | Accuracy | Macro F1 |
|:---|:---:|:---:|
| Math Score | 0.54 | 0.52 |
| Reading Score | ~0.55 | ~0.54 |
| Writing Score | ~0.56 | ~0.55 |

#### Per-class breakdown — Math Grade

| Grade | Precision | Recall | F1 |
|:---|:---:|:---:|:---:|
| A | 0.56 | 0.86 | 0.68 |
| B | 0.51 | 0.57 | 0.54 |
| C | 0.50 | 0.49 | 0.49 |
| D | 0.49 | 0.42 | 0.45 |
| F | 0.68 | 0.33 | 0.45 |

---

## Summary

* **Key analytical findings:** Lunch status (a proxy for economic situation) is consistently one of the strongest predictors of test scores across all subjects. Students on free/reduced lunch score noticeably lower. Test preparation course completion has a clear positive effect. Gender differences are subject-specific: females outperform in reading and writing, males in math.
* **Pass/Fail prediction:** Decision Trees achieve 76–79% accuracy across subjects, with the model tending toward higher recall on the Fail class (better at catching failures than correctly identifying passes).
* **Grade classification:** The 5-class grade task is substantially harder, with accuracy around 54–56%. The model performs best on extreme grades (A and F) and struggles most with middle grades (C and D), reflecting the continuous and overlapping nature of score distributions.
* **Feature importance:** `lunch` and `test preparation course` consistently rank as the most predictive features for pass/fail outcomes, while `gender` and `race/ethnicity` contribute less once economic proxies are accounted for.
