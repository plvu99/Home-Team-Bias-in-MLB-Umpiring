# ️Home-Team Bias in MLB Umpiring

## 🔎 Overview

This project investigates **whether Major League Baseball (MLB) umpires exhibit systematic home-team bias and how such bias may influence game outcomes.** Using umpire scorecard data from the 2015–2022 MLB seasons, the analysis combines statistical modeling and clustering techniques to examine patterns in missed calls and their impact on run expectancy.

The study applies both **supervised learning** (regression and classification) and **unsupervised learning **(clustering) to understand whether umpire behavior consistently favors home teams and to identify groups of umpires with similar decision-making patterns.

## 🔐 Business Problem

Umpires play a critical role in baseball, and their calls directly influence game fairness and outcomes. Even top-performing MLB umpires miss approximately 12–13 calls per game, and incorrect calls can significantly affect run expectancy.

However, an important question remains: _Do umpires systematically favor the home team?_

Understanding this issue matters because:
- Umpire bias may affect competitive fairness
- It can influence fan perception and trust in officiating
- Teams may adjust strategies depending on home vs away disadvantages
- Leagues may use analytics to improve umpire training and evaluation systems

This project aims to quantify the existence and magnitude of home-team bias in MLB umpiring decisions.

## 📊 Dataset

The dataset was sourced from Umpire Scorecards via [Kaggle](https://www.kaggle.com/datasets/mattop/mlb-baseball-umpire-scorecards-2015-2022) and includes game-level umpire performance data for MLB games between 2015 and 2022.

Each record represents one MLB game and includes information such as:
- Umpire ID
- Home and away teams
- Number of incorrect calls
- Umpire accuracy
- Umpire consistency
- Favorability toward the home team
- Run expectancy impact of incorrect calls

Key variables analyzed include:
- **favor_home:** Difference between the home team’s and away team’s run expectancy impact.
- **total_run_impact:** Total change in run expectancy caused by missed calls.

Dataset size: 18,000+ MLB games, 18 features

## 📍 Methodology

The analysis applied both supervised and unsupervised learning methods.

### Data Preprocessing
- Removed rows with missing values
- Converted key variables to numeric format
- Selected relevant features for modeling
- Standardized variables used in clustering

### Regression Analysis

Two regression models examined whether incorrect calls systematically favor the home team.

**Simple Linear Regression**

Modeled relationship between `incorrect_calls` and:
- `favor_home`
- `total_run_impact`

**Multiple Linear Regression**

Added additional predictors: accuracy, interaction terms, performance indicators

Evaluation metrics: R² (goodness of fit), RMSE, train/test validation, 5-fold cross-validation

### Classification Models

Two classification models were used to predict whether an umpire's calls favor the home team.

**Logistic Regression**

Classifies games based on whether run impact exceeds the median.

**Decision Tree**

Captures nonlinear relationships using features such as umpire ID, home team, away team, incorrect calls

Model performance evaluated using accuracy, confusion matrix, cross-validation scores

### Clustering Analysis

Two clustering techniques were applied to identify groups of umpires based on bias patterns.

**K-Means Clustering**

Grouped umpires based on:
- `favor_home`
- `total_run_impact`

Cluster selection used:
- Elbow method
- Silhouette score

**Hierarchical Clustering**

Included additional variables: accuracy, consistency, run impact

Cluster structures were analyzed using:
- Dendrograms
- Merge height analysis

<img width="853" height="556" alt="image" src="https://github.com/user-attachments/assets/a8ff98c4-e388-47b6-b214-671d47927a87" />

<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/57d34803-79fe-44f8-b7ff-e668ac36883b" />

## 🔑 Key Insights

### Regression Results

The regression models showed almost no relationship between incorrect calls and home-team favorability.

Even when additional predictors were added, the model’s explanatory power remained extremely low (R² ≈ 0).

This suggests that missed calls alone do not systematically favor the home team.

However, umpire accuracy was significantly associated with run impact. When highly accurate umpires make incorrect calls, those calls tend to have larger impacts on run expectancy.

<img width="833" height="547" alt="image" src="https://github.com/user-attachments/assets/89d89e5e-cca2-4d29-af85-efd35fe7efca" />

<img width="833" height="547" alt="image" src="https://github.com/user-attachments/assets/a0691407-43d8-49a7-a6d6-60bb990e727a" />

### Classification Results

Classification models performed poorly, with prediction accuracy around 51%, which is roughly equivalent to random guessing.

This indicates that incorrect call counts alone cannot reliably predict home-team bias.

One reason is that most combinations of umpire, home team, and away team occur only once, limiting patterns that machine learning models can learn.

<img width="1570" height="790" alt="image" src="https://github.com/user-attachments/assets/dff3fb3d-07ef-4f56-84b6-e3f654bc5dd0" />

### K-Means Clustering

Three clusters of umpire behavior emerged:

**Neutral Umpires (58%)**
- Favorability scores close to zero
- Minimal bias toward either team

**Away-Team Bias (20%)**
- Negative favor_home values
- Calls tend to benefit the visiting team

**Home-Team Bias (22%)**
- Positive favor_home values
- Calls more frequently benefit the home team

Most umpires appear neutral, but a meaningful minority show systematic bias.

<img width="713" height="470" alt="image" src="https://github.com/user-attachments/assets/a5c2ba77-ff1d-44f6-9479-14c4033c660e" />

### Hierarchical Clustering

Three performance-based clusters were identified:

<img width="519" height="171" alt="Screenshot 2026-03-08 at 4 38 53 AM" src="https://github.com/user-attachments/assets/7cab377d-5680-4e34-a88e-55d555e337ed" />

**Cluster 1 – High Accuracy Neutral Umpires**
- Highest accuracy and consistency
- Low run impact
- Minimal bias

**Cluster 2 – Slight Away Bias**
- Moderate accuracy
- Slight preference toward away teams

**Cluster 3 – Home Bias Umpires**
- Lowest accuracy
- Highest run impact
- Stronger home-team favorability

These clusters reveal measurable differences in umpire performance and bias patterns.

## ✍️ Business Recommendations

### 1. Improve Umpire Performance Monitoring

Leagues could monitor umpires based on bias and performance metrics to detect potential patterns that affect fairness.

### 2. Assign High-Accuracy Umpires to High-Stake Games

Umpires with strong accuracy and neutrality metrics may be better suited for playoff games or high-impact matchups.

### 3. Use Data-Driven Umpire Training

Umpires showing higher bias or lower accuracy may benefit from targeted retraining programs.

### 4. Expand Use of Technology

Technologies such as automated strike zones could help reduce the influence of human bias in critical calls.

Improve Future Data Collection

Future studies should include which team was batting, types of incorrect calls, or pitch location information.

This would allow deeper analysis of situational bias.

## ⚙ Tools & Technologies

- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Machine Learning (Linear Regression, Logistic Regression, Decision Trees)
- Clustering (K-Means, Hierarchical Clustering)
- Model Evaluation (Cross-validation, RMSE, R², Silhouette Score)
