# DA5401 Assignment 8: Ensemble Learning for Complex Regression — Bike Sharing Demand

## Student Information

* **Name:** Saggurthi Dinesh
* **Roll Number:** BE21B032
* **Email:** be21b032@smail.iitm.ac.in
* **Course:** DA5401 - Data Analytics Laboratory
* **Assignment:** 8

---

## Repository Structure

```bash
DA5401/A8/
├── DA5401_BE21B032_A8.ipynb    # Main Jupyter Notebook
└── README.md                   # This file
```

Dataset
Source
UCI Bike Sharing Demand Dataset (Hourly)

Samples: ~17,000 hourly observations

Target Variable: cnt (Total bike rentals per hour)

Key Features
Temporal: season, month, weekday, hour

Weather: temperature, humidity, windspeed, weathersit

Categorical Encoded: season, mnth, hr, weekday, weathersit

Preprocessing Steps
Dropped irrelevant columns (instant, casual, registered)

Sorted data chronologically by dteday and hr

One-hot encoded categorical variables

Applied an 80:20 time-based train-test split to preserve temporal integrity

 Objective
To implement and compare three ensemble learning techniques — Bagging, Boosting, and Stacking — for a complex regression task predicting hourly bike rentals.

The goal is to analyze how these ensembles manage the bias–variance trade-off and achieve improved accuracy over baseline single models.

Implementation Overview
Part A — Baseline Models
Decision Tree Regressor (max_depth=6)

Linear Regression (Standard Scaled)

The better-performing baseline model (based on RMSE) was selected for ensemble comparison.

Part B — Ensemble Techniques
1. Bagging Regressor (Variance Reduction)

Base learner: Decision Tree Regressor

Number of estimators: 50

Purpose: Reduce variance by averaging over bootstrap samples

RMSE: 155.52

Observation: Only minor improvement from a single tree — variance reduced, but bias remained high.

2. Gradient Boosting Regressor (Bias Reduction)

Concept: Sequential ensemble focusing on residual correction

Parameters: 300 estimators, learning_rate = 0.05, max_depth = 3

RMSE: 110.46

Observation: Significant improvement; reduced bias, better nonlinear fit.

Part C — Stacking for Optimal Performance
Base Learners (Level-0):

K-Nearest Neighbors Regressor

Bagging Regressor

Gradient Boosting Regressor

Meta-Learner (Level-1):

Ridge Regression (with scaling)

Concept: Stacking trains a meta-model to optimally combine predictions from diverse learners. Each base learner captures unique aspects of the data, while the Ridge model learns their optimal combination.

RMSE: 107.02 (Best Overall)

Observation: Demonstrates improved balance of bias and variance, leveraging complementary strengths.

Results & Analysis

Model_RMSE

Decision Tree (max_depth=6) - 158.69 

Linear Regression (scaled)-133.84

Bagging Regressor-155.52

Gradient Boosting Regressor-110.46

Stacking Regressor-107.02

Key Insights
Bagging stabilized predictions but didn’t capture new signals.

Boosting substantially improved accuracy through sequential learning.

Stacking outperformed all others, combining bias-reducing (boosting) and variance-reducing (bagging) effects.

Plot Interpretations
Bagging vs Actual: Wide spread → High bias, modest variance reduction

Linear Regression vs Actual: Smooth fi, but underestimates peaks

Gradient Boosting vs Actual: Tight clustering → reduced bias

Stacking vs Actual: Closest alignment with diagonal, minimal error

RMSE Comparison Bar Chart: Visual confirmation of stepwise improvement

Conclusion
This experiment demonstrates that model diversity and meta-learning yield superior regression performance.

While Bagging and Boosting each address one side of the bias–variance trade-off, Stacking effectively integrates both, leading to the lowest RMSE (107.02).
