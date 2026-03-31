# construction-cost-estimation

# 🏗️ Construction Cost Estimation (Solafune Competition)

## 📌 Overview

This project was developed for the **Solafune Machine Learning Competition**, where the goal was to predict **construction cost per square meter (USD)** using economic and geographic data.

* 📊 Problem Type: Regression
* 📍 Countries: Japan & Philippines
* 📅 Time Range: 2019 – 2024
* 📏 Metric: RMSLE (Root Mean Squared Logarithmic Error)
* 🏆 Final Rank: **77th place**

📄 Detailed report: 

---

## 🎯 Objective

Build a model that accurately predicts construction costs across different regions, handling large variations in price scales between countries.

---

## 📂 Dataset

* 1,024 training samples
* 1,024 evaluation samples
* 23 total columns
* Includes:

  * Economic indicators (GDP, CPI)
  * Geographic features
  * Risk classifications
  * Satellite image references (not used)

---

## ⚙️ Approach

### ✔️ Key Decisions

* Ignored satellite imagery (17GB) → focused only on tabular data
* Applied **log transformation** to target (critical for RMSLE)
* Used **simple but strong baseline models**

---

## 🔧 Features Used

Main features include:

* Country
* Geolocation
* GDP (deflated)
* CPI
* Climate & risk indicators
* Infrastructure access
* Distance to capital

⚠️ Reality check:

> "country" alone explains ~90% of predictions — meaning your model is **mostly just separating Japan vs Philippines**, not deeply learning patterns.

---

## 🤖 Models

### 1. XGBoost

* n_estimators: 1000
* learning_rate: 0.05
* max_depth: 6

### 2. LightGBM

* Same configuration as XGBoost

### 🔀 Ensemble

* Final output = **50% XGBoost + 50% LightGBM**

---

## 📊 Results

| Model     | OOF RMSLE  |
| --------- | ---------- |
| XGBoost   | 0.2026     |
| LightGBM  | 0.2018     |
| **Blend** | **0.2002** |

* 📈 Final Score: **0.2002 RMSLE**
* 🏆 Leaderboard Rank: **77**

---

## 📉 Key Insights

### What Actually Worked

* Log transformation → non-negotiable for RMSLE
* Ensembling → consistent improvement
* Cross-validation → reliable results

### What Didn’t (or was weak)

* No feature engineering
* No hyperparameter tuning
* No satellite data (this is the biggest miss)

---

## 🚫 Limitations (Don’t Ignore This)

* Model is **over-reliant on country feature**
* Poor within-country prediction capability
* No generalization to new regions
* Basically a **strong baseline, not a competitive final solution**

---

## 🚀 Improvements (If You Want to Actually Compete)

### High Impact

* Use **Sentinel-2 & VIIRS data**
* Extract band statistics (mean, std, etc.)

### Medium Impact

* Feature engineering (GDP × distance, temporal trends)

### Low Impact

* Hyperparameter tuning
* Add CatBoost

---

## 🛠️ Tech Stack

* Python
* pandas, numpy
* scikit-learn
* XGBoost
* LightGBM

---

## 📁 Repository Structure

```
├── solafune-ml.ipynb   # Main notebook
├── submission.csv      # Final predictions
├── README.md           # Project documentation
```

---



