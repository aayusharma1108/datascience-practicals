# Practical: Exploring Teaching Ratings (Tenure, Age, Gender, Evaluations)

Descriptive analysis of the **TeachingRatings** dataset (from the `AER` R package, loaded via Rdatasets).

## Dataset

- **Source:** https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/AER/TeachingRatings.csv
- **Size:** 463 observations, 13 columns
- **Variables used:** `minority`, `tenure`, `age`, `gender`, `eval`

## Tools Used

Python, pandas, Matplotlib (Google Colab)

## Questions and Findings

### Q1. What percentage of minority instructors have tenure?

| Group | % with tenure |
|---|---|
| Minority | 84.38% |
| Non-minority | 76.94% |

The tenure rate is about 7.4 percentage points higher among minority instructors. This is a modest difference, and no significance test was run, so it should not be read as a strong effect.

### Q2. Does average age differ by tenure status?

| Tenure | Mean age |
|---|---|
| No | 50.19 |
| Yes | 47.80 |

Instructors without tenure have a higher average age in this sample. The standard deviations are also reported in the notebook output.

### Q3. Which plot suits the age variable?
A **histogram**, because age is a continuous numerical variable and a histogram shows how values are spread across intervals. Most instructors fall between roughly 45 and 65 years old.

### Q4. Gender counts: `bar()` vs `barh()`
- `plt.bar()` draws vertical bars with categories on the x-axis.
- `plt.barh()` draws horizontal bars with categories on the y-axis, which works better when category labels are long.

Both show the same counts of male and female instructors.

### Q5. Median evaluation score of tenured instructors
**Median = 4.0.** Tenured instructors are generally rated well, around "good" on the evaluation scale.

## Conclusion
- Tenure is slightly more common among minority instructors in this sample.
- Non-tenured instructors have a higher mean age.
- Most instructors are between about 45 and 65.
- Tenured instructors have a median evaluation of 4.0.

## Limitations
- Each row is a course evaluation, and instructors teach multiple courses, so the percentages and means count some instructors more than once.
- Differences are descriptive only. No statistical tests were run, so they may not be significant.
