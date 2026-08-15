# Project 5 — Vanguard A/B Test

## 📊 Project Overview

This project analyzes the results of an A/B test conducted for Vanguard to evaluate whether a redesigned digital customer experience improved the user journey and conversion rate.

The analysis compares two groups:

- **Control:** users who experienced the existing digital process.
- **Test:** users who experienced the redesigned digital process.

The main objective is to use data analysis and statistical hypothesis testing to determine whether the new experience produced a significant improvement in conversion.

---

## 🎯 Business Objective

The main business question is:

> **Does the redesigned digital experience improve the customer conversion rate compared with the existing experience?**

To answer this question, the project analyzes user journeys through the digital process and compares the performance of the Control and Test groups.

---

## 🔬 A/B Test

The experiment divides clients into two groups:

| Group | Description |
|---|---|
| **Control** | Existing digital experience |
| **Test** | Redesigned digital experience |

The customer journey consists of five main steps:

`Start → Step 1 → Step 2 → Step 3 → Confirm`

A successful conversion is defined as a client reaching the **`confirm`** step.

---

## 🗂️ Data

The project uses the following datasets:

### Experiment Clients

Contains information about clients participating in the A/B test.

Main columns:

- `client_id`
- `Variation`

The experiment dataset contains **70,609 clients**:

- **26,968 Test clients**
- **23,532 Control clients**
- **20,109 clients without a recorded Variation**

The 20,109 clients without a Variation were investigated separately and were not assigned artificially to either Test or Control.

### Web Data

The web interaction datasets contain:

- `client_id`
- `visitor_id`
- `visit_id`
- `process_step`
- `date_time`

The process steps are:

`start → step_1 → step_2 → step_3 → confirm`

The web datasets were combined and cleaned before the final analysis.

---

## 🧹 Data Cleaning & Preparation

The analysis included:

- Inspecting dataset shapes and columns
- Checking data types
- Identifying missing values
- Checking for duplicated records
- Checking unique clients
- Comparing client IDs across datasets
- Identifying clients with and without experiment assignments
- Sorting website interactions chronologically
- Grouping interactions by `visit_id`
- Reconstructing individual customer journeys
- Identifying incomplete journeys
- Identifying repeated process steps
- Identifying backward navigation
- Creating client-level conversion indicators

No artificial Test or Control assignments were made for clients with missing experimental variation.

The main identifier used to connect the datasets was:

`client_id`

---

## 🔗 Data Integration

The experiment data was merged with the web interaction data using `client_id`.

Only clients with a valid `Test` or `Control` assignment were included in the final A/B test comparison.

The final experiment population consisted of:

| Variation | Clients |
|---|---:|
| Control | 23,532 |
| Test | 26,968 |
| **Total** | **50,500** |

---

## 🔎 Customer Journey Analysis

Each customer's journey was reconstructed according to the sequence of process steps.

Expected journey:

`start → step_1 → step_2 → step_3 → confirm`

The analysis investigated:

- Completed visits
- Incomplete visits
- Funnel conversion
- Backward navigation
- Repeated steps
- Number of visits per client
- Most frequent visitors
- Common backward transitions

### Funnel Analysis

| Process Step | Unique Visits | Conversion from Start |
|---|---:|---:|
| Start | 25,601 | 100.00% |
| Step 1 | 20,668 | 80.73% |
| Step 2 | 17,832 | 69.65% |
| Step 3 | 16,222 | 63.36% |
| Confirm | 15,189 | 59.33% |

The largest drop-off occurs between:

`start → step_1`

The overall visit-level conversion from `start` to `confirm` was **59.33%**.

---

## 👤 Visits per Client

The analysis examined how frequently clients returned to the website.

Results:

- **Average visits per client:** 1.38
- **Median visits per client:** 1
- **Maximum visits by one client:** 21
- **Clients with one visit:** 14,865
- **Clients with multiple visits:** 5,244

This shows that most clients interacted with the website once, while approximately 26% returned for multiple visits.

---

## 🔁 Repeated Process Steps

Repeated process steps were treated as user behaviour rather than duplicate data because the dataset contained **no completely duplicated rows**.

