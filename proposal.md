# CSC172 Association Rule Mining Project Proposal

**Student:** John Robert M. Mamauag, 2021-1415
**Date:** 1/5/2026  

---

## 1. Project Title

**Powerlifting Performance & Equipment Analysis**

---

## 1.5 Brief Intro to Powerlifting

Powerlifting is a strength sport where athletes compete to lift the heaviest weights in three exercises: squat, bench press, and deadlift. Competitors are grouped by weight class, age, and sometimes equipment use. The goal is to maximize the total weight lifted across all three lifts.

---

## 2. Problem Statement

Powerlifting coaches and enthusiasts want to identify patterns between athletes’ characteristics, equipment use, and performance outcomes. This project analyzes the Open Powerlifting Database to discover frequent associations between variables such as weight class, age group, equipment (e.g., knee sleeves, suits), and lift type success. Findings can help optimize training recommendations, competition preparation, and personalized coaching strategies.

---

## 3. Objectives

- Preprocess powerlifting competition data and perform exploratory data analysis (EDA) with visualizations  
- Implement **FP-Growth algorithm** to generate association rules linking athlete attributes, equipment, and performance outcomes  
- Evaluate rules using support, confidence, lift, and conviction metrics  
- Identify actionable insights for coaches and athletes  
- Optionally explore predictive insights using decision trees or other classification algorithms  

---

## 4. Dataset Plan

- **Source:** Open Powerlifting Database – Kaggle (~100K+ competition records)  
- **Domain:** Powerlifting competition results  
- **Acquisition:** Direct Kaggle download to `data/openpowerlifting.csv`  
- **Relevant Features:**  
  - `sex`  
  - `weight_class_kg`  
  - `age_class`  
  - `equipment`  
  - `best3squat_kg`  
  - `best3bench_kg`  
  - `best3deadlift_kg`  
  - `total_kg`  

---

## 5. Technical Approach

**Preprocessing:**  

- Filter for valid records (non-null lift results)  
- Categorize continuous variables like total weight lifted, age, and weight class into bins  
- One-hot encode categorical variables using `mlxtend` TransactionEncoder  

**Algorithm:**  

- **Primary:** FP-Growth  
  - Efficiently finds frequent itemsets without generating all candidate combinations  
  - Supports longer itemsets, allowing discovery of more detailed associations  
- **Optional Predictive Analysis:** Decision Tree or Random Forest for performance classification  

**Framework:** Python + pandas + mlxtend + matplotlib/seaborn  

**Environment:** Jupyter Notebook / VSCode

---

## 6. Expected Challenges & Mitigations

- **Challenge:** Highly diverse and sparse dataset (many unique athletes, weight classes, and equipment types)  
  - **Solution:** Filter infrequent items (support > 0.01)  

- **Challenge:** Long runtime for mining frequent patterns with many attributes  
  - **Solution:** Use FP-Growth for memory- and time-efficient pattern discovery  

- **Challenge:** Trivial or obvious rules (e.g., male lifters lift more than female lifters)  
  - **Solution:** Filter rules by lift/conviction thresholds to focus on actionable insights 