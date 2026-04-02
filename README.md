# Quantitative Analysis — Investa Insights UBC

**Role:** Junior Quantitative Analyst  
**Context:** Quantitative research and modelling produced to support equity and LBO pitch competitions at Investa Insights UBC. Each notebook was built to give a specific investment thesis a rigorous, data-driven backbone.

---

## Repository Overview

| Notebook | Thesis Supported | Core Methods |
|---|---|---|
| [`revenue_analysis.ipynb`](#1-triclip-revenue-analysis--monte-carlo--sensitivity) | Abbott (ABT) — TriClip structural heart device (Stock Pitch) | Monte Carlo simulation, OVAT sensitivity, competitive market share modelling |
| [`quality_factor_decomposition.ipynb`](#2-quality-factor-decomposition--dupont-analysis) | Abbott (ABT) — Vascular innovation driving outperformance (Stock Pitch) | DuPont decomposition, quality z-scores, hypothesis testing |
| [`pca.ipynb`](#3-pca--k-means-clustering--medical-device-sector) | Abbott (ABT) — Peer group positioning (Stock Pitch) | PCA, K-Means clustering, cluster stability analysis |
| [`credit_risk_analysis.ipynb`](#4-imax-lbo--credit-risk-analysis) | IMAX Corporation (LBO Pitch) | Merton model, Altman Z-Score, debt capacity, covenant stress testing |

---

## 1. TriClip Revenue Analysis — Monte Carlo & Sensitivity

**File:** `revenue_analysis.ipynb`  
**Thesis:** Abbott's TriClip device holds a structurally advantaged position in tricuspid regurgitation treatment with limited competitive alternatives, supporting a long equity case.

### What was built

Three interlocking models to answer the core investor questions on a single device:

**Monte Carlo Simulation (10,000 scenarios, 2021–2031)**
- Sampled six stochastic inputs (revenue per case, clips per case, market penetration, ASP decay, competitive share erosion) from calibrated distributions using `scipy.stats`
- Produced P10 / P50 / P90 revenue fan charts to bound the range of plausible outcomes
- Terminal year 2031 base case: $48,000 revenue per procedure

**Tornado / OVAT Sensitivity Analysis**
- One-variable-at-a-time sweeps across all key assumptions
- Ranked inputs by revenue impact magnitude to identify which assumptions the thesis lives or dies on

**Competitive Market Share Model**
- Modelled Abbott vs. Edwards Lifesciences (Evoque) vs. a hypothetical 2028 new entrant
- Quantified Abbott's share trajectory under competitive entry using logistic-curve dynamics
- Validated segment projections against total-company Bloomberg financials as a consistency check

**Data sources:** Bloomberg Terminal (monthly fundamentals) + Thesis II slide-deck assumptions  
**Output:** 6-panel publication-ready figure

### Skills demonstrated
`Monte Carlo simulation` · `scenario analysis` · `sensitivity analysis` · `market share modelling` · `scipy` · `numpy` · `matplotlib`

---

## 2. Quality Factor Decomposition — DuPont Analysis

**File:** `quality_factor_decomposition.ipynb`  
**Thesis:** Abbott's 2020 vascular innovation milestone produced measurable, statistically significant financial advantages over its medical device peers — providing quantitative support for the long thesis.

### What was built

**DuPont Decomposition**
- Decomposed ROE into Net Margin × Asset Turnover × Equity Multiplier for all 11 companies across 70 months of Bloomberg data
- Isolated exactly *where* Abbott's returns come from versus the peer group

**Composite Quality Z-Score**
- Normalised four fundamental metrics (Net Margin, Asset Turnover, ROA, ROE) into a single peer-relative composite score per company per period
- Produced a ranked leaderboard of the universe on quality

**Pre / Post-2020 Structural Break Analysis**
- Split the sample at Abbott's key innovation inflection point
- Measured the change in each company's quality score and DuPont components across the break

**Statistical Significance Testing**
- One-sample t-tests to confirm whether Abbott's outperformance is statistically meaningful (p < 0.05) or within noise
- Quantified the probability that observed improvements reflect a real structural shift

**Universe:** ABT, MDT, BSX, DXCM, TMO, BDX, EW, PODD, ITGR, MMSI, ZBH  
**Data:** Bloomberg Terminal monthly fundamentals (~70 months)

### Skills demonstrated
`DuPont decomposition` · `factor construction` · `z-score normalisation` · `hypothesis testing` · `t-tests` · `pandas` · `scipy.stats` · `seaborn`

---

## 3. PCA & K-Means Clustering — Medical Device Sector

**File:** `pca.ipynb`  
**Thesis:** Abbott occupies a structurally distinct peer cluster driven by latent quality factors that separate it from the broader medical device universe — validating the investment thesis using unsupervised learning.

### What was built

**Rolling Quarterly PCA**
- Ran StandardScaler + PCA independently on each quarter's cross-section of 11 companies × 8+ fundamental features
- Tracked explained variance per principal component over time
- Extracted the top feature loadings driving PC1 each quarter to identify what the latent "quality factor" actually measures

**Company PC1 Trajectory Analysis**
- Plotted each firm's principal component score quarter-by-quarter
- Identified which companies are trending toward or away from the high-quality cluster

**K-Means Clustering (k=3) on Latent Factor Space**
- Clustered companies in PC1/PC2 space rather than on raw metrics, removing the distortion of correlated fundamentals
- Produced peer groupings based on structural financial characteristics

**Cluster Stability & Migration Analysis**
- Computed each company's stability ratio: fraction of quarters it stayed in the same cluster
- Identified "migrators" — companies whose fundamental profile shifted over the sample
- Generated a full heatmap of cluster membership (companies × quarters)

**Animated Cluster Evolution**
- Produced an animated GIF showing company movement through PC1/PC2 space across all quarters

**Data:** Bloomberg Terminal quarterly fundamentals  
**Universe:** 11 medical device companies

### Skills demonstrated
`PCA` · `K-Means clustering` · `unsupervised learning` · `dimensionality reduction` · `sklearn` · `StandardScaler` · `time-series factor analysis` · `matplotlib.animation`

---

## 4. IMAX LBO — Credit Risk Analysis

**File:** `credit_risk_analysis.ipynb`  
**Thesis:** Quantitative stress-testing of IMAX Corporation's credit profile under a hypothetical leveraged buyout — identifying the leverage level at which risk-adjusted returns deteriorate and covenant headroom erodes.

### What was built

**Core Credit Metrics**
- Net Debt / EBITDA, Interest Coverage Ratio (EBITDA / Interest), and Altman Z-Score computed from live Yahoo Finance data
- Benchmarked against standard LBO financing thresholds (4–6× leverage, ≥ 2× ICR floor)

**Merton Structural Credit Model**
- Solved a system of non-linear equations (`scipy.optimize.fsolve`) for implied asset value and asset volatility using observed equity price, equity volatility, and balance sheet data
- Computed Distance-to-Default (DD) and 1-year Probability of Default (PD) from the structural model
- Quantified the market-implied credit risk embedded in IMAX's equity price

**Debt Capacity & Risk-Adjusted IRR**
- Swept leverage from 1× to 8× EBITDA and computed both nominal and risk-adjusted IRR at each level
- Identified the precise "risk cliff" — the leverage point at which the PD penalty overwhelms the equity return uplift

**Covenant Stress Testing**
- Modelled illustrative covenant headroom under base and stressed assumptions
- Stress scenario: simultaneous revenue shock + margin compression
- Flagged the conditions under which IMAX would breach a typical leverage covenant

**Joint Sensitivity Grids**
- Two-dimensional revenue × margin sensitivity tables for both Leverage and ICR
- Showed the full envelope of outcomes, not just point estimates

**Data:** Live Yahoo Finance (`yfinance`); self-contained, runs on current financials  
**Output:** Four-panel dashboard (credit metrics, Merton PD curve, debt capacity, covenant headroom)

### Skills demonstrated
`Merton model` · `structural credit modelling` · `Altman Z-Score` · `LBO analysis` · `covenant analysis` · `scipy.optimize` · `yfinance` · `sensitivity analysis` · `IRR modelling`

---

## Technical Stack

| Category | Tools |
|---|---|
| **Data** | Bloomberg Terminal, `yfinance`, Excel (Bloomberg exports) |
| **Numerical** | `numpy`, `scipy` (stats, optimize) |
| **Data wrangling** | `pandas` |
| **Machine learning** | `scikit-learn` (PCA, KMeans, StandardScaler) |
| **Statistics** | `statsmodels`, `scipy.stats` |
| **Visualisation** | `matplotlib`, `seaborn`, `matplotlib.animation` |
| **Environment** | Python 3, Jupyter Notebooks |

---

## Domain Coverage

- **Equity research** — fundamental factor construction, peer benchmarking, structural break analysis
- **Financial modelling** — revenue forecasting, scenario analysis, Monte Carlo simulation
- **Credit & LBO** — structural credit models, leverage analysis, covenant stress testing
- **Quantitative methods** — PCA, clustering, hypothesis testing, sensitivity analysis
- **Medical devices sector** — deep familiarity with ABT, MDT, BSX, EW, DXCM and broader universe