Results:

- **Total visits:** 27,757
- **Visits with repeated steps:** 11,346
- **Percentage with repeated steps:** 40.88%

Most frequently repeated steps:

| Process Step | Visits with Repetition |
|---|---:|
| Start | 8,268 |
| Step 1 | 4,605 |
| Step 2 | 3,165 |
| Step 3 | 2,189 |
| Confirm | 1,376 |

The `start` step was the most frequently repeated step.

---

## ↩️ Backward Navigation

Backward navigation was also investigated.

Results:

- **Total visits:** 27,757
- **Visits with backward steps:** 6,573
- **Visits without backward steps:** 21,184
- **Visits with backward steps:** 23.68%
- **Visits without backward steps:** 76.32%

This indicates that approximately one quarter of visits contained at least one backward transition.

### Most Common Backward Transitions

| Transition | Frequency | Percentage |
|---|---:|---:|
| step_1 → start | 3,539 | 34.37% |
| step_3 → step_2 | 1,823 | 17.70% |
| step_2 → step_1 | 1,758 | 17.07% |
| step_3 → start | 1,322 | 12.84% |
| step_2 → start | 968 | 9.40% |
| step_3 → step_1 | 429 | 4.17% |
| confirm → start | 329 | 3.19% |
| confirm → step_1 | 69 | 0.67% |
| confirm → step_3 | 59 | 0.57% |
| confirm → step_2 | 2 | 0.02% |

The most common backward transition was:

`step_1 → start`

representing **34.37%** of all backward transitions.

---

## 📉 Backward Navigation and Completion

Visits were separated into two groups:

- Visits without backward navigation
- Visits with backward navigation

### Completion Results

| Visit Type | Visits | Completed | Completion Rate |
|---|---:|---:|---:|
| No backward steps | 21,184 | 12,093 | **57.09%** |
| Backward steps | 6,573 | 3,096 | **47.10%** |

Visits containing backward navigation had a completion rate approximately **9.99 percentage points lower** than visits without backward navigation.

This indicates an **association** between non-linear navigation and lower completion. It does not by itself prove that backward navigation causes users to abandon the process.

---

## 🔄 Conversion Definition

For the A/B test, conversion was calculated at the **client level**.

A client was classified as converted when their web activity contained the final:

`confirm`

process step.

This approach prevents clients with multiple visits or repeated web events from being counted multiple times.

---

## 📈 A/B Test Results

The final conversion results were:

| Variation | Clients | Conversions | Conversion Rate |
|---|---:|---:|---:|
| Control | 23,532 | 15,434 | **65.59%** |
| Test | 26,968 | 18,687 | **69.29%** |

The Test group achieved a higher conversion rate than the Control group.

### Absolute Improvement

`69.29% - 65.59% = +3.70 percentage points`

### Relative Improvement

The Test group achieved approximately a:

**+5.64% relative improvement**

in conversion compared with the Control group.

---

## 🧪 Statistical Hypothesis Testing

A **Two-Proportion Z-Test** was used to determine whether the difference between the Control and Test conversion rates was statistically significant.

### Null Hypothesis (H₀)

There is no significant difference in conversion rates between the Control and Test groups.

`H₀: p_test = p_control`

### Alternative Hypothesis (H₁)

There is a significant difference in conversion rates between the Control and Test groups.

`H₁: p_test ≠ p_control`

### Test Results

- **Z-statistic:** -8.8745
- **P-value:** < 0.001
- **Significance level:** 0.05

Since:

`p < 0.05`

the null hypothesis is rejected.

### Statistical Conclusion

The difference in conversion rates between the Test and Control groups is **statistically significant**.

The Test experience produced a significantly higher conversion rate than the Control experience.

---

## 💡 Key Findings

### 1. The Test experience performed better

The Test group achieved:

**69.29% conversion**

compared with:

**65.59% conversion**

for the Control group.

This represents:

- **+3.70 percentage points**
- **≈ +5.64% relative improvement**

### 2. The improvement is statistically significant

The Two-Proportion Z-Test produced:

