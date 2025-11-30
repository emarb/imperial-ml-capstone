# Imperial ML Capstone
This is part of the capstone project for the Professional Certificate in Machine Learning and AI from Imperial College Business School.

The project has been set up in a way that real-world conditions are simulated. Results can only be submitted once a week, and the results are back in a few days. This means that any brute-force strategy is out of the question and we are given enough time to reflect on an approach for the following week. There is a total of 13 attempts in 13 weeks.

## Black‑Box Optimization Goal
The goal of this project is the optimization of **8 black-box functions**. For each function, 10 initial data points are provided, and each week I must submit a new point. This simulates expensive, slow evaluations.

All variables range from 0 to 1 and vary from 2‑dimensional to 8‑dimensional.

In a **black-box optimization** problem, you have a function:

```
f(x): R^d → R
```

that you can **evaluate** (possibly at high cost), but:

- You don’t know its analytic form  
- You can’t compute gradients  
- Each evaluation is expensive or noisy  

Goal:

```
x* = argmin_x f(x)
```

We treat `f(x)` as a **true black box**.

## Tools and Libraries Used
- **NumPy**: vectorised numerical operations  
- **Scikit‑learn**: Gaussian Processes, SVMs, kernels, scaling  
- **SciPy**: optimization routines, distances, statistics  
- **TensorFlow / Keras**: neural-network surrogate experiments  
- **Pandas**: storing evolving results in a `results_df` dataframe  
- **Jupyter Notebooks**: chronological workflow documentation  

(Trade-offs and limitations described in the original text are preserved.)

## Files and Reproducibility

### Inputs
Initial challenge data is in the `initial_data/` folder.

### Outputs
Weekly platform results (`inputs.txt`, `outputs.txt`) are stored in `submissions/`.

### Reproducing the Work
Re-run the notebook with all data downloaded, ensuring sequential execution since sampling is simulated week by week.

## Results Overview (Week 6)

| Function | Baseline Best | Improved Value | % Improvement | Samples Improved |
|----------|---------------|----------------|---------------|------------------|
| 1 | 7.710875114502849e-16 | 2.6752879910742468e-09 | +347,031,616.55% | 1 |
| 2 | 0.6112052157614438 | 0.6669887774564723 | +9.13% | 1 |
| 3 | -0.034835313350078584 | -0.0014942495830570148 | +95.71% | 1 |
| 4 | -4.025542281908162 | 0.6230693654973547 | +115.48% | 2 |
| 5 | 1088.8596181962705 | 3997.541487950317 | +267.13% | 2 |
| 6 | -0.7142649478202404 | -0.4072033805462628 | +42.98% | 1 |
| 7 | 1.3649683044991994 | 1.5999115378376856 | +17.21% | 2 |
| 8 | 9.598482002566342 | 9.9383263498539 | +3.54% | 3 |

### Methodology Note
On week 6, I revisited previous results and adopted an iterative strategy of repeating whichever technique produced the most recent improvement.

## Functions Overview
More details of boundaries, plots and structure are in the notebook.

### Function 1 (2D → 1D)
Contamination-source detection in 2D space; only proximity produces nonzero readings. Bayesian optimisation used to detect weak and strong signals.

### Function 2 (2D → 1D)
Noisy log-likelihood surface with local optima. Bayesian optimisation used to explore vs exploit under uncertainty.

### Function 3 (3D → 1D)
Drug‑compound triad experiment; objective is minimisation of side effects (maximisation of a transformed output).

### Function 4 (4D → 1D)
Hyperparameter optimisation for a costly warehouse‑allocation simulator. Objective: approximate expensive baseline reliably.

### Function 5 (4D → 1D)
Unimodal chemical‑process yield optimisation; single global peak.

### Function 6 (5D → 1D)
Cake‑recipe optimisation with five ingredients; negative scoring system, reframed as maximisation.

### Function 7 (6D → 1D)
Hyperparameter optimisation of a common ML model. Literature‑informed search can help.

### Function 8 (8D → 1D)
High‑dimensional ML surrogate optimisation (e.g., 8 hyperparameters). Local maxima may be the practical target.

## Visualisations (Placeholder)
_To be added: plots, 2D/3D projections, convergence curves, acquisition functions._