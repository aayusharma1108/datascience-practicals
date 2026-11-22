# Practical 12: Metropolis Algorithm and Deterministic Model

This practical has two parts:
- **Part A:** the Metropolis algorithm (MCMC) used to sample from a standard normal distribution
- **Part B:** a deterministic exponential population growth model

## Tools Used
Python, NumPy, pandas, Matplotlib, Seaborn (Google Colab)

---

## Part A: Metropolis Algorithm

### Aim
To implement the Metropolis algorithm to generate samples from a probability distribution using Markov Chain Monte Carlo (MCMC).

### Theory
The Metropolis algorithm generates samples from a distribution that is hard to sample directly. It only needs the target density up to a constant. The steps are:

1. Start at an initial value.
2. Propose a new value from a symmetric distribution centred on the current value (here, a normal proposal).
3. Compute the acceptance probability: `min(1, p(proposed) / p(current))`.
4. Accept the proposal with that probability. Otherwise keep the current value.
5. Repeat to build a chain of samples.

**Target distribution:** standard normal, p(x) ∝ exp(-x²/2). The acceptance ratio in the code is therefore `exp(-0.5 * (proposed² - current²))`.

### Settings

| Setting | Value |
|---|---|
| Samples | 10,000 |
| Initial value | 0 |
| Proposal standard deviation | 1 |
| Random seed | 42 |

### Results

| Statistic | Metropolis samples | True N(0, 1) value |
|---|---|---|
| Mean | 0.055 | 0 |
| Variance | 1.000 | 1 |
| Standard deviation | 1.000 | 1 |
| Acceptance rate | 0.712 | (not applicable) |

- The **trace plot** shows the chain moving around zero without drifting, which suggests it is exploring the distribution.
- The **histogram** of the samples closely follows the standard normal density curve.
- The sample mean and variance are close to the true values, so the algorithm recovers the target distribution.

### Conclusion
The Metropolis algorithm generated samples that match a standard normal distribution, using only accept/reject decisions on random proposals.

### Notes
- **MCMC samples are correlated.** Each sample depends on the previous one, so 10,000 samples carry less information than 10,000 independent draws. Rejected proposals repeat the same value (visible in the first 10 samples), and the mean error is larger than for independent sampling.
- **The acceptance rate of 71% is high**, which means the steps are small relative to the target. For a one-dimensional normal target, a rate around 40 to 45% is more efficient, which a larger proposal standard deviation (about 2 to 3) would give.
- **No burn-in was removed.** This is acceptable here because the chain starts at 0, in the middle of the distribution. Starting from a far-off value would need a burn-in period.

---

## Part B: Deterministic Model

### Aim
To implement a deterministic population growth model and visualize how the population changes over time.

### Theory
A deterministic model has no randomness: the same initial conditions and parameters always give the same output. This practical uses **continuous exponential growth**:

**N(t) = N₀ · e^(r·t)**

| Symbol | Meaning | Value |
|---|---|---|
| N₀ | initial population | 100 |
| r | growth rate | 0.05 (5%) |
| t | time | 0 to 50 |

### Results

| Time | Population |
|---|---|
| 0 | 100.00 |
| 10 | 164.87 |
| 20 | 271.83 |
| 30 | 448.17 |
| 40 | 738.91 |
| 50 | 1218.25 |

The population grows steadily at a constant relative rate and ends at about 1,218 after 50 time units, more than 12 times the starting value. The curve is smooth and upward bending because each increase is proportional to the current population.

### Conclusion
The deterministic model gives completely predictable results when the initial population and growth rate are fixed.

### Notes
- **5% here is a continuous rate**, so the effective growth per time unit is e^0.05 - 1 ≈ 5.13%. Growing exactly 5% per period, N₀(1.05)^t, would give about 1,147 at t = 50 instead of 1,218.
- **The model assumes unlimited resources.** The population grows without bound. A logistic model, which levels off at a carrying capacity, is more realistic for long time spans.
- **There is no randomness.** A stochastic version, where growth varies randomly, would show the range of possible outcomes instead of a single curve. This links back to Part A, since MCMC is a stochastic method.
