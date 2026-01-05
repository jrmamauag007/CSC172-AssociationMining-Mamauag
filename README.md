# Powerlifting Performance & Equipment Analysis

**CSC172 Data Mining and Analysis – Final Project**

Mindanao State University – Iligan Institute of Technology

**Student:** John Robert M. Mamauag (2021-1415)

**Semester:** AY 2025–2026, Semester 1

---

## Abstract

Powerlifting is a strength sport where athletes compete to lift the heaviest weights in three exercises: squat, bench press, and deadlift. Competitors are grouped by weight class, age, and sometimes equipment use.

This project applies **association rule mining using the FP-Growth algorithm** to the **Open Powerlifting Database** to discover meaningful relationships between athlete demographics, equipment usage, weight classes, and performance outcomes. The analysis focuses on **2019 competition data** to reduce computational complexity while maintaining relevance. Key findings show strong associations between age group (24–34), weight class, sex, equipment choice (Raw vs Single-ply), and high performance as measured by **IPF Points**. The workflow includes data preprocessing, exploratory data analysis (EDA), frequent pattern mining, rule evaluation using support, confidence, and lift, and visualization of results.

---

## Table of Contents

1. Introduction
2. Dataset Description
3. Methodology
4. Results
5. Discussion
6. Conclusion
7. References
8. Appendix: Code Summary

---

## 1. Introduction

### 1.1 Problem Statement

Powerlifting coaches and athletes seek to understand how demographic factors (age, sex, weight class) and equipment choices relate to competitive performance. Given the size and complexity of competition data, identifying consistent patterns manually is difficult. This project aims to uncover **frequent and statistically strong associations** that can support training and competition strategy decisions.

### 1.2 Objectives

* Preprocess powerlifting competition data for association rule mining
* Filter and reduce a large-scale dataset to a manageable and relevant subset
* Apply FP-Growth to generate frequent itemsets and association rules
* Evaluate rules using support, confidence, and lift
* Visualize and interpret meaningful performance-related patterns

### 1.3 Scope and Limitations

**Scope:**

* Analysis limited to **2019 competition data** from the Open Powerlifting Database
* Focus on categorical attributes and derived performance labels

**Limitations:**

* No longitudinal (year-to-year) performance trends
* Missing values in some attributes (e.g., AgeClass)
* Binary representation of attributes (presence/absence only)

---

## 2. Dataset Description

### 2.1 Source and Acquisition

* **Source:** Open Powerlifting Database (Kaggle)
* **Original Size:** ~800,000+ rows
* **Filtered Size (2019):** ~70,000 competition entries
* **Format:** CSV

### 2.2 Data Structure

Each row represents a single competition entry with attributes including:

* Sex
* AgeClass
* WeightClassKg
* Equipment
* TotalKg
* IPFPoints
* Date of competition

### 2.3 Sample Attributes Used for Mining

* Sex (M, F)
* AgeClass (e.g., 20–23, 24–34)
* Weight class (binned: <60, 60–75, 75–90, 90–105, 105–120, 120+)
* Equipment (Raw, Wraps, Single-ply)
* HighPerformance (derived from IPFPoints threshold)

---

## 3. Methodology

### 3.1 Data Preprocessing

* Converted `Date` column to datetime format
* Filtered dataset to **year 2019** to reduce size and runtime
* Removed rows with missing critical values (WeightClassKg, IPFPoints)
* Converted numeric columns using safe type casting
* Binned weight classes into standard competition categories
* Derived **HighPerformance** label from IPFPoints
* One-hot encoded categorical attributes for transaction format

**Final Transaction Matrix:**

* ~70,987 transactions × 29 binary attributes

---

### 3.2 Exploratory Data Analysis (EDA)

* Majority of lifters fall within the **24–34 age class**
* Raw equipment dominates lighter and middle weight classes
* Single-ply equipment is concentrated in heavier male lifters

---

### 3.3 FP-Growth Algorithm Implementation

* Library: `mlxtend.frequent_patterns`
* Algorithm: `fpgrowth()`
* Parameters:

  * Minimum support: 0.02
  * Maximum itemset length: 3
* Rule generation: `association_rules()`

FP-Growth was selected over Apriori due to better performance on large and sparse datasets.


## 4. Results

### 4.1 Top Association Rules (2019)

Examples of strong rules discovered:

* (24–34, 90–105) → (Male, Raw)

  * Confidence ≈ 78%, Lift ≈ 3.9
* (90–105, HighPerformance) → (Male, Raw)

  * Confidence ≈ 71%, Lift ≈ 3.6
* (24–34, Male) → HighPerformance

  * Confidence ≈ 74%, Lift ≈ 2.7

These rules indicate strong links between age, weight class, sex, equipment choice, and elite performance.

---

### 4.2 Key Visualizations
https://drive.google.com/file/d/16Tw5vp0OsC-FPYgtkR5J-QsiqVmeRVIo/view?usp=sharing
* Scatter plot of **Support vs Confidence**, bubble size representing Lift
* Visualization shows most strong rules have:

  * Low support but high confidence
  * Lift values well above 1, indicating non-random associations

---

### 4.3 Performance Metrics

* One-hot encoded matrix: (70,987 × 29)
* Frequent itemsets discovered: 116
* Runtime suitable for execution on a standard local machine (no cloud computing)

---

## 5. Discussion

### 5.1 Insights

* Lifters aged **24–34** consistently dominate high-performance rules
* Raw equipment is strongly associated with high performance in lighter and mid-weight classes
* Single-ply equipment is prevalent among superheavy male lifters

### 5.2 Actionable Implications

* Coaches can tailor equipment and training strategies by age and weight class
* Athletes can benchmark performance expectations within their demographic group
* Analysts can use IPFPoints-based rules to identify elite performance profiles

### 5.3 Challenges and Mitigations

* **Highly sparse and diverse dataset**
  → Filtered infrequent items (support > 0.01)
* **Very large dataset (~800k rows)**
  → Reduced to 2019 data for efficiency and relevance

---

## 6. Conclusion

This project demonstrates that **association rule mining using FP-Growth** can effectively uncover meaningful patterns in competitive powerlifting data. Strong associations were found between age, sex, weight class, equipment choice, and high performance. The results provide valuable insights for coaching, athlete development, and sports analytics, while also showcasing the applicability of data mining techniques to real-world sports datasets.

---

## 7. Video Presentation

https://drive.google.com/file/d/1IIzErHiVddpuwTGoCMS4lXEDbLTg9Sgk/view?usp=sharing

---

## 8. References

* Open Powerlifting Database – Kaggle
* `mlxtend` documentation

---

## 9. Appendix: Code Summary

* Data loading and filtering by year
* Data cleaning and feature selection
* Weight class binning
* Transaction encoding (one-hot)
* FP-Growth frequent itemset mining
* Association rule generation and visualization
