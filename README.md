# Anscombe's Quartet — Data Analysis

A hands-on exploration of Anscombe's Quartet using Python, demonstrating why visualising data is essential before drawing statistical conclusions.

---

## Overview

Anscombe's Quartet is a classic dataset constructed by statistician Francis Anscombe in 1973. It consists of four subsets (I, II, III, IV), each containing 11 (x, y) data points. The subsets share nearly identical descriptive statistics — mean, variance, correlation, and linear regression coefficients — yet each tells a completely different story when plotted.

This project loads, summarises, and visualises all four datasets to make that point concrete.

---

## Repository Contents

| File | Description |
|------|-------------|
| `anscombe_quartet.tsv` | Raw data — 44 rows with columns `dataset`, `x`, `y` |
| `anscombe_analysis.ipynb` | Jupyter notebook containing all analysis and plots |
| `anscombe_plots.png` | 2×2 scatter plot grid with regression lines |
| `anscombe_residuals.png` | 2×2 residual plot grid |
| `PLAN.md` | Original project plan and plot proposal |

---

## What Was Done

### 1. Descriptive Statistics

The notebook begins by loading the TSV file and computing per-dataset summary statistics: mean and variance of both x and y, and sample size. The result confirms Anscombe's design — all four datasets are statistically indistinguishable at a glance:

| Dataset | x mean | x var | y mean | y var | n |
|---------|--------|-------|--------|-------|---|
| I | 9.0 | 11.0 | 7.50 | 4.13 | 11 |
| II | 9.0 | 11.0 | 7.50 | 4.13 | 11 |
| III | 9.0 | 11.0 | 7.50 | 4.12 | 11 |
| IV | 9.0 | 11.0 | 7.50 | 4.12 | 11 |

### 2. Linear Regression

OLS regression was fitted to each dataset using `scipy.stats.linregress`. Again, the results are virtually identical across all four:

| Dataset | Slope | Intercept | r | r² | p-value |
|---------|-------|-----------|---|----|---------|
| I | 0.500 | 3.000 | 0.816 | 0.667 | 0.0022 |
| II | 0.500 | 3.001 | 0.816 | 0.666 | 0.0022 |
| III | 0.500 | 3.002 | 0.816 | 0.666 | 0.0022 |
| IV | 0.500 | 3.002 | 0.817 | 0.667 | 0.0022 |

---

## Plots

### Plot 1 — Scatter Plots with Regression Lines (`anscombe_plots.png`)

![Anscombe's Quartet scatter plots](anscombe_plots.png)

A 2×2 grid of scatter plots, one panel per dataset. Each panel shows the raw data points overlaid with the fitted OLS regression line (dashed black), annotated with the regression equation and Pearson r value.

**What each panel reveals:**

- **Dataset I (blue):** The reference case. Points scatter reasonably around the regression line with no obvious pattern in the residuals. A linear model is appropriate here.

- **Dataset II (green):** The relationship is clearly curved — a smooth arc through the points. A straight line is a poor summary; a quadratic term would fit far better. The statistics alone give no hint of this curvature.

- **Dataset III (orange):** The underlying relationship is actually more linear than Dataset I, but a single high-leverage outlier near (13, 12.7) pulls the regression line away from the majority of points. Remove that one observation and the fit is near-perfect.

- **Dataset IV (pink/magenta):** Nearly all x-values are identical (x = 8), making the x-variable almost degenerate. The apparent correlation and positive slope are driven entirely by one isolated point at x = 19. Without that outlier there is no linear relationship at all.

---

### Plot 2 — Residual Plots (`anscombe_residuals.png`)

![Residual plots](anscombe_residuals.png)

A 2×2 grid of residual plots (y − ŷ vs. fitted values), one panel per dataset. A horizontal line at residual = 0 marks the ideal. Well-behaved residuals should scatter randomly around this line with no discernible structure.

**What each panel reveals:**

- **Dataset I (blue):** Residuals are scattered roughly symmetrically around zero across the range of fitted values. No systematic pattern is visible. This confirms the linear model is appropriate.

- **Dataset II (green):** A clear U-shaped (parabolic) curve is visible in the residuals — negative at both ends, positive in the middle. This systematic pattern is the diagnostic signature of a missing quadratic term. The linear model consistently under-predicts at low and high fitted values and over-predicts in the middle.

- **Dataset III (orange):** Ten of the eleven points produce residuals that drift steadily from positive to negative as fitted values increase — a downward trend that indicates the regression slope is being inflated by the single outlier. That outlier itself appears as an isolated point with a large positive residual (~3.2) near fitted value = 10.

- **Dataset IV (pink/magenta):** All points stack vertically at fitted value ≈ 7 (corresponding to x = 8), with residuals spread across a wide range. The lone outlier at x = 19 sits exactly on the regression line (residual ≈ 0) because it anchors the line. This plot exposes the degenerate x-distribution that the scatter plot makes obvious but the summary stats completely hide.

---

## Key Takeaway

All four datasets share the same slope, intercept, correlation, and p-value to two or three decimal places. Yet they represent four fundamentally different data-generating processes:

| Dataset | Story |
|---------|-------|
| **I** | Well-behaved linear relationship — the textbook case |
| **II** | Curved (quadratic) relationship; a linear model is a poor fit |
| **III** | Linear with one high-leverage outlier distorting the line |
| **IV** | Near-constant x with one remote point driving all apparent correlation |

**Summary statistics alone are insufficient to characterise a dataset. Always visualise your data.**

---

## Requirements

```
pandas
numpy
matplotlib
scipy
```

Install with:

```bash
pip install pandas numpy matplotlib scipy
```

---

## Running the Analysis

Open the notebook and run all cells:

```bash
jupyter notebook anscombe_analysis.ipynb
```

The two PNG files will be (re)generated in the project directory.
