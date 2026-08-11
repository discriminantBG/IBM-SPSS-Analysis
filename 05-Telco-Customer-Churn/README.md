# Telco Customer Churn & Revenue Analysis

## Overview
This project represents an in-depth statistical analysis of a telecommunications company's customer database (`WA_Fn-UseC_-Telco-Customer-Churn.csv`). The primary objective is to extract business insights regarding consumer behavior, revenue-generating factors, and the root causes of customer churn. The analysis was conducted on a sample of **7043** valid cases using IBM SPSS Statistics.

## Methodology
The following parametric statistical methods were applied to answer specific business questions:
*   **Independent-Samples T-Test (Welch)** to compare means between two independent groups.
*   **Pearson Chi-Square Test** to establish dependencies between categorical variables.
*   **One-Way Welch ANOVA & Games-Howell Post Hoc** to compare means across more than two groups when the assumption of homogeneity of variances is violated.
*   **Two-Way ANOVA (GLM Univariate)** to calculate the main effects and interactions between two categorical factors.
*   **Multiple Linear Regression** (including the creation of interaction terms) to predict continuous variables.
*   **Binary Logistic Regression** for classification and calculating churn risk.

---

## Business Cases & Results

### Case 1: Impact of Partner Status on Monthly Revenue (T-Test)
**Objective:** To determine whether customers with a partner generate higher monthly bills (`MonthlyCharges`).
*   Levene's test indicated unequal variances, therefore a Welch $t$-test was utilized.
*   **Result:** There is a statistically significant difference ($t(6927.01) = 8.15$, $p < .001$). 
*   Customers with a partner pay significantly higher average monthly bills ($M = 67.78$) compared to single customers ($M = 61.95$). 

### Case 2: Payment Preferences Among Senior Citizens (Chi-Square)
**Objective:** To investigate the relationship between age category (`SeniorCitizen`) and preferred payment method (`PaymentMethod`).
*   Validity checks showed **0%** of cells with an expected count below 5.
*   **Result:** A statistically significant dependence was established ($\chi^2(3) = 270.52$, $p < .001$).
*   Over half of the senior citizens (**52.0%**) prefer Electronic check, whereas this share is only **30.0%** among non-seniors.
*   Conversely, Mailed checks are significantly less popular among seniors (**8.2%** vs. **25.7%**).

### Case 3: Comparison of Charges by Payment Method (One-Way ANOVA)
**Objective:** To identify significant differences in average monthly bills (`MonthlyCharges`) across the four payment methods.
*   Due to the violation of homogeneity of variances, the Welch ANOVA and Games-Howell post-hoc tests were applied.
*   **Result:** A significant difference was established ($F_{Welch}(3, 3568.16) = 520.92$, $p < .001$).
*   Customers using Electronic check have the highest statistically significant bills ($M = 76.26$), while those using Mailed check have the lowest ($M = 43.92$). 
*   The only groups with no significant difference between them are those using Bank transfer (automatic) and Credit card (automatic).

### Case 4: Predicting Total Revenue (Multiple Linear Regression)
**Objective:** To model the total amount paid (`TotalCharges`) based on tenure in months (`tenure`) and the monthly bill (`MonthlyCharges`).
*   The initial model explained **89.5%** of the variance ($R^2 = .895$), but residual analysis revealed strong curvilinearity (heteroscedasticity).
*   **Optimization:** The model was refined by introducing an interaction term (the mathematical product of tenure and the monthly bill).
*   **Result:** The new model explains **99.9%** of the variance ($R^2 = .999$). 
*   The standard error was reduced to just **67.26**. 
*   The statistical significance is entirely captured by the interaction term ($p < .001$).

### Case 5: Predicting Customer Churn Risk (Binary Logistic Regression)
**Objective:** To isolate the key factors leading to customer churn (`Churn_num`).
*   The model is statistically significant (Omnibus Test $p < .001$).
*   It improves the prediction of churned customers from **0%** to **48.8%**, with an overall model accuracy of **78.8%**.
*   **Result 1 (Tenure):** For each additional month of tenure, the odds of a customer churning decrease by **3.2%** ($Exp(B) = 0.968$, $p < .001$).
*   **Result 2 (Contracts):** Customers on a month-to-month contract have **5.6 times** higher odds of churning compared to those on a 2-year contract ($Exp(B) = 5.613$, $p < .001$).
*   **Result 3 (Services):** Customers with Fiber optic internet represent the highest risk – they have over **7 times** higher odds of churning compared to customers without internet ($Exp(B) = 7.115$, $p < .001$).
*   **Result 4 (Pricing):** When isolating the effects of contracts and services, the amount of the monthly bill is not a statistically significant factor for churn ($p = .150$).

### Case 6: Impact of Internet and Contract on Revenue (Two-Way ANOVA)
**Objective:** To analyze the main effects and the interaction between internet connection type (`InternetService`) and contract duration (`Contract`) on the generated monthly bills.
*   **Result 1 (Internet):** A statistically significant main effect of internet type was found ($F(2, 7034) = 20456.93$, $p < .001$, $\eta_p^2 = .853$). Fiber optic is the most expensive service with an average bill of **96.79**, followed by DSL at **60.69**, and no internet at **21.00**.
*   **Result 2 (Contracts):** A significant main effect of contract type is present ($F(2, 7034) = 798.15$, $p < .001$, $\eta_p^2 = .185$). When controlling for the service type, 2-year contracts yield the highest revenue (**65.60** on average) compared to month-to-month contracts (**52.55**).
*   **Result 3 (Interaction):** Contract length increases revenue most notably for premium services. The difference is most pronounced with Fiber optic – month-to-month generates **87.02**, whereas a 2-year contract jumps to **104.57**. For customers without internet, the contract type does not significantly alter the bill (ranging between **20.41** and **21.78**).

---

## Key Business Recommendations (Actionable Insights)
*   **Focus on Fiber Optic Quality:** A technical audit of the fiber optic internet service is imperative, as it is the leading cause (posing over **7 times** higher risk) of customer loss.
*   **Migration to Term Contracts:** Marketing campaigns should incentivize customers on month-to-month contracts to switch to 1- or 2-year plans. This drastically reduces the churn risk and simultaneously increases the average revenue from customers with internet services (reaching up to **104.57** for fiber optic).
*   **Develop "Family Packages":** Customers with a partner are more profitable, which justifies creating targeted cross-selling offers to encourage adding a second household line.
*   **Maintain Pricing Levels:** According to the logistic regression, the monthly bill itself does not independently drive churn; therefore, aggressively lowering prices is not an optimal customer retention strategy.
