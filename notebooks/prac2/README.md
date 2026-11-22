# Practical: Descriptive Statistics on Teaching Ratings

Exploratory and descriptive analysis of the **TeachingRatings** dataset (from the `AER` R package, loaded via Rdatasets).

## Dataset

- **Source:** https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/AER/TeachingRatings.csv
- **Size:** 463 observations, 13 columns
- **Variables used:** `students`, `beauty`, `gender`, `tenure`

## Tools Used

Python, pandas, Matplotlib (Google Colab)

## Questions and Findings

### Q1. Is the data a time series or cross-sectional?
**Cross-sectional.** Each row is a course evaluation measured at a single point in time, and there is no time variable tracking the same unit over successive periods. Some instructors appear in several rows because they teach more than one course, but those rows are different courses, not repeated measurements over time. A time series would need the same unit tracked across time periods.

### Q2. Mean, median, minimum and maximum of `students`

| Statistic | Value |
|---|---|
| Mean | 36.62 |
| Median | 23 |
| Minimum | 5 |
| Maximum | 380 |

The mean is well above the median, and the maximum (380) is far larger than typical class sizes. The distribution is therefore **right-skewed**, with a few very large classes pulling the mean up. The median describes a typical class better here.

### Q3. Descriptive statistics table
`df.describe()` gives the count, mean, standard deviation, minimum, quartiles and maximum for every numeric variable. See the output in the notebook.

### Q4. Histogram of `beauty`
The beauty score is a standardized variable ranging roughly from -1.45 to 1.97. Most instructors fall between about -1 and 0.5, near the average. The distribution is not perfectly symmetric.

### Q5. Does the beauty score differ by gender?

| Gender | Mean beauty score |
|---|---|
| Female | 0.12 |
| Male | -0.08 |

Female instructors have a slightly higher average beauty score, a difference of about 0.20 on the standardized scale. The standard deviations are similar for the two groups, so the difference is mainly in the average level, not the spread.

### Q6. Does the proportion with tenure differ by gender?

| Gender | % with tenure |
|---|---|
| Female | 74.36% |
| Male | 80.60% |

A higher percentage of male instructors have tenure than female instructors in this sample.

## Conclusion
- The data is cross-sectional.
- Class size (`students`) is strongly right-skewed.
- Female instructors have a slightly higher average beauty score, and male instructors have a higher tenure rate in this sample.

## Limitations
These are descriptive comparisons only. No statistical test was run, so the gender differences may or may not be statistically significant, and they do not show cause and effect. The beauty score is also a rating assigned by others, not an objective measure.
