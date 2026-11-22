# Practical 5: Understanding the Two-Tailed Test

## Aim
To understand probability and perform a two-tailed Z-test using Python.

## Objectives
- Calculate the probability of evaluation scores greater than a given value
- Calculate the probability of evaluation scores within a specified range
- Understand null and alternative hypotheses
- Calculate the Z-score and p-value
- Interpret the results of a two-tailed hypothesis test

## Dataset
- **Source:** https://vincentarelbundock.github.io/Rdatasets/csv/AER/TeachingRatings.csv (from the `AER` R package)
- **Size:** 463 observations, 13 columns
- **Variable used:** `eval` (instructor teaching evaluation score)

## Tools Used
Python, pandas, NumPy, SciPy (`scipy.stats.norm`), Matplotlib (Google Colab)

## Part 1: Probabilities from the Normal Distribution

Evaluation scores were assumed to be approximately normally distributed, using the sample statistics as the parameters.

| Statistic | Value |
|---|---|
| Mean of `eval` | 3.998 |
| Standard deviation | 0.555 |

Each value was converted to a z-score with `z = (x - mean) / std`, and probabilities were found with the normal CDF.

| Question | z-score(s) | Probability |
|---|---|---|
| P(score > 4.5) | 0.904 | 0.1829 (18.29%) |
| P(3.5 < score < 4.2) | -0.898 and 0.364 | 0.4573 (45.73%) |

## Part 2: Two-Tailed One-Sample Z-Test

**Problem:** A regional basketball league has a historical mean score of 12 points. A sample of 36 players has a mean of 10.7 points. The population standard deviation is 5.5, and the significance level is α = 0.05.

**Hypotheses**
- H₀: μ = 12 (the regional mean is not different from the historical mean)
- H₁: μ ≠ 12 (the regional mean is different from the historical mean)

**Calculations**

| Quantity | Formula | Value |
|---|---|---|
| Standard error | σ / √n | 0.917 |
| Z-statistic | (x̄ - μ) / SE | -1.418 |
| P-value (two-tailed) | 2 × (1 - Φ(\|z\|)) | 0.156 |
| Critical values (α = 0.05) | ±z₀.₉₇₅ | ±1.960 |

## Interpretation
Since |z| = 1.418 is less than 1.960, and the p-value (0.156) is greater than α (0.05), we **fail to reject H₀**.

The sample mean of 10.7 is lower than 12, but the difference is not statistically significant at the 5% level. There is not enough evidence that the regional players' mean score differs from the historical mean of 12 points.

## Conclusion
Normal-distribution probabilities were computed for the evaluation scores, and a two-tailed Z-test was carried out. The test did not give sufficient evidence to reject the null hypothesis.

## Assumptions and Limitations
- The evaluation scores were assumed to be normal. The real distribution may be skewed, so the Part 1 probabilities are approximate.
- The Z-test assumes the population standard deviation is known.
- Failing to reject H₀ does not prove it is true. It means the sample gave insufficient evidence against it.
