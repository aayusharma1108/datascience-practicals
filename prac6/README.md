# Practical 6: Understanding T-Test, ANOVA and Chi-Square

## Aim
To understand and apply statistical tests (independent t-test, one-way ANOVA, chi-square test of independence and Pearson correlation) using Python.

## Objectives
- Compare the mean evaluation scores of male and female instructors
- Compare beauty scores across age groups
- Examine the association between tenure and gender
- Measure the correlation between teaching evaluation and beauty scores
- Understand p-values and statistical hypothesis testing

## Dataset
- **Source:** TeachingRatings dataset from the `AER` R package (https://vincentarelbundock.github.io/Rdatasets/csv/AER/TeachingRatings.csv)
- **Size:** 463 course evaluations, 13 columns
- **File:** `TeachingRatings.csv` (included in this folder)
- **Variables used:** `eval`, `gender`, `age`, `beauty`, `tenure`

## Tools Used
Python, pandas, NumPy, SciPy (`scipy.stats`), Matplotlib, Seaborn (Google Colab)

All tests use a significance level of **α = 0.05**.

## Results

### Q1. Independent two-sample t-test: does gender affect teaching evaluation?
Welch's t-test (`equal_var=False`) was used.

- **H₀:** the mean evaluation scores of male and female instructors are equal
- **H₁:** the means differ

| Group | Mean evaluation |
|---|---|
| Male | 4.07 |
| Female | 3.90 |

T-statistic = 3.267, p-value = 0.0012.
**Decision:** p < 0.05, so reject H₀. The mean evaluation differs significantly between male and female instructors in this dataset.

### Q2. One-way ANOVA: does the beauty score differ by age group?
Age was divided into groups (Below 30, 30-40, 40-50, Above 50) using `pd.cut`, because ANOVA needs a categorical grouping variable.

- **H₀:** the mean beauty scores are equal across all age groups
- **H₁:** at least one age group has a different mean

F-statistic = 10.97, p-value ≈ 5.75 × 10⁻⁷.
**Decision:** p < 0.05, so reject H₀. At least one age group has a different mean beauty score. ANOVA does not say which groups differ. A post-hoc test such as Tukey's HSD would show that.

### Q3. Chi-square test: is tenure associated with gender?

| Tenure | Female | Male |
|---|---|---|
| No | 50 | 52 |
| Yes | 145 | 216 |

Chi-square = 2.207, degrees of freedom = 1, p-value = 0.137.
**Decision:** p > 0.05, so fail to reject H₀. There is not enough evidence that tenure and gender are associated.

### Q4. Pearson correlation: evaluation score vs. beauty score
Pearson r = 0.189, p-value ≈ 4.25 × 10⁻⁵.
**Decision:** p < 0.05, so reject H₀. There is a statistically significant but **weak positive** correlation. A value of 0.19 means beauty explains only about 3.6% of the variation in evaluation scores (r² ≈ 0.036).

## Summary Table

| Test | Variables | Statistic | p-value | Decision |
|---|---|---|---|---|
| Welch t-test | eval by gender | t = 3.267 | 0.0012 | Reject H₀ |
| One-way ANOVA | beauty by age group | F = 10.97 | 5.7 × 10⁻⁷ | Reject H₀ |
| Chi-square | tenure and gender | χ² = 2.207 | 0.137 | Fail to reject H₀ |
| Pearson correlation | eval and beauty | r = 0.189 | 4.2 × 10⁻⁵ | Reject H₀ |

## Conclusion
Male instructors have a significantly higher mean evaluation than female instructors, beauty scores differ across age groups, and evaluation scores have a weak positive correlation with beauty scores. Tenure and gender were not significantly associated.

## Limitations
- Each row is a course evaluation, and instructors teach several courses, so observations are not fully independent. This can make p-values look more significant than they should.
- A significant p-value shows that an effect is unlikely to be due to chance. It does not show how large or important the effect is.
- Correlation and group differences do not show cause and effect.
- Chi-square assumes expected counts of at least 5 in each cell, which holds for this table.
