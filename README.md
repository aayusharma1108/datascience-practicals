# Statistics and Machine Learning Practicals

A collection of 12 practicals covering data analysis, statistical testing, regression, machine learning and Bayesian sampling methods in Python. Each practical has its own folder with a notebook, its dataset (where needed) and a README with the aim, method, results and conclusion.

**Author:** Aayu, B.Tech CSE (Data Science)

## Contents

| # | Practical | Topics | Dataset |
|---|---|---|---|
| 01 | [Revisiting Pandas and NumPy](./practical-01-pandas-numpy) | DataFrames, NumPy arrays, matrix operations | Student marks (created in code) |
| 02 | [Descriptive Statistics](./practical-02-descriptive-statistics) | Cross-sectional data, summary statistics, histograms, group comparisons | TeachingRatings |
| 03 | [Exploring Tenure, Age and Evaluations](./practical-03-exploring-teaching-ratings) | Group percentages, histograms, bar charts, medians | TeachingRatings |
| 04 | [Understanding Data with Graphs](./practical-04-graphs) | Duplicate rows, mean and standard deviation, scatter plots | TeachingRatings |
| 05 | [Two-Tailed Test](./practical-05-two-tailed-test) | Normal probabilities, Z-scores, p-values, one-sample Z-test | TeachingRatings |
| 06 | [T-Test, ANOVA, Chi-Square](./practical-06-hypothesis-tests) | Welch t-test, one-way ANOVA, chi-square, Pearson correlation | TeachingRatings |
| 07 | [Regression with T-Test and ANOVA](./practical-07-regression) | OLS regression, coefficients, R-squared, ANOVA table | TeachingRatings |
| 08 | [Decision Trees and Max Depth](./practical-08-decision-trees) | Entropy, Gini, information gain, overfitting | Pima Indians Diabetes |
| 09 | [K-Nearest Neighbors](./practical-09-knn) | Feature scaling, confusion matrix, choosing K, PCA plot | Iris |
| 10 | [Principal Component Analysis](./practical-10-pca) | Standardization, covariance, explained variance | Wine |
| 11 | [Monte Carlo and MCMC](./practical-11-mcmc-sunspots) | Gamma fit, Metropolis-Hastings, credible intervals | SILSO sunspot numbers |
| 12 | [Metropolis Algorithm and Deterministic Model](./practical-12-metropolis-deterministic) | MCMC sampling, exponential growth model | Generated in code |

## Key Findings

- **Teaching ratings (practicals 2 to 7):** evaluation scores differ significantly by gender (male instructors about 0.17 points higher) and correlate weakly with beauty score (r ≈ 0.19). Age, tenure and course division show little or no strong relationship. These effects are statistically significant but small, with R² below 4%.
- **Decision trees (08):** a shallow tree (depth 4) reached 80.5% test accuracy, while a very deep tree (depth 20) reached only 70.1%, which shows overfitting.
- **KNN (09):** 93.3% accuracy at K = 5 and 96.7% at K = 1 on the Iris test set. Only versicolor and virginica were confused.
- **PCA (10):** three components keep roughly two-thirds of the variance in the 13 Wine features while still separating the wine classes.
- **MCMC (11):** Metropolis-Hastings estimated the Gamma parameters for the sunspot counts as a ≈ 1.17 and b ≈ 71.7, in agreement with maximum likelihood.
- **Metropolis (12):** 10,000 samples reproduced a standard normal distribution (mean 0.055, variance 1.000).

## Skills Covered

- **Data handling:** pandas, NumPy, cleaning and grouping data
- **Visualization:** Matplotlib and Seaborn (histograms, box plots, scatter plots, heatmaps, trace plots, 3D plots)
- **Statistics:** probability, Z-test, t-test, ANOVA, chi-square, correlation, regression
- **Machine learning (scikit-learn):** decision trees, KNN, PCA, train/test splitting, scaling, evaluation metrics
- **Bayesian and simulation methods:** Monte Carlo simulation, Metropolis and Metropolis-Hastings MCMC

## Tools and Libraries

Python 3, pandas, NumPy, SciPy, statsmodels, scikit-learn, Matplotlib, Seaborn, Google Colab

## How to Run

1. Open a notebook in [Google Colab](https://colab.research.google.com/) (File → Open notebook → GitHub), or download it and run it with Jupyter.
2. Practicals that read a CSV file (such as the diabetes data) expect the file to be in the same folder as the notebook. Upload it to your Colab session first.
3. To run locally:
   ```bash
   pip install pandas numpy scipy statsmodels scikit-learn matplotlib seaborn jupyter
   jupyter notebook
   ```

## Repository Structure

```
.
├── README.md
├── practical-01-pandas-numpy/
├── practical-02-descriptive-statistics/
├── ...
└── practical-12-metropolis-deterministic/
```

Each practical folder contains the notebook (`.ipynb`), any dataset it needs, and its own `README.md`.

## Data Sources

- **TeachingRatings:** `AER` R package, via [Rdatasets](https://vincentarelbundock.github.io/Rdatasets/)
- **Pima Indians Diabetes:** UCI / Kaggle
- **Iris and Wine:** built into scikit-learn (`load_iris`, `load_wine`)
- **Sunspot numbers:** [SILSO](https://www.sidc.be/SILSO/), Royal Observatory of Belgium
