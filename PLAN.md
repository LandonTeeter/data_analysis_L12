# An analysis of Anscombe data

## Goal

Analyze data set and visualize it, and see what we want to do with ut

## Implementations

-First look at the data and generate descriptive stats
-Data is in anscombe_quartet.tsv
-Second create a Jupyter Light notebook in which you will generate plots
-Third, Propose the types of plots youd like to genrate
-Fourth, Save this proposal to the end of this file and let me look at it
-Approval of plan before we go ahead with it

---

## Plot Proposal (Step 4)

### Plots to generate in `anscombe_analysis.ipynb`

**1. 2×2 Scatter Plot Grid with Regression Lines**
- One panel per dataset (I, II, III, IV)
- Each panel shows raw data points + OLS regression line
- Annotated with equation and Pearson r
- Purpose: the core Anscombe illustration — identical stats, wildly different shapes

**2. 2×2 Residual Plot Grid**
- Residuals (y − ŷ) vs. fitted values for each dataset
- Horizontal zero line for reference
- Purpose: exposes non-linearity (II), outlier leverage (III), and degenerate x-distribution (IV) that the summary stats hide

### Why these two plot types?
The scatter plots show the raw relationship; the residual plots reveal *why* a single linear model fails for datasets II–IV. Together they make the strongest possible case for the Anscombe message: **always visualise your data**.