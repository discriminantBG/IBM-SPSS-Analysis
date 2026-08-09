# IBM HR Analytics: Exploratory Data Analysis, Hypothesis Testing and Predictive Modeling in SPSS

## Project Overview

This project presents an end-to-end statistical analysis of employee compensation, gender pay differences, educational alignment, departmental salary variation, and the main predictors of monthly income.

The analysis was conducted in **IBM SPSS Statistics** using the **IBM HR Analytics Employee Attrition & Performance** dataset. Five business questions were translated into statistical hypotheses and investigated using descriptive statistics, parametric and non-parametric procedures, effect sizes, post-hoc comparisons, regression diagnostics, and business interpretation.

The purpose of the project is not only to report statistically significant results, but also to:

- select an appropriate statistical method for each business question;
- verify the assumptions of every method;
- distinguish statistical significance from practical importance;
- interpret effect sizes and confidence intervals;
- identify limitations in the data and models;
- translate statistical output into responsible HR recommendations.

---

## Executive Summary

The dataset contains **1,470 employee records** and no missing values in the variables used in the analyses.

The main findings are:

1. `MonthlyIncome` is strongly right-skewed and not normally distributed. The median is therefore a better description of the typical salary than the mean.
2. No statistically significant unadjusted difference in average monthly income was detected between male and female employees. The observed effect was negligible.
3. `EducationField` and `Department` have a strong and statistically significant association, indicating substantial alignment between academic background and organizational placement.
4. Average monthly income differs statistically across departments, but the practical effect of department is extremely small. Only Sales and Research & Development differed significantly in the post-hoc comparison.
5. `TotalWorkingYears` is the strongest unique predictor of log monthly income among age, total experience, and company tenure. `YearsAtCompany` has a much weaker positive contribution, while `Age` is not significant after experience is controlled.

---

## Dataset

- **Dataset:** IBM HR Analytics Employee Attrition & Performance
- **Sample size:** \(N=1,470\)
- **Missing values in analyzed variables:** 0
- **Unit of analysis:** One employee record
- **Software:** IBM SPSS Statistics v28+

### Principal variables

| Variable | Measurement level | Description |
|---|---|---|
| `MonthlyIncome` | Scale | Employee monthly income |
| `Age` | Scale | Employee age in years |
| `TotalWorkingYears` | Scale | Total years of professional experience |
| `YearsAtCompany` | Scale | Years at the current company |
| `DistanceFromHome` | Scale | Distance between home and workplace |
| `Gender` | Nominal | Employee gender |
| `Department` | Nominal | Organizational department |
| `EducationField` | Nominal | Employee field of education |
| `Attrition` | Nominal | Whether the employee left the company |
| `JobLevel` | Ordinal | Organizational job level |

---

# Phase 1 — Exploratory Data Analysis and Normality Testing

## Business Question 1

> What is the distribution of employee monthly income? Are salaries normally distributed, or are the results affected by skewness and extreme values?

## Why this analysis was required

Before selecting inferential procedures, it is necessary to understand the distribution of the quantitative outcome. A strongly skewed salary variable can:

- make the mean unrepresentative of a typical employee;
- produce unusual observations and long tails;
- affect residual distributions in regression models;
- motivate transformations or robust/non-parametric methods.

## Statistical procedures

- descriptive statistics;
- mean and median comparison;
- standard deviation;
- skewness and kurtosis;
- Kolmogorov–Smirnov test;
- Shapiro–Wilk test;
- histogram;
- Normal Q–Q Plot;
- boxplot.

## Hypotheses for the normality tests

\[
H_0:\text{MonthlyIncome follows a normal distribution}
\]

\[
H_1:\text{MonthlyIncome does not follow a normal distribution}
\]

At \(\alpha=.05\):

- if \(p>.05\), normality is not rejected;
- if \(p\leq.05\), normality is rejected.

Normality tests are sensitive in large samples, so their p-values were interpreted together with skewness, the histogram, Q–Q Plot, boxplot, and the difference between the mean and median.

## SPSS procedure

1. Select **Analyze → Descriptive Statistics → Explore**.
2. Move `MonthlyIncome` to **Dependent List**.
3. Under **Statistics**, request descriptive statistics.
4. Under **Plots**, select:
   - histogram;
   - normality plots with tests;
   - boxplot.
5. Select **OK**.

## Results

| Statistic | Result |
|---|---:|
| Mean | $6,502.93 |
| Median | $4,919.00 |
| Standard deviation | $4,707.96 |
| Maximum | $19,999 |
| Skewness | 1.370 |
| Kolmogorov–Smirnov | .169, \(p<.001\) |
| Shapiro–Wilk | .828, \(p<.001\) |

Both normality tests are significant, so the null hypothesis of normality is rejected. The mean is also substantially higher than the median, and the graphical outputs show a long upper tail.

## Interpretation

`MonthlyIncome` is **strongly positively/right-skewed**. Most employees are concentrated in the entry-to-middle salary range, while a smaller group of highly paid employees extends the distribution towards the maximum of $19,999.

The mean is pulled upward by the upper tail. Consequently, the median of **$4,919** is a better measure of the typical employee's monthly compensation than the mean of **$6,502.93**.

## Business conclusion

HR salary reporting should include the median and percentile-based summaries instead of relying only on the arithmetic mean. Reporting only the mean would make the typical salary appear higher than it is for most employees.

---

# Phase 2 — Gender Pay Comparison

## Business Question 2

> Is there a statistically significant difference in average monthly income between male and female employees?

## Method

An **Independent Samples t-test** was used because:

- the dependent variable, `MonthlyIncome`, is quantitative;
- the grouping variable, `Gender`, contains two independent groups;
- the objective is to compare the group means.

Levene's test was used to determine whether equal variances could be assumed. Cohen's \(d\) was used to evaluate the practical magnitude of the observed difference.

## Hypotheses

\[
H_0:\mu_{female}=\mu_{male}
\]

There is no difference in population mean monthly income between female and male employees.

\[
H_1:\mu_{female}\neq\mu_{male}
\]

There is a difference in population mean monthly income between the two groups.

## SPSS procedure

1. Select **Analyze → Compare Means → Independent-Samples T Test**.
2. Move `MonthlyIncome` to **Test Variable(s)**.
3. Move `Gender` to **Grouping Variable**.
4. Define the two group values.
5. Request the effect-size output if available in the installed SPSS version.
6. Select **OK**.

## Descriptive results

| Group | \(N\) | Mean | Standard deviation |
|---|---:|---:|---:|
| Female | 588 | $6,686.57 | $4,695.61 |
| Male | 882 | $6,380.51 | $4,714.86 |

The descriptive mean difference is approximately **$306.06 in favor of female employees**.

## Levene's test

\[
F=.259,\quad p=.611
\]

Because \(p>.05\), the equal-variance assumption is not rejected. Therefore, the **Equal variances assumed** row of the t-test output is used.

## t-test result

\[
t(1468)=-1.221,\quad p=.222
\]

The 95% confidence interval for the male-minus-female mean difference is:

\[
[-\$797.65,\ +\$185.53]
\]

The interval includes zero, which agrees with the non-significant p-value.

## Effect size

\[
d=-.065
\]

The absolute effect size is extremely small and practically negligible.

## Interpretation

Because \(p=.222>.05\), the null hypothesis is not rejected. The sample does not provide sufficient evidence of a difference in average monthly income between male and female employees.

The correct conclusion is **not** that the organization has proven zero gender bias. This test is an unadjusted comparison of two group means. It does not control for job level, job role, department, experience, working pattern, performance, or other salary-related characteristics.

## Business conclusion

No statistically significant **unadjusted** gender pay difference was detected, and the observed effect size was negligible. A more complete pay-equity audit should use multiple regression and compare employees with similar job level, role, experience, department, and other relevant characteristics.

---

# Phase 3 — Educational Alignment Across Departments

## Business Question 3

> Is an employee's field of education associated with the department in which the employee works?

## Method

A **Chi-square test of independence** was selected because both variables are categorical:

- `EducationField` — nominal;
- `Department` — nominal.

Cramér's \(V\) was used to measure the strength of the association because statistical significance alone does not show whether the relationship is weak or strong.

## Hypotheses

\[
H_0:\text{EducationField and Department are independent}
\]

\[
H_1:\text{EducationField and Department are associated}
\]

## SPSS procedure

1. Select **Analyze → Descriptive Statistics → Crosstabs**.
2. Place one categorical variable in **Rows** and the other in **Columns**.
3. Under **Statistics**, select:
   - Chi-square;
   - Phi and Cramér's V.
4. Under **Cells**, select:
   - observed counts;
   - expected counts;
   - appropriate row or column percentages.
5. Select **OK**.

## Assumption check

Only **11.1% of the cells** had expected counts below 5. This is within the commonly applied rule that fewer than 20% of expected counts should be below 5, with no expected count below 1.

**Assessment:** The Pearson chi-square approximation is acceptable.

## Results

\[
\chi^2(10)=1024.979,\quad p<.001
\]

Because \(p<.05\), the null hypothesis of independence is rejected.

The effect size was:

\[
V=.590,\quad p<.001
\]

This represents a strong association between field of education and department.

## Crosstabulation findings

- 100% of employees with a Marketing education in this sample were placed in Sales.
- 100% of employees with a Human Resources education in this sample were placed in Human Resources.
- 72.6% of Life Sciences graduates were placed in Research & Development.
- 78.2% of Medical graduates were placed in Research & Development.

These percentages describe the observed dataset and should not automatically be generalized as permanent recruitment rules without confirming the sampling context.

## Business conclusion

Academic specialization and departmental placement are strongly aligned. The pattern is consistent with targeted recruitment and role allocation: Marketing education aligns with Sales, Human Resources education aligns with HR, and Life Sciences/Medical education aligns primarily with Research & Development.

The result may support workforce-planning decisions, but HR should also monitor whether highly rigid educational filters unnecessarily exclude candidates with transferable skills or non-traditional career paths.

---

# Phase 4 — Salary Differences Across Departments

## Business Question 4

> Does average monthly income differ across Human Resources, Research & Development, and Sales?

## Method

A **One-Way ANOVA** framework was selected because:

- `MonthlyIncome` is quantitative;
- `Department` is a categorical factor with three independent groups;
- the objective is to compare more than two group means.

Because Levene's test detected unequal variances, the classical equal-variance ANOVA and Tukey procedure were not treated as the primary evidence. The robust **Welch test** and **Games–Howell post-hoc test** were used instead.

## Hypotheses

\[
H_0:\mu_{HR}=\mu_{R\&D}=\mu_{Sales}
\]

\[
H_1:\text{At least one departmental mean differs}
\]

## SPSS procedure

1. Select **Analyze → Compare Means → One-Way ANOVA**.
2. Move `MonthlyIncome` to **Dependent List**.
3. Move the numeric-coded `Department` variable to **Factor**.
4. Under **Options**, select:
   - Descriptive;
   - Homogeneity of variance test;
   - Welch test;
   - Means plot.
5. Under **Post Hoc**, select:
   - Tukey for equal variances;
   - Games–Howell for unequal variances.
6. Use Levene's result to decide which post-hoc output is appropriate.

If `Department` is stored as a string variable and is unavailable in the required menu, it must first be converted to a numeric categorical variable using **Transform → Automatic Recode**. The recoded variable should remain measured as nominal.

## Descriptive departmental means

| Department | \(N\) | Mean monthly income |
|---|---:|---:|
| Human Resources | 63 | $6,654.51 |
| Research & Development | 961 | $6,281.25 |
| Sales | 446 | $6,959.17 |

## Homogeneity of variance

The standard first row of Levene's table, **Based on Mean**, reported:

\[
F(2,1467)=12.361,\quad p<.001
\]

Because \(p<.05\), the equal-variance assumption is rejected.

The median-based and trimmed-mean variants also produced significant results, reinforcing the conclusion that group variances are unequal.

## Robust overall comparison

The Welch test reported:

\[
F_W(2,163.838)=3.708,\quad p=.027
\]

Because \(p=.027<.05\), the null hypothesis of equal departmental means is rejected. At least one department differs in mean monthly income.

## Games–Howell post-hoc comparisons

| Comparison | Mean difference | \(p\) | Conclusion |
|---|---:|---:|---|
| Sales vs Research & Development | +$677.92 | .018 | Significant |
| Human Resources vs Research & Development | — | .871 | Not significant |
| Human Resources vs Sales | — | .914 | Not significant |

Sales employees earned significantly more on average than Research & Development employees. The Human Resources group did not differ significantly from either of the other departments.

## Effect size

\[
\eta^2=.004
\]

Department explains only approximately **0.4% of the variance in monthly income**.

## Interpretation

The overall departmental difference is statistically significant, but its practical magnitude is extremely small. The large sample makes it possible to detect relatively small mean differences.

This demonstrates why the p-value and effect size must be interpreted together:

- the Welch p-value shows that a difference is unlikely to be entirely due to sampling error;
- \(\eta^2\) shows that department contributes very little to explaining salary variation.

## Business conclusion

Sales employees receive slightly higher average compensation than Research & Development employees, potentially reflecting commissions, bonuses, or different role structures. However, department by itself is not a major salary determinant. Job level, job role, seniority, and total experience are likely much more important.

---

# Phase 5 — Predictive Salary Modeling

## Business Question 5

> How do `Age`, `TotalWorkingYears`, and `YearsAtCompany` jointly predict monthly income, and which variable is the strongest predictor after the others are controlled?

## Method

A simultaneous **Multiple Linear Regression** was fitted using the Enter method.

The first model used raw `MonthlyIncome`. Because the outcome and residuals were strongly non-normal, the dependent variable was transformed using the natural logarithm:

```text
LnMonthlyIncome = LN(MonthlyIncome)
```

The final model was:

\[
\ln(\text{MonthlyIncome})=
\beta_0+
\beta_1(\text{Age})+
\beta_2(\text{TotalWorkingYears})+
\beta_3(\text{YearsAtCompany})+\varepsilon
\]

## Hypotheses

### Overall model

\[
H_0:\beta_1=\beta_2=\beta_3=0
\]

\[
H_1:\text{At least one }\beta_j\neq0
\]

### Individual predictor

For each predictor:

\[
H_0:\beta_j=0
\qquad\text{versus}\qquad
H_1:\beta_j\neq0
\]

## SPSS procedure

1. Select **Transform → Compute Variable**.
2. Create `LnMonthlyIncome` using `LN(MonthlyIncome)`.
3. Select **Analyze → Regression → Linear**.
4. Set `LnMonthlyIncome` as **Dependent**.
5. Set `Age`, `TotalWorkingYears`, and `YearsAtCompany` as **Independent(s)**.
6. Retain **Method: Enter**.
7. Under **Statistics**, select:
   - Estimates;
   - Model fit;
   - Confidence intervals;
   - Collinearity diagnostics;
   - Durbin–Watson.
8. Under **Plots**, set `ZPRED` on X and `ZRESID` on Y and request:
   - Histogram;
   - Normal probability plot.
9. Under **Save**, request:
   - standardized residuals;
   - Cook's distance;
   - leverage values.

## Model summary

| Statistic | Result | Interpretation |
|---|---:|---|
| \(R\) | .743 | Strong observed-to-predicted association on the log scale |
| \(R^2\) | .552 | 55.2% of log-income variance explained |
| Adjusted \(R^2\) | .551 | Adjusted explanatory power |
| Standard error of estimate | .44542 | Residual error on the log scale |
| Durbin–Watson | 1.977 | No clear first-order residual autocorrelation |

The model explains **55.2% of the variation in `LnMonthlyIncome`**. It should not be stated that it explains exactly 55.2% of the variation in income measured directly in dollars because the dependent variable is logarithmic.

## Overall model significance

\[
F(3,1466)=600.973,\quad p<.001
\]

The overall null hypothesis is rejected. The three predictors considered jointly predict log monthly income significantly better than an intercept-only model.

## Regression coefficients

| Predictor | \(B\) | SE | Standardized \(\beta\) | \(t\) | \(p\) | 95% CI for \(B\) | Tolerance | VIF |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Constant | 7.834 | .054 | — | 144.174 | <.001 | [7.727, 7.940] | — | — |
| `Age` | approximately .000 | .002 | -.003 | -.112 | .911 | [-.004, .003] | .515 | 1.942 |
| `TotalWorkingYears` | .060 | .003 | **.698** | 23.462 | <.001 | [.055, .065] | .345 | 2.897 |
| `YearsAtCompany` | .008 | .002 | **.070** | 3.050 | .002 | [.003, .012] | .580 | 1.723 |

The fitted equation using the rounded SPSS coefficients is:

\[
\widehat{\ln(\text{MonthlyIncome})}
=7.834
+0.000(\text{Age})
+0.060(\text{TotalWorkingYears})
+0.008(\text{YearsAtCompany})
\]

The exact coefficient for `Age` is slightly negative but appears as .000 after rounding.

## Coefficient interpretation

### Total professional experience

\[
B=.060,\quad \beta=.698,\quad p<.001
\]

For a log-transformed dependent variable, the exact percentage difference is calculated as:

\[
100(e^B-1)
\]

Therefore:

\[
100(e^{.060}-1)\approx6.18\%
\]

Holding age and company tenure constant, one additional year of total professional experience is associated with approximately **6.2% higher expected monthly income**.

### Years at the company

\[
B=.008,\quad \beta=.070,\quad p=.002
\]

\[
100(e^{.008}-1)\approx0.80\%
\]

Holding age and total experience constant, one additional year at the current company is associated with approximately **0.8% higher expected monthly income**.

### Age

\[
\beta=-.003,\quad p=.911
\]

Age is not statistically significant, and its 95% confidence interval includes zero. It contributes no detectable additional linear predictive information once total working experience and company tenure are controlled.

This does not mean that age has no simple relationship with income. It means that age adds no unique predictive value after the two experience variables are already in the model.

## Strongest predictor

The standardized beta coefficients are compared because they place all predictors on the same scale:

| Rank | Predictor | Absolute \(\beta\) | Interpretation |
|---:|---|---:|---|
| 1 | `TotalWorkingYears` | **.698** | Strongest unique predictor |
| 2 | `YearsAtCompany` | .070 | Significant but weak contribution |
| 3 | `Age` | .003 | No significant unique contribution |

`TotalWorkingYears` is the strongest **predictor among the three included variables**. The result should not be described as a causal effect.

## Regression diagnostics

### Residual normality

The log transformation produced an approximately bell-shaped residual histogram and a Normal P–P Plot that closely followed the diagonal.

**Conclusion:** Residual normality improved substantially and is reasonably acceptable.

The regression assumption concerns the residuals, not whether each predictor is normally distributed.

### Independence

\[
\text{Durbin–Watson}=1.977
\]

The value is close to 2 and does not indicate clear first-order autocorrelation. Actual case independence also depends on the dataset's sampling design.

### Multicollinearity

All VIF values are below 3 and all tolerance values exceed .20. The maximum condition index is 14.247.

**Conclusion:** The predictors are related but do not exhibit severe multicollinearity.

### Outliers and influence

- standardized residual range: -3.381 to 2.961;
- maximum Cook's distance: .044;
- maximum centered leverage: .020.

At least one standardized residual falls below -3, and some cases have comparatively high leverage. However, the maximum Cook's distance is far below 1, so no single record appears to dominate the model.

### Linearity and homoscedasticity

The `ZRESID` versus `ZPRED` plot retained visible bands, changes in spread, and systematic structure after the log transformation.

This suggests possible:

- heteroscedasticity;
- nonlinear relationships;
- omitted organizational variables;
- discrete salary bands associated with `JobLevel` or `JobRole`.

The transformation improved normality but did not make every model assumption perfect. Conventional standard errors and confidence intervals—particularly for the relatively weak `YearsAtCompany` coefficient—should therefore be interpreted cautiously.

## Business conclusion

Total professional experience is the dominant salary predictor among the three variables. Internal tenure also has a positive association, but its unique contribution is much smaller. Age adds no independent predictive information once experience is controlled.

The results may indicate that accumulated market experience is rewarded more strongly than organizational tenure. This could create salary-compression risks if experienced external hires receive substantially higher salaries than long-serving employees with similar responsibilities.

## Recommended model extension

A future model should include:

- `JobLevel`;
- `JobRole`;
- `Department`;
- relevant performance variables;
- other compensation-related controls.

Categorical variables should be dummy-coded appropriately. Robust standard errors or a suitable bootstrap procedure should also be considered because the residual plot suggests possible heteroscedasticity.

---

# Consolidated HR Recommendations

## 1. Improve compensation reporting

Use the median, quartiles, and distribution plots alongside the mean. The strong right skew makes the mean alone a misleading description of typical compensation.

## 2. Expand the gender pay-equity audit

The unadjusted t-test found no significant mean difference, but this is not sufficient to prove complete pay equity. Conduct an adjusted regression or matched comparison controlling for job level, role, department, experience, tenure, and other relevant variables.

## 3. Maintain educational alignment without excessive rigidity

The strong relationship between education and department supports specialized recruitment. HR should nevertheless ensure that hiring criteria allow for transferable skills and alternative professional pathways.

## 4. Focus beyond department-level salary comparisons

Department explains only 0.4% of income variance. Compensation reviews should focus more heavily on job level, role, total experience, performance, and salary bands.

## 5. Review experience and tenure rewards

Total working experience has a much stronger salary relationship than internal tenure. HR should examine whether long-serving employees experience salary compression relative to newly hired experienced employees.

## 6. Improve the predictive model

Add job hierarchy variables and use robust inference. The present model has strong explanatory power, but the residual structure indicates that continuous experience variables do not capture the full compensation system.

---

# Statistical Methods Demonstrated

| Business problem | Statistical method | Supporting evidence |
|---|---|---|
| Describe salary distribution | EDA and normality analysis | Mean, median, skewness, K–S, Shapiro–Wilk, histogram, Q–Q Plot, boxplot |
| Compare two independent groups | Independent Samples t-test | Levene's test, t-test, 95% CI, Cohen's \(d\) |
| Test association between categorical variables | Chi-square test of independence | Expected counts, Pearson \(\chi^2\), Cramér's \(V\), crosstab percentages |
| Compare more than two independent means | One-Way ANOVA framework | Levene, Welch, Games–Howell, \(\eta^2\) |
| Predict a quantitative outcome | Multiple linear regression | \(R^2\), adjusted \(R^2\), \(F\), \(B\), \(\beta\), \(t\), CI, VIF, residual diagnostics |

---

# Repository Contents

```text
IBM-HR-Analytics-SPSS/
├── README.md
├── input/
│   └── ibm_hr.sav
│   └── WA_Fn-UseC_-HR-Employee-Attrition.csv
├── output/
    └── ibm_hr.spv


```

# Portfolio Skills Demonstrated

- exploratory data analysis in IBM SPSS;
- correct identification of nominal, ordinal, and scale variables;
- formulation of null and alternative hypotheses;
- selection of parametric and robust statistical procedures;
- normality and assumption testing;
- interpretation of p-values, confidence intervals, and effect sizes;
- Independent Samples t-test and Levene's test;
- chi-square test and Cramér's \(V\);
- One-Way ANOVA, Welch test, and Games–Howell comparisons;
- multiple linear regression and logarithmic transformation;
- interpretation of unstandardized and standardized coefficients;
- multicollinearity, residual, leverage, and influence diagnostics;
- distinction between statistical and practical significance;
- translation of statistical results into HR recommendations;
- critical reporting of limitations and avoidance of causal overstatement.

---

# Final Project Conclusion

The project shows that employee compensation cannot be understood through a single group comparison or descriptive statistic.

Monthly income is strongly right-skewed, so median-based reporting is essential. No significant unadjusted gender difference was detected. Educational background is strongly aligned with departmental placement. Departmental salary differences exist but explain very little of total income variation. Among age, total working experience, and company tenure, total professional experience is by far the strongest unique predictor of log monthly income.

The combined evidence suggests that compensation is influenced more by professional experience and organizational job structure than by gender, department alone, or chronological age. A stronger future salary model should incorporate job level and job role and should use robust inference to address the remaining residual structure.

---

**Author:** Georgi Bratkov  
**GitHub Portfolio:** [github.com/discriminantBG](https://github.com/discriminantBG)