**p < 0.001**

Therefore, the observed difference is statistically significant and unlikely to be explained by random variation alone.

### 3. The customer journey contains friction

The analysis identified:

- **23.68%** of visits containing backward navigation
- **40.88%** of visits containing repeated process steps
- **59.33%** visit-level conversion from `start` to `confirm`

These patterns suggest opportunities to reduce friction throughout the digital journey.

### 4. Backward navigation is associated with lower completion

Visits without backward navigation had a:

**57.09% completion rate**

while visits with backward navigation had:

**47.10% completion rate**

This represents an approximately **9.99 percentage-point difference**.

---

## 📊 Visualizations

The project includes visual analysis of:

- Customer funnel
- Conversion rates
- Test vs Control performance
- User journey behaviour
- Backward transitions
- Repeated process steps

The A/B test visualization compares:

- **Control: 65.59%**
- **Test: 69.29%**

## 📊 Visualizations

### A/B Test Conversion Rate

![Vanguard A/B Test Conversion Rate](images/vanguard_ab_test_conversion_rate.png)

### Customer Journey Funnel

![Vanguard Customer Journey Funnel](images/vanguard_customer_journey_funnel.png)
---

## 🛠️ Tools & Technologies

### Programming & Data Analysis

- Python
- Pandas
- NumPy

### Statistical Analysis

- Statsmodels
- Two-Proportion Z-Test
- Hypothesis testing
- Conversion rate analysis

### Data Visualization

- Matplotlib
- Seaborn

### Development Environment

- Jupyter Notebook
- Visual Studio Code

### Version Control

- Git
- GitHub

---

## 📚 Main Python Techniques

The project includes practical use of:

- `pandas.read_csv()`
- DataFrame filtering
- Boolean indexing
- `groupby()`
- `agg()`
- `apply()`
- `merge()`
- `isin()`
- `unique()`
- `nunique()`
- `value_counts()`
- `reset_index()`
- `sort_values()`
- Sets and set operations
- Proportion calculations
- Statistical hypothesis testing

---

## 🚀 Analytical Methodology

The project followed this workflow:

`Raw Data`

↓

`Data Inspection`

↓

`Data Cleaning`

↓

`Data Validation`

↓

`Dataset Integration`

↓

`Customer Journey Reconstruction`

↓

`Funnel Analysis`

↓

`User Behaviour Analysis`

↓

`A/B Test Analysis`

↓

`Conversion Rate Comparison`

↓

`Statistical Hypothesis Testing`

↓

`Business Conclusion`

---

## 📌 Business Interpretation

The results suggest that the redesigned digital experience has a positive impact on the likelihood that clients complete the online process.

The Test experience increased conversion from:

**65.59% → 69.29%**

This represents:

**+3.70 percentage points**

and approximately:

**+5.64% relative improvement**

The statistical test confirms that the difference is highly significant.

From a business perspective, the Test experience could potentially:

- Increase digital conversion
- Improve completion of the online customer journey
- Reduce customer drop-off
- Improve the efficiency of the digital onboarding process
- Increase the number of clients reaching the final confirmation stage

However, statistical significance should be considered together with business significance. The practical and financial impact of the improvement should also be evaluated before full implementation.

---

## 🏁 Final Conclusion

The A/B test provides strong evidence that the **Test experience performs better than the Control experience**.

The Test group achieved a **69.29% conversion rate**, compared with **65.59% for the Control group**.

This represents a:

**+3.70 percentage-point improvement**

and approximately:

**+5.64% relative improvement**.

The Two-Proportion Z-Test produced:

**Z = -8.8745**

with:

**p < 0.001**

Therefore, the difference is statistically significant.

### Final Recommendation

Based on the results of this analysis, the **Test experience should be considered for implementation**, subject to further business validation of the practical and financial impact of the conversion improvement.

The user journey analysis also indicates that there are opportunities to further improve the digital experience by reducing repeated actions, backward navigation, and early-stage drop-off.

---

## 👩‍💻 Author

**Teresa Mendes Coelho**

Data Analytics Bootcamp — Ironhack
