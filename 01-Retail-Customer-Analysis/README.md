# SPSS Retail Customer Behavior & Hypothesis Testing

## Overview
This repository contains a statistical analysis of retail customer behavior based on the **Customer Shopping Trends Dataset** ($N = 3900$). The research is conducted using **IBM SPSS Statistics** to evaluate key business hypotheses regarding the impact of loyalty subscriptions, discounts, customer satisfaction, and payment options.

---

## Dataset Summary
* **Total Records:** 3,900 transactions
* **Variables Used in Task 1:**
  * `Purchase Amount (USD)` — Dependent Variable (Scale / Quantitative)
  * `Subscription Status` — Independent Variable (Nominal / Binary: *Yes* / *No*)

---

## Statistical Hypothesis Testing

### Task 1: Impact of Subscription Program on Basket Size

#### 1. Business Question & Context
Does a loyalty subscription (`Subscription Status`: *Yes*) lead to a higher average single-purchase order value (`Purchase Amount USD`) compared to non-subscribers (*No*)?

#### 2. Hypotheses
* **Null Hypothesis ($H_0$):** There is no statistically significant difference in mean purchase amount between subscribers and non-subscribers ($\mu_1 = \mu_2$).
* **Alternative Hypothesis ($H_1$):** There is a statistically significant difference in mean purchase amount between the two groups ($\mu_1 \neq \mu_2$).

#### 3. Assumption Checks

* **Normality Check:**
  * **Formal Tests (Kolmogorov-Smirnov & Shapiro-Wilk):** Both tests yield $p < 0.001$, formally rejecting normality.
  * **Visual Analysis (Q-Q Plot):** Observed values align closely with the expected normal line with minor tail deviations.
  * **Methodological Decision:** Due to the large sample size ($N = 3900 \gg 30$) and in accordance with the **Central Limit Theorem (CLT)**, the sampling distribution of the mean is normally distributed. Therefore, a parametric **Independent Samples t-test** is applicable.

