# Bayesian Parameter Estimation from Homodyne Measurements

This repository contains a practical study of Bayesian parameter estimation
(BPE) for continuous-variable quantum states using homodyne quadrature
measurements.

The project considers both Gaussian and non-Gaussian optical states and studies
how posterior estimates and their uncertainties evolve as the number of
homodyne measurements increases.

The purpose of this repository is not to introduce a new Bayesian estimation
method, but to document a reproducible implementation of Bayesian parameter
estimation for representative quantum-optical models.

---

## Report

A technical report accompanying this repository is available here:

[Bayesian Parameter Estimation Report](Bayesian_Parameter_Estimation_Report.pdf)

> **Status:** Work in progress. The PDF will be updated as the report is completed.

---

## Case Studies

Four cases are considered:

1. **Simulated squeezed-thermal state**
2. **Experimental squeezed-thermal state**
3. **Simulated non-Gaussian vacuum-single-photon state**
4. **Experimental non-Gaussian single-photon state**

The repository is organized as

```text
Bayesian-Parameter-Estimation/
├── 01_simulated_squeezed_thermal/
├── 02_experimental_squeezed_thermal/
├── 03_simulated_non_gaussian/
├── 04_experimental_non_gaussian/
├── Bayesian_Parameter_Estimation_Report.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

Each case-study folder contains the corresponding Jupyter notebook together
with the figures generated during the analysis.

---

## Bayesian Parameter Estimation

For a homodyne dataset

$$
D=\{(x_i,\theta_i)\}_{i=1}^{N},
$$

and a parametrized quantum state $\rho(\mathbf{s})$, the probability density
for an individual homodyne measurement is

$$
p(x_i|\theta_i,\mathbf{s})
=
\mathrm{Tr}
\left[
\Pi(x_i,\theta_i)\rho(\mathbf{s})
\right].
$$

Assuming independent measurements, the total log-likelihood is

$$
\log L(\mathbf{s})
=
\sum_{i=1}^{N}
\log p(x_i|\theta_i,\mathbf{s}).
$$

Bayes' theorem gives

$$
p(\mathbf{s}|D)
=
\frac{
p(D|\mathbf{s})p(\mathbf{s})
}{
p(D)
},
$$

and therefore

$$
p(\mathbf{s}|D)
\propto
p(D|\mathbf{s})p(\mathbf{s}).
$$

Posterior distributions are sampled numerically using Markov-chain Monte Carlo
(MCMC) with `emcee`.

---

## Gaussian Model: Squeezed-Thermal State

The Gaussian state is modeled as

$$
\rho_{\mathrm{sq-th}}(\mathbf{s})
=
S(r,\phi)\,
\rho_{\mathrm{th}}(n_{\mathrm{th}})
S^\dagger(r,\phi),
$$

with

$$
\mathbf{s}
=
(r_{\mathrm{dB}},\phi,n_{\mathrm{th}}).
$$

The inferred quantities are:

- squeezing strength $r_{\mathrm{dB}}$,
- squeezing angle $\phi$,
- thermal occupation $n_{\mathrm{th}}$.

Both simulated and experimental homodyne datasets are analyzed.

For the simulated case, the inferred posterior can be compared directly with
the known ground-truth parameters. For the experimental case, the analysis
focuses on stabilization of the inferred parameters and contraction of the
posterior uncertainty as the amount of data increases.

---

## Non-Gaussian Model: Noisy Single-Photon State

The non-Gaussian state is modeled as a vacuum-single-photon mixture,

$$
\rho(c)
=
c|0\rangle\langle0|
+
(1-c)|1\rangle\langle1|,
$$

with

$$
0\leq c\leq1.
$$

The Bayesian inference determines the posterior distribution of the mixing
parameter $c$.

The simulated dataset provides a controlled example with known ground truth,
while the experimental dataset is used to study the effective parameter
inferred from measured single-photon homodyne data.

---

## Posterior Uncertainty

Posterior estimates are summarized using the 16th, 50th, and 84th percentiles.

The width of the central 68% credible interval is

$$
\Delta_{68}=q_{84}-q_{16}.
$$

Its dependence on the number of measurements is compared with the reference
statistical scaling

$$
\Delta_{68}\propto N^{-1/2}.
$$

For simulated datasets, convergence toward known ground-truth parameters can
be studied directly.

For experimental datasets, where no independently known true parameters are
available, the main quantities of interest are posterior stabilization and
uncertainty contraction.

---

## Repository Contents

### `01_simulated_squeezed_thermal`

Bayesian parameter estimation of a simulated squeezed-thermal state.

Main outputs include:

- simulated homodyne quadrature sequence,
- marginalized posterior distributions,
- joint posterior distributions,
- parameter correlations,
- posterior convergence with increasing $N$,
- credible-interval contraction,
- posterior-convergence GIF.

### `02_experimental_squeezed_thermal`

Application of the squeezed-thermal model to experimental homodyne data.

Main outputs include:

- experimental quadrature sequence,
- posterior distributions for $r_{\mathrm{dB}}$, $\phi$, and $n_{\mathrm{th}}$,
- parameter correlations,
- stabilization with increasing dataset size,
- credible-interval contraction,
- posterior-convergence GIF.

### `03_simulated_non_gaussian`

Bayesian estimation of the parameter $c$ for a simulated
vacuum-single-photon mixture.

Main outputs include:

- simulated homodyne quadrature sequence,
- non-Gaussian marginal quadrature distribution,
- posterior distribution of $c$,
- convergence toward the known ground truth,
- posterior contraction,
- posterior-convergence GIF.

### `04_experimental_non_gaussian`

Application of the vacuum-single-photon model to experimental non-Gaussian
homodyne data.

Main outputs include:

- experimental quadrature sequence,
- measured non-Gaussian marginal distribution,
- posterior distribution of $c$,
- stabilization with increasing dataset size,
- credible-interval contraction,
- posterior-convergence GIF.

The inferred posterior should be interpreted conditional on the assumed model.
A narrow posterior indicates precise inference of $c$ within that model, but
does not by itself demonstrate that the model provides a complete physical
description of the experimental state.

---

## Requirements

The Python dependencies and package versions used for this project are listed
in [`requirements.txt`](requirements.txt).

The main versions used are:

```text
numpy==2.2.4
scipy==1.15.2
matplotlib==3.8.4
torch==2.5.1
emcee==3.1.6
corner==2.2.3
pillow==11.1.0
```

Install them with

```bash
python -m pip install -r requirements.txt
```

---

## Running the Project

Clone the repository:

```bash
git clone https://github.com/JCRodriguezPJ/Bayesian-Parameter-Estimation.git
cd Bayesian-Parameter-Estimation
```

Install the dependencies:

```bash
python -m pip install -r requirements.txt
```

Then open any of the Jupyter notebooks inside the four case-study directories.

Each notebook follows the general workflow:

```text
data preparation
      ↓
likelihood definition
      ↓
Bayesian posterior
      ↓
MCMC sampling
      ↓
posterior analysis
      ↓
figures and convergence study
```

---

## Experimental Data

The experimental case-study folders contain the data required by their
corresponding notebooks.

The experimental results should be interpreted as parameter estimates
conditional on the chosen physical model. Experimental imperfections,
calibration uncertainty, noise, and model mismatch may produce deviations from
the idealized models used in the inference.

---

## Notes

The animated GIFs illustrate how the posterior distributions evolve as the
number of homodyne measurements increases.

Intermediate image frames used to generate the animations are excluded from
the repository through `.gitignore`.

---

## Purpose of This Repository

This repository is intended as a compact and reproducible study of Bayesian
parameter estimation for continuous-variable quantum optical states.

The main focus is on:

- direct inference of physically meaningful state parameters,
- posterior uncertainty quantification,
- correlations between inferred parameters,
- convergence with increasing measurement number,
- comparison between simulated and experimental data,
- practical implementation using MCMC.