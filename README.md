# Advanced Intrusion Detection System
## A Unified Approach Using Supervised and Unsupervised Learning

**Author:** Amal Shaji  
**Institution:** Middlesex University London  
**Department:** Computer Science  
**Degree:** MSc Cybersecurity and Penetration Testing  
**Supervisor:** Dr. A.R. Lasebae  
**Year:** 2023  

---

## Overview

This research addresses a critical gap in modern
intrusion detection by developing a two-phase
hybrid IDS framework that combines supervised
ensemble learning with unsupervised clustering
to detect both known and unknown network threats.

Traditional signature-based IDS cannot detect
zero-day attacks. This research proposes an
anomaly-based approach using machine learning
to proactively identify threats that have no
prior signature — bridging the gap between
known attack detection and emerging threat
resilience.

---

## Research Objectives

- Train and evaluate multiple supervised ML
  models for known intrusion detection
- Optimise selected models through
  hyperparameter tuning using Grid Search
  cross-validation
- Construct an ensemble model combining the
  highest performing classifiers using a
  Voting Classifier
- Integrate an unsupervised K-Means model
  to cluster and detect previously unknown
  attacks
- Evaluate framework viability in real-world
  network security contexts

---

## Datasets

| Dataset | Phase | Description |
|---------|-------|-------------|
| CICIDS2017 | Phase 1 | Supervised training and evaluation — approximately 2.8 million network flows across 22 attack categories simulated in a realistic environment |
| CICDDoS2019 | Phase 2 | Unsupervised clustering — labels removed to simulate zero-day attack detection scenario |

> Datasets are not included in this repository
> due to file size. Both datasets are publicly
> available from the Canadian Institute for
> Cybersecurity.

---

## Methodology

### Phase 1 — Supervised Learning

**Data Preprocessing**

The CICIDS2017 dataset was cleaned and prepared 
through the following steps:

- Removed zero values and duplicate columns
  to reduce variance and prevent overfitting
- Eliminated statistical summary columns, including min, max, mean, and standard
  deviation, as they introduced noise without
  adding discriminative value
- Applied four feature selection methods to
  identify the most informative features for
  intrusion detection

**Feature Selection**

Four complementary feature selection methods 
were applied and their results combined:

| Method | Approach |
|--------|---------|
| Random Forest | Gini impurity-based feature importance ranking |
| Lasso Regression | L1 regularisation shrinking insignificant coefficients to zero |
| Univariate ANOVA | Statistical significance of each feature relative to the target variable |
| Correlation Matrix | Pearson correlation to identify and remove multicollinear features |

12 features were eliminated through this process, producing a cleaner and more 
computationally efficient dataset for
model training.

**Supervised Model Evaluation**

Five models were evaluated using default 
parameters on a 70/30 train-test split:

| Model | Precision | Recall | F1 Score |
|-------|-----------|--------|---------|
| XGBoost | 0.99 | 0.95 | 0.97 |
| Decision Tree | 0.96 | 0.97 | 0.97 |
| Random Forest | 0.97 | 0.93 | 0.95 |
| SVM | 0.83 | 0.82 | 0.82 |
| Logistic Regression | 0.16 | 0.14 | 0.15 |

XGBoost, Decision Tree, and Random Forest 
were selected as the top performers.
Logistic Regression and SVM were eliminated 
due to poor performance on this dataset.

**Hyperparameter Optimisation**

Grid Search cross-validation was applied 
to Random Forest and Decision Tree to
fine-tune their parameters:

- Random Forest: n_estimators, max_features
- Decision Tree: criterion, splitter

XGBoost was not subjected to optimisation 
due to its built-in regularisation 
capabilities that inherently reduce 
overfitting risk.

**Ensemble Model**

A Voting Classifier combining the three 
optimised models was evaluated using both 
hard and soft voting strategies:

| Ensemble | Precision | Recall | F1 Score |
|----------|-----------|--------|---------|
| Hard Voting | 0.99 | 0.96 | 0.97 |
| Soft Voting | 0.99 | 0.95 | 0.97 |

Hard voting was selected as the final 
ensemble. Its consensus-driven approach, 
requiring unanimous agreement across all 
three models, significantly reduces false 
positives and enhances resilience against 
unknown attack patterns.

---

### Phase 2 — Unsupervised Learning

K-Means clustering was applied to the 
unlabelled CICDDoS2019 dataset to simulate
zero-day attack detection. The implementation 
combined:

- PCA dimensionality reduction to address
  the computational complexity of the
  high-dimensional dataset;
- K-Means++ initialisation for improved
  cluster convergence and stability;
- Elbow curve method for optimal K
  identification

Computational constraints during the 
research period prevented full integration 
of both phases into a single unified 
framework. However, the supervised ensemble 
and unsupervised clustering components 
individually demonstrated strong performance, 
validating the viability of the combined 
approach.

---

## Key Results

- Hard voting ensemble achieved **99%
  precision** across 22 attack categories
  on the CICIDS2017 dataset
- XGBoost demonstrated the strongest
  individual model performance at 0.99
  precision
- Four-method feature selection reduced
  dataset dimensionality without compromising
  detection accuracy
- K-Means clustering validated the
  potential for unknown attack identification
  through unsupervised anomaly detection

---

## Technologies

| Technology | Purpose |
|-----------|---------|
| Python | Primary implementation language |
| scikit-learn | ML model training and evaluation |
| XGBoost | Gradient boosting classifier |
| pandas | Data manipulation and preprocessing |
| NumPy | Numerical computation |
| matplotlib / seaborn | Results visualisation |
| PCA | Dimensionality reduction |
| K-Means++ | Unsupervised clustering |

---

## Repository Structure

```
msc-ids-dissertation/
├── README.md
├── ids_research.py
└── results/
    ├── hard_voting_classification_report.png
    ├── soft_voting_classification_report.png
    ├── feature_importance_rf.png
    ├── feature_importance_lasso.png
    ├── feature_importance_univariate.png
    └── correlation_matrix.png
```

---

## Limitations and Future Work

Full integration of the supervised and 
unsupervised phases was constrained by the 
computational resources available during 
the research period. Future work should 
explore distributed computing to address 
this limitation and investigate real-time
model retraining through transfer learning 
from unsupervised clustering outputs to 
continuously improve detection of emerging 
threats.

---

## Citation

```
Shaji, A. (2023). Advanced Intrusion Detection
System: A Unified Approach Using Supervised
and Unsupervised Learning. MSc Dissertation,
Middlesex University London, Faculty of
Science and Technology.
```
