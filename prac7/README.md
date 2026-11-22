# Practical 7: Understanding Regression with T-Test and ANOVA

## Aim
To study the relationship between instructors' gender, age, beauty scores and teaching evaluation scores using regression analysis, a t-test, ANOVA and correlation.

## Objectives
- Understand regression analysis and its application in statistics
- Examine whether gender affects teaching evaluation scores (regression with a t-test)
- Study whether beauty scores differ across age groups (regression with ANOVA)
- Examine the relationship between teaching evaluation and beauty scores
- Interpret regression coefficients, p-values and R-squared
- Draw conclusions from the TeachingRatings dataset

## Dataset
- **Source:** https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/AER/TeachingRatings.csv (from the `AER` R package)
- **Size:** 463 course evaluations, 13 columns
- **Variables used:** `eval`, `gender`, `age`, `beauty`

## Tools Used
Python, pandas, SciPy, statsmodels (`ols`, `anova_lm`) (Google Colab)

All tests use a significance level of **α = 0.05**.

## Results

### Q1. Regression with t-test: `eval ~ gender`
Model: `smf.ols("eval ~ C(gender)", data=df)`

| Term | Coefficient | Std. error | t | p-value |
|---|---|---|---|---|
| Intercept (female mean) | 3.901 | 0.039 | 99.19 | < 0.001 |
| Male (vs. female) | 0.168 | 0.052 | 3.25 | 0.001 |

R² = 0.022, F = 10.56, p = 0.0012.

Male instructors score 0.168 points higher on average than female instructors, and the difference is statistically significant (p < 0.05). However, R² = 0.022 means gender explains only about 2.2% of the variation in evaluation scores, so the effect is small. With one binary predictor, this regression is equivalent to a two-sample t-test (here F = t²).

### Q2. Regression with ANOVA: `beauty ~ age group`
Age was grouped into **40 and younger**, **41 to 56** and **57 and older** using `pd.cut`.

| Source | df | Sum of squares | Mean square | F | p-value |
|---|---|---|---|---|---|
| Age group | 2 | 20.42 | 10.21 | 17.60 | 4.3 × 10⁻⁸ |
| Residual | 460 | 266.93 | 0.58 | | |

p < 0.05, so we reject H₀ (equal mean beauty score in all age groups). At least one age group has a different mean beauty score. ANOVA does not show which groups differ, so a post-hoc test such as Tukey's HSD is needed.

### Q3. Regression and correlation: `eval ~ beauty`

| Term | Coefficient | Std. error | t | p-value |
|---|---|---|---|---|
| Intercept | 3.998 | 0.025 | 157.73 | < 0.001 |
| Beauty | 0.133 | 0.032 | 4.13 | < 0.001 |

R² = 0.036, F = 17.08, p = 4.25 × 10⁻⁵.

Each one-unit increase in beauty score is associated with an average increase of 0.133 in the evaluation score, and the relationship is statistically significant. R² = 0.036 means beauty explains only about 3.6% of the variation in evaluation scores. The correlation coefficient is r = √0.036 ≈ 0.19, a weak positive correlation.

## Summary Table

| Analysis | Predictor | Key result | p-value | Decision |
|---|---|---|---|---|
| Regression / t-test | Gender | Male +0.168, R² = 0.022 | 0.001 | Reject H₀ |
| Regression / ANOVA | Age group | F = 17.60 | 4.3 × 10⁻⁸ | Reject H₀ |
| Regression / correlation | Beauty | Slope 0.133, R² = 0.036 | < 0.001 | Reject H₀ |

## Conclusion
Gender and beauty score both have statistically significant but small relationships with teaching evaluation scores, and beauty scores differ across age groups. Regression coefficients show the size and direction of an effect, p-values show whether it is likely due to chance, and R² shows how much of the variation the model explains. Here R² is low in both models, so other factors matter much more.

## Limitations
- Each row is a course evaluation and instructors teach multiple courses, so observations are not fully independent. The Durbin-Watson statistics (about 1.4) hint at correlated residuals, which can make p-values look more significant than they should.
- The residuals are slightly skewed (skew about -0.5), so the normality assumption holds only approximately.
- These are associations, not causal effects.
