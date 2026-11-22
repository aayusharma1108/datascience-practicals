# Practical 11: Monte Carlo and MCMC on Sunspot Data

## Aim
To study monthly sunspot activity using Monte Carlo simulation and Markov Chain Monte Carlo (the Metropolis-Hastings algorithm), and to estimate the parameters of a Gamma distribution fitted to the data.

## Objectives
- Load and visualize the monthly sunspot time series (1749 to 2018)
- Model the positive sunspot counts with a Gamma distribution
- Run a Monte Carlo simulation from a Gamma distribution with a = 4 and b = 10
- Implement the Metropolis-Hastings algorithm to estimate the Gamma shape (a) and scale (b)
- Interpret trace plots and histograms, and remove burn-in samples
- Report parameter estimates with 95% credible intervals

## Dataset
- **Source:** SILSO monthly mean total sunspot number, version 2.0 (https://www.sidc.be/SILSO/DATA/SN_m_tot_V2.0.csv)
- **Period used:** January 1749 to November 2018
- **Size:** 3,239 monthly observations
- **Variable used:** `Sunspot` (monthly mean total sunspot number)

## Tools Used
Python, NumPy, pandas, Matplotlib, SciPy (`scipy.stats.gamma`) (Google Colab)

## Key Concepts
- **Gamma distribution:** a right-skewed distribution for positive values, with shape *a* and scale *b*. Its mean is *a·b* and its variance is *a·b²*.
- **Monte Carlo simulation:** generating many random samples from a known distribution to study its behaviour.
- **MCMC (Metropolis-Hastings):** a way to sample from a posterior distribution. A new parameter value is proposed and accepted with probability min(1, posterior ratio). Otherwise the chain stays where it is.
- **Burn-in:** the first part of the chain, discarded because it still reflects the starting values.
- **Credible interval:** the range that contains 95% of the posterior probability for a parameter.

## Procedure and Results

### 1. Sunspot time series
The monthly series shows repeating rises and falls, which are the solar activity cycles (roughly 11 years long).

### 2. Gamma fit to the data
The 12-year cycle index was computed (23 blocks). Months with a positive sunspot count were then used, because the Gamma distribution is defined only for positive values. A Gamma distribution was fitted by maximum likelihood with `gamma.fit(sunspots, floc=0)`.

| Parameter | Maximum likelihood estimate |
|---|---|
| Shape (a) | 1.174 |
| Scale (b) | 71.64 |

A density histogram with the fitted Gamma curve overlaid shows how well the model matches the data.

### 3. Monte Carlo simulation (a = 4, b = 10)
1,000 samples were drawn with `np.random.gamma` (seed 42). The theoretical mean is a·b = 40 and the theoretical standard deviation is √(a·b²) = 20. Three histograms with the theoretical density were compared: the first 50 samples, all 1,000 samples and the last 50 samples. The 50-sample histograms are noisy, while the 1,000-sample histogram follows the theoretical curve closely, which illustrates that Monte Carlo estimates improve with more samples.

### 4. Metropolis-Hastings MCMC

| Setting | Value |
|---|---|
| Starting values | a = 4, b = 10 |
| Iterations | 10,000 |
| Burn-in discarded | 2,000 |
| Samples kept | 8,000 |
| Proposal | random walk on log(a) and log(b), standard deviation 0.08 |
| Priors | weak exponential, log prior = -0.01a - 0.001b |
| Acceptance rate | 0.0955 (about 9.6%) |

Proposals were made in log space, so a and b always stay positive. The Jacobian terms (log a and log b) are added to the log posterior to correct for this change of variable.

### 5. Trace plots and histograms
The trace plots show how a and b move during sampling, and the histograms show their posterior distributions after burn-in.

### 6. Final estimates (after burn-in)

| Parameter | Posterior mean | Median | 95% credible interval |
|---|---|---|---|
| a (shape) | 1.174 | 1.175 | [1.123, 1.223] |
| b (scale) | 71.71 | 71.72 | [68.16, 75.89] |

The MCMC estimates agree closely with the maximum likelihood fit (a = 1.174, b = 71.64). This is expected, because the priors are weak and the dataset is large. The implied mean of the fitted distribution is a·b ≈ 84 sunspots per month.

## Conclusion
The positive monthly sunspot counts were modelled with a Gamma distribution. A Monte Carlo simulation showed how sample size affects how closely samples match the true distribution. The Metropolis-Hastings algorithm then estimated the Gamma parameters, starting far from the true values (a = 4, b = 10) and converging to a ≈ 1.17 and b ≈ 71.7. After removing burn-in, the posterior means and 95% credible intervals were computed.

## Limitations and Notes
- **Independence assumption.** The Gamma likelihood treats the 3,239 months as independent, but the sunspot series is a strongly autocorrelated cycle. The real uncertainty is larger than the narrow credible intervals suggest, and a time-series model would be needed to capture the cycle.
- **Zeros are excluded.** Months with a sunspot count of 0 (common near solar minima) were removed, and the Gamma model cannot represent them. The number of excluded months was not reported.
- **The 12-year blocks are approximate.** Solar cycles vary between roughly 9 and 14 years, and the cycle index was computed but not used in the fit.
- **Acceptance rate.** About 9.6% is on the low side (a common target for two parameters is roughly 20 to 40%), so the chain moves in fairly large steps and many proposals are rejected. a and b are also strongly negatively correlated, which makes independent proposals less efficient. A smaller step size would improve mixing.
- **Convergence checks.** Convergence was judged only from trace plots. Autocorrelation plots, effective sample size, or several chains started at different values (the Gelman-Rubin statistic) would be stronger evidence.
- Results use a single random seed (42).
