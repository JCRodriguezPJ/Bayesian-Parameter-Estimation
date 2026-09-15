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
└── .gitignore