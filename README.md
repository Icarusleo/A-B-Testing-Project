# A-B-Testing-Project
# 🎮 Mobile Game A/B Testing: Bootstrapping Analysis

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Library-Pandas-orange)
![Statistics](https://img.shields.io/badge/Method-Bootstrapping-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 Project Overview
This project analyzes the results of an A/B test performed on the mobile puzzle game **Cookie Cats**. The goal is to determine whether moving the "forced break" (gate) from **Level 30** to **Level 40** affects player retention.

Instead of relying on standard parametric tests (like t-tests) which assume normal distribution, this project utilizes **Bootstrapping (Resampling)** to generate accurate Confidence Intervals for retention metrics.

---

## 🧪 The Hypothesis & Data
* **Control Group (Gate 30):** Players encounter a forced wait at Level 30.
* **Test Group (Gate 40):** Players encounter a forced wait at Level 40.
* **Metric:** 1-Day Retention (Did the player come back 1 day after installation?)

### Why Bootstrapping?
Retention data is binary (0 or 1) and creates a Bernoulli distribution. At large sample sizes, the Central Limit Theorem helps, but Bootstrapping allows us to:
1.  Visualize the uncertainty distribution.
2.  Calculate exact Confidence Intervals without normality assumptions.
3.  Directly calculate the probability of one group being better than the other.

---

## 💻 Technical Implementation
The core analysis involves simulating the experiment **1,000 to 10,000 times** using Python.

### Key Code Logic (Bootstrapping)
```python
# Resampling the dataset with replacement
boot_mean = df.sample(frac=1, replace=True).groupby('version')['retention_1'].mean()

# Calculating the % difference (Lift)
boot_1d['diff'] = (boot_1d['gate_30'] - boot_1d['gate_40']) / boot_1d['gate_40'] * 100