* **Homogeneity of Variance (Levene's Test):**
  * $F = 0.295$, $p = 0.587$.
  * Since $p > 0.05$, the assumption of equal variances holds (**Equal variances assumed**). The first row of the test output is analyzed.

#### 4. Descriptive Statistics & T-test Results

**Group Statistics:**
| Subscription (`Subscription Status`) | $N$ | Mean | Std. Deviation ($SD$) | Std. Error Mean ($\text{SE}$) |
| :--- | :---: | :---: | :---: | :---: |
| **Yes (Subscribers)** | 1053 | $\$59.49$ | $23.450$ | $0.723$ |
| **No (Non-subscribers)** | 2847 | $\$59.87$ | $23.775$ | $0.446$ |

**Independent Samples t-test Results (Equal Variances Assumed):**
* **$t$-statistic:** $t(3898) = -0.437$
* **Significance ($p$-value):** $\text{Sig. (2-tailed)} = 0.662$
* **Mean Difference:** $-\$0.373$ (Subscribers spend $\$0.37$ less per order)
* **Std. Error Difference:** $0.854$
* **95% Confidence Interval of Difference:** $[-2.048;\ 1.302]$

**Effect Size:**
* **Cohen's $d$:** $-0.016$ (95% CI: $[-0.086;\ 0.055]$)
* **Interpretation:** $|d| < 0.20$ indicates a negligible / non-existent practical effect size.

#### 5. Business Conclusions & Recommendations
1. **Fail to Reject Null Hypothesis ($H_0$):** Since $p = 0.662 > 0.05$ and the 95% confidence interval spans zero, the difference of $\$0.37$ between groups is not statistically significant.
2. **Practical Significance:** Subscriptions do not incentivize customers to increase individual purchase amounts. The Average Order Value (AOV) for both groups remains virtually identical ($\approx \$60$).
3. **Business Recommendation:** The marketing team should not rely on the subscription model to drive basket size (Average Order Value). Focus should shift toward assessing whether subscriptions increase repeat order frequency (`Frequency of Purchases`).

---

### Task 2: Impact of Discounts on Customer Satisfaction

#### 1. Business Question & Context
Does applying a price discount (`Discount Applied`: *Yes*) result in higher customer satisfaction ratings (`Review Rating`) compared to full-price purchases (*No*)?

#### 2. Hypotheses
* **Null Hypothesis ($H_0$):** There is no statistically significant difference in mean review rating between purchases made with and without a discount ($\mu_1 = \mu_2$).
* **Alternative Hypothesis ($H_1$):** There is a statistically significant difference in mean review rating between the two groups ($\mu_1 \neq \mu_2$).

#### 3. Assumption Checks
* **Normality Check:** The Q-Q plot shows observed values aligning closely along the expected normal reference line. In accordance with the Central Limit Theorem ($N = 3900 \gg 30$), the sampling distribution of the mean is assumed normal, validating the use of a parametric Independent Samples t-test.
* **Homogeneity of Variance (Levene's Test):** $F = 0.081$, $p = 0.776 > 0.05$. The assumption of equal variances holds (**Equal variances assumed** row).

#### 4. Descriptive Statistics & T-test Results

**Group Statistics:**
| Discount Applied (`DiscountApplied`) | $N$ | Mean | Std. Deviation ($SD$) | Std. Error Mean ($\text{SE}$) |
| :--- | :---: | :---: | :---: | :---: |
| **Yes (Discounted)** | 1677 | $3.740$ | $0.7172$ | $0.0175$ |
| **No (Full Price)** | 2223 | $3.758$ | $0.7155$ | $0.0152$ |

**Independent Samples t-test Results (Equal Variances Assumed):**
* **$t$-statistic:** $t(3898) = -0.780$
* **Significance ($p$-value):** $\text{Sig. (2-tailed)} = 0.436$
* **Mean Difference:** $-0.0181$ (Discounted purchases rated $0.018$ points lower)
* **Std. Error Difference:** $0.0232$
* **95% Confidence Interval of Difference:** $[-0.0635;\ 0.0274]$

**Effect Size:**
* **Cohen's $d$:** $-0.025$ (95% CI: $[-0.089;\ 0.038]$)
* **Interpretation:** $|d| < 0.20$ indicates a negligible / non-existent practical effect size.

#### 5. Business Conclusions & Recommendations
1. **Fail to Reject Null Hypothesis ($H_0$):** Since $p = 0.436 > 0.05$ and the 95% confidence interval spans zero, the difference of $-0.018$ rating points between groups is not statistically significant.
2. **Practical Significance:** Price discounts do not enhance the customer's perceived value or satisfaction rating. The mean review rating remains virtually identical ($\approx 3.75 / 5.00$) regardless of promotional pricing.
3. **Business Recommendation:** Discount strategies should be deployed purely for volume acquisition or inventory clearance, not as a mechanism to boost customer satisfaction scores.

---

### Task 3: Product Category & Payment Method Association

#### 1. Business Question & Context
Is there a statistically significant association between the product category (`Category`) and the selected payment method (`Payment Method`)? The goal is to evaluate whether dynamic checkout UI optimization (prioritizing specific payment options based on cart contents) is justified.

#### 2. Hypotheses
* **Null Hypothesis ($H_0$):** Product category and payment method are independent (no association).
* **Alternative Hypothesis ($H_1$):** Product category and payment method are dependent (buyers of certain categories favor specific payment methods).

#### 3. Assumption Checks
* **Measurement Scale:** Both variables are nominal (4 categories $\times$ 6 payment methods).
* **Expected Cell Counts:** $0$ cells ($0.0\%$) have an expected count of less than $5$. The minimum expected count is $52.50$, fully satisfying the assumptions for Pearson's Chi-Square test.

#### 4. Chi-Square Test Results & Effect Size

**Contingency Table Summary ($4 \times 6$ Crosstabulation):**
* Analyzed $N = 3900$ valid cases across Categories (*Accessories, Clothing, Footwear, Outerwear*) and Payment Methods (*Bank Transfer, Cash, Credit Card, Debit Card, PayPal, Venmo*).

**Test Results:**
* **Pearson Chi-Square ($\chi^2$):** $\chi^2(15) = 18.322$
* **Significance ($p$-value):** $\text{Asymptotic Significance (2-sided)} = 0.246$
* **Likelihood Ratio:** $18.548$ ($p = 0.235$)

**Effect Size:**
* **Cramér's $V$:** $0.040$ ($p = 0.246$)
* **Phi ($\phi$):** $0.069$ ($p = 0.246$)
* **Interpretation:** Cramér's $V = 0.040$ indicates an extremely weak, practically non-existent association.

#### 5. Business Conclusions & Recommendations
1. **Fail to Reject Null Hypothesis ($H_0$):** Since $p = 0.246 > 0.05$, there is no statistically significant relationship between product category and payment choice.
2. **Practical Significance:** Customers select payment methods based on personal preference or convenience rather than the category of product being purchased.
3. **Business Recommendation:** E-commerce operations should **not** invest in building dynamic, category-specific checkout flows. A standardized, uniform payment gateway arrangement should be maintained for all shoppers regardless of cart contents.

---

### Task 4: Relationship Between History of Purchases and Current Order Value

#### 1. Business Question & Context
Is there a statistically significant correlation between a customer's purchasing history (`Previous Purchases`) and their current order value (`Purchase Amount USD`)? The objective is to evaluate whether historical engagement naturally leads to larger transaction sizes.

#### 2. Hypotheses
* **Null Hypothesis ($H_0$):** There is no linear correlation between previous purchase count and current purchase amount ($\rho = 0$).
* **Alternative Hypothesis ($H_1$):** There is a statistically significant linear correlation between the two variables ($\rho \neq 0$).

#### 3. Descriptive Statistics
* **Previous Purchases:** $\text{Mean} = 25.35$, $SD = 14.447$, $N = 3900$
* **Purchase Amount (USD):** $\text{Mean} = \$59.76$, $SD = 23.685$, $N = 3900$

#### 4. Correlation Analysis Results
* **Pearson Correlation Coefficient ($r$):** $0.008$
* **Significance ($p$-value):** $\text{Sig. (2-tailed)} = 0.615$
* **Sample Size ($N$):** $3900$

#### 5. Business Conclusions & Recommendations
1. **Fail to Reject Null Hypothesis ($H_0$):** Since $p = 0.615 > 0.05$, the correlation coefficient of $r = 0.008$ is statistically indistinguishable from zero.
2. **Practical Significance:** The frequency of past purchases does not influence basket size. A long-term loyal customer spends essentially the same amount per transaction as a new customer.
3. **Business Recommendation:** Customer segmentation should decouple order frequency from order value. Upselling and cross-selling campaigns must be designed independently of purchase history counts.

---
### Task 5: Predictive Modeling — Simple Linear Regression

#### 1. Business Question & Context
Can customer satisfaction (`Review Rating`) serve as a valid predictor for the transaction amount (`Purchase Amount USD`)? The business objective is to estimate how much order values increase per unit increase in customer rating.

#### 2. Model Specification & Hypotheses
* **Regression Model:** $Y = B_0 + B_1 \cdot X$
  * Dependent Variable ($Y$): `Purchase Amount USD`
  * Independent Variable ($X$): `Review Rating`
* **Null Hypothesis ($H_0$):** Slope $B_1 = 0$ (Review rating does not predict purchase amount).
* **Alternative Hypothesis ($H_1$):** Slope $B_1 \neq 0$ (Review rating statistically predicts purchase amount).

#### 3. Model Diagnostic & Assumption Checks
* **Linearity & Model Fit:** $R = 0.031$, $R^2 = 0.001$, Adjusted $R^2 = 0.001$. Standard Error of the Estimate = $23.677$.
* **Residual Analysis:** 
  * The standardized residual histogram exhibits a uniform (flat) distribution pattern rather than a normal bell curve.
  * The Normal P-P plot displays an S-curve deviation from the expected diagonal reference line, violating the normality of residuals assumption.

#### 4. Regression Analysis Results

**ANOVA Table Summary:**
* **Sum of Squares:** Regression = $2071.746$, Residual = $2,185,258.700$, Total = $2,187,330.446$
* **F-test Statistic:** $F(1, 3898) = 3.696$
* **Overall Model Significance:** $p = 0.055 > 0.05$

**Coefficients Summary:**
* **Constant ($B_0$):** $55.948$ ($t = 27.680$, $p < 0.001$, 95% CI $[51.985;\ 59.911]$)
* **Review Rating ($B_1$):** $1.018$ ($t = 1.922$, $p = 0.055$, Standardized $\beta = 0.031$, 95% CI $[-0.020;\ 2.056]$)

#### 5. Business Conclusions & Recommendations
1. **Fail to Reject Null Hypothesis ($H_0$):** Since $p = 0.055 > 0.05$, the relationship between rating and purchase amount is not statistically significant at the 5% level.
2. **Lack of Predictive Power:** With $R^2 = 0.001$, $99.9\%$ of the variation in transaction amounts is driven by unmeasured external factors (e.g., product seasonality, income, individual needs) rather than rating.
3. **Business Decision:** Customer review scores should **not** be used in financial models to forecast basket size or revenue growth.
