# 📊 Data Analysis Projects

Exploratory data analysis projects that dig into real-world datasets to surface patterns, relationships, and actionable insights. The focus is on **statistical analysis, multi-dimensional visualization, and interpretable modeling** — understanding the data, not just predicting from it.

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=ffdd54)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![imbalanced-learn](https://img.shields.io/badge/imbalanced--learn-orange?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![Seaborn](https://img.shields.io/badge/Seaborn-blue?style=for-the-badge&logo=python&logoColor=white)

---

## 📂 Projects Overview

| Project | Type | Dataset Size | Key Techniques | Best Performance |
| :--- | :--- | :--- | :--- | :--- |
| **Student Performance Analysis** | EDA + Classification | 1,000 students · 8 features | Pivot analysis, 3D visualization, Decision Tree + SMOTE | Pass/Fail Accuracy: **~78%** |

---

## 🎓 Student Performance Analysis

A comprehensive analysis of how demographic, socioeconomic, and preparation factors influence student test scores in math, reading, and writing — combining multi-faceted EDA with Decision Tree classifiers to rank the most predictive features.

**Dataset:** 1,000 student records with no missing values — 5 categorical features (gender, race/ethnicity, parental education level, lunch type, test preparation course) and 3 numeric score columns (math, reading, writing).

### Highlights

**Exploratory Analysis:**
- Males score higher in math (avg 68.7 vs 63.6); females outperform in reading (72.6 vs 65.5) and writing (72.5 vs 63.3)
- Lunch type — a proxy for economic status — is the most consistent differentiator across all three subjects
- Pivot tables and percentage charts reveal economic inequality distribution across ethnic groups
- 3D surface plots expose the joint effect of parental education level and race/ethnicity on reading and writing scores
- Test preparation course completion shows a clear positive effect on scores across all subjects and demographic groups

**Modeling:**
- Scores binned into **Pass/Fail** (threshold: 60) and **letter grades** (F, D, C, B, A) using `pd.cut`
- Decision Tree classifiers + SMOTE oversampling trained separately per subject and per task
- Feature importances visualized as ranked bar charts per subject

### Key Result

| Subject | Pass/Fail Accuracy | Grade Accuracy |
| :--- | :---: | :---: |
| Math | 0.76 | 0.54 |
| Reading | 0.78 | ~0.55 |
| Writing | **0.79** | ~0.56 |

> Grade classification is substantially harder — the model performs best on extremes (A and F) and struggles most with middle grades (C/D), reflecting the continuous and overlapping nature of score distributions.

**Top predictive features (consistent across subjects):** `lunch` · `test preparation course` · `parental level of education`

---

## ⚙️ Core Techniques

- Multi-dimensional EDA — KDE plots, boxplots, 3D scatter plots, pairplots, pivot tables
- Categorical encoding — ordered `pd.Categorical` for proper ranking in visualizations
- Score discretization — `pd.cut` for binary Pass/Fail and 5-class letter grade targets
- Class imbalance handling — SMOTE oversampling per classification task
- Interpretable ML — Decision Tree feature importances as an analytical tool
- Cross-factor analysis — pivot tables and point plots for interaction effects between demographic variables

---
