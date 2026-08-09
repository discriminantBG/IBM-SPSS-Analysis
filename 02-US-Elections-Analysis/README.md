# 📊 Statistical Analysis of 2020 US Presidential Election Data (IBM SPSS)

## 📌 Project Overview
This project provides an Exploratory Data Analysis (EDA) and rigorous statistical hypothesis testing on the 2020 US Presidential Election dataset using **IBM SPSS Statistics**. 

The main objectives are:
1. Evaluating the distribution and normality of county-level vote totals.
2. Comparing average voting patterns between major political parties.
3. Testing categorical dependency between candidate party affiliation and county-level victories.
4. Analyzing state-level geographical variations in vote distributions using non-parametric methods.

---

## 📁 Repository Structure

```text
US-Elections-SPSS-Analysis/
│
├── data/
│   ├── president_county_candidate.csv      # Raw election dataset (CSV format)
│   └── spss_usa_elec.sav                   # Processed SPSS Data file (.sav)
│
├── outputs/                                # SPSS exported outputs, plots and viewer file
│   ├── spss_usa_elec.spv                   # Complete SPSS Output Viewer file (.spv)
│   ├── normality_test.png                  # Shapiro-Wilk / Kolmogorov-Smirnov
│   ├── t_test_results.png                  # Independent Samples T-Test
│   ├── crosstabs_chi_square.png            # Chi-Square Test & Cramer's V
│   ├── kruskal_wallis_summary.png          # Non-parametric ANOVA summary
│   └── pairwise_comparisons.png            # Post-hoc pairwise state tests
│
└── README.md                               # Project documentation
````
---

## 📊 Dataset Specifications
* **Source:** Kaggle — US Election 2020 Dataset (`president_county_candidate.csv`)
* **Scope:** N = 32,177 records across US counties and states.
* **Key Variables:**
  * `state` (Nominal / String): US State.
  * `party` (Nominal / Categorical): Political party (`DEM`, `REP`, `LIB`, `GRN`, etc.).
  * `total_votes` (Scale / Continuous): Total votes received by a candidate in a given county.
  * `won` (Binary / Nominal): County victory status (`True` / `False`).

---

## 🔬 Methodology & Hypothesis Testing

### 1. Test of Normality (Exploratory Data Analysis)
* **Objective:** Assess whether the dependent variable `total_votes` follows a normal distribution.
* **Test Used:** Kolmogorov-Smirnov Test (with Lilliefors Significance Correction).
* **Statistical Result:** D(32177) = 0.445, p < 0.001.
* **Conclusion:** The assumption of normality is strongly violated (p < 0.05). The distribution displays heavy positive skewness (Skewness = 32.034), driven by a vast number of small rural counties alongside a few extremely high-density metropolitan areas (e.g., Los Angeles County).

---

### 2. Two-Group Mean Comparison (Independent Samples T-Test)
* **Objective:** Determine if there is a statistically significant difference in mean county votes between the Democratic (`DEM`) and Republican (`REP`) parties.
* **Assumptions Check (Levene's Test):** F = 21.642, p < 0.001. Equality of variances is rejected (p < 0.05), requiring the interpretation of Welch's t-test (`Equal variances not assumed`).
* **Group Means:**
  * Democratic Party: Mean = 17,709.14 (SD = 80,206.44, SE = 1178.36)
  * Republican Party: Mean = 16,098.79 (SD = 45,531.31, SE = 668.93)
* **Test Result:** t(7336.52) = 1.188, p = 0.235.
* **Confidence Interval & Effect Size:**
  * 95% CI of Difference = [-1045.82, 4266.51]
  * Cohen's d = 0.025 (negligible effect size).
* **Conclusion:** We fail to reject the null hypothesis (p >= 0.05). The average vote difference of 1,610.35 votes per county between the two major parties is **not statistically significant**. The drastically higher standard deviation in Democratic votes highlights greater population variance in Democratic-leaning counties.

---

### 3. Categorical Association Analysis (Chi-Square Test of Independence)
* **Objective:** Evaluate whether winning a county (`won`) is statistically dependent on political party affiliation (`party`).
* **Test Used:** Pearson Chi-Square (Chi^2) via Crosstabulation.
* **Assumption Check:** Only 1.9% of cells have expected counts < 5 (below the maximum 20% threshold), confirming test validity.
* **Statistical Results:**
  * Pearson Chi^2(25) = 16215.35, p < 0.001.
  * Cramer's V = 0.710, p < 0.001.
* **Conclusion:** The null hypothesis is rejected (p < 0.05). There is an extremely strong and statistically significant relationship (V = 0.710) between political party alignment and county-level victory.

---

### 4. Multi-Group Non-Parametric Comparison (Kruskal-Wallis H Test)
* **Objective:** Compare county vote distributions across all 50 states without assuming normality.
* **Test Used:** Independent-Samples Kruskal-Wallis Test with Post-hoc Pairwise Comparisons (Bonferroni correction).
* **Statistical Result:** H(50) = 10998.99, p < 0.001.
* **Post-hoc Insights:**
  * Significant differences (p_adj < 0.001) exist between high-density and low-density states (e.g., Vermont vs. Colorado).
  * Non-significant differences (p_adj = 1.000) were observed between states with similar county structures (e.g., Louisiana vs. Iowa).
* **Conclusion:** Geographical location (state) exerts a highly significant effect on county vote distributions.

---

## 🛠️ Key Takeaways & Methodology Summary

1. **Robustness over Parametrics:** Due to extreme skewness in population data, non-parametric alternatives (such as Kruskal-Wallis H) provide more reliable inferences when comparing multi-group geographic distributions.
2. **Variance Analysis:** While overall mean party votes per county do not differ significantly, variance analysis reveals distinct urban-rural clustering patterns between parties.

---

## ⚙️ Software & Tools
* **IBM SPSS Statistics v28+** (Explore, Compare Means, Crosstabs, Non-parametric Tests)
* **Markdown** (Documentation)
