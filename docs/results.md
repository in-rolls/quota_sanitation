# Sanitation: estimates and measurement

Detailed numerical comparisons accompanying the [repository summary](../readme.md). Source paths are relative to the repository root. Tables retain the existing saved estimates; this revision clarifies their interpretation and does not rerun estimation.

## Coverage by fiscal year

None of the six pre-election level comparisons has p < 0.05. This does not establish parallel trends. The FY 2016–17 interactions are positive with p-values of 0.02–0.03, while later-year point estimates are negative and imprecise. The temporal pattern distinguishes the observed years; significance differences alone do not establish differences between their effects.

Source: `code/replication/02_table3_robustness.R`, `output/replication/pretrends.csv`

| Fiscal Year | Period | BW=0.10 p-value | BW=0.075 p-value | BW=0.05 p-value |
|-------------|--------|-----------------|------------------|-----------------|
| 2013-14 | Pre-treatment | 0.63 | 0.53 | 0.99 |
| 2014-15 | Pre-treatment | 0.39 | 0.49 | 0.33 |
| 2015-16 | Partial (elections Oct 2015) | 0.85 | 0.83 | 0.67 |
| **2016-17** | **Post-treatment** | **0.02** | **0.02** | **0.03** |
| 2017-18 | Post-treatment | 0.39 | 0.25 | 0.30 |
| 2018-19 | Post-treatment | 0.56 | 0.61 | 0.37 |


## Coverage-change estimates

Using FY 2016–17 minus FY 2014–15 coverage gives positive interactions at all three bandwidths. Differencing removes fixed additive differences, but causal interpretation still requires comparable counterfactual changes and measurement over time.

Source: `code/replication/02_table3_robustness.R`, `output/replication/did_robustness.csv`

| Bandwidth | N | Interaction Coef | SE | p-value |
|-----------|---|------------------|-----|---------|
| 0.10 | 7,263 | 122.5 | 49.1 | **0.013** |
| 0.075 | 5,488 | 146.1 | 58.7 | **0.013** |
| 0.05 | 3,707 | 177.0 | 72.1 | **0.014** |


## Preferences by state

Uttar Pradesh preference interactions are imprecise and differ in sign across measures. Madhya Pradesh estimates are positive and more precise. These are state-specific associations; a significant estimate in one state and an insignificant estimate in another does not establish a between-state difference or identify mediation of the reservation effect.

Source: `code/replication/01_table2.R`, `output/replication/table2_by_state.csv`

Parentheses report standard errors. Significance markers follow the saved tables.

| State | N | m3 (pref1) | m4 (pref2) | m5 (pref3) |
|-------|---|-----------|-----------|-----------|
| **UP** | 385 | **-0.30** (0.42) | **-0.60** (0.39) | +0.26 (0.33) |
| MP | 382 | +0.99*** (0.27) | +1.07*** (0.23) | +0.60** (0.27) |
| Bihar | 408 | +0.43 (0.43) | +0.44 (0.38) | +0.29 (0.33) |
| Rajasthan | 193 | -0.84 (0.81) | -0.15 (1.08) | -0.91 (0.96) |
| Haryana | 104 | -5.02 (6.43) | -0.50 (3.90) | -2.10 (3.19) |


## Preferences and covariate adjustment

Preference interactions are larger after adding village fixed effects, while toilet-use interactions are positive across specifications. Unadjusted and within-village models compare different variation. Larger adjusted coefficients are not by themselves evidence of a statistical artifact. The mechanism interpretation requires explaining the relevant comparison and linking survey preferences to governing decisions.

Source: `code/replication/01_table2.R` → `run_table2_control_sensitivity()`, `output/replication/table2_control_sensitivity.csv`

| Specification | Toilet Use | Pref 1 | Pref 2 | Pref 3 |
|---------------|------------|--------|--------|--------|
| 1. Raw (no FE, no controls) | 0.19*** | 0.16 | 0.20 | 0.13 |
| 2. Village FE only | 0.13** | 0.35 | 0.46* | 0.37* |
| 3. Village FE + Wealth | 0.13** | 0.31 | 0.42* | 0.36* |
| 4. Paper spec (+ Edu FE) | 0.13** | 0.34 | 0.43* | 0.38* |

| State | Female × Muslim (m2) | N |
|-------|---------------------|---|
| Bihar | 0.04 (SE: 0.09) | 1,132 |
| Madhya Pradesh | 0.09 (SE: 0.05) | 1,782 |
| Uttar Pradesh | 0.14 (SE: 0.07) | 1,825 |
| Rajasthan | 0.32 (SE: 0.24) | 530 |
| Haryana | 0.81 (SE: 0.29) | 2,469 |


## NREGA sanitation spending

The reported Female × Muslim Share interactions are negative in 2016 and 2017. This pattern differs from a positive spending-channel prediction. An interaction describes how a contrast varies with Muslim share; it is not by itself the full reservation effect at a given share. NREGA spending and SBM toilet coverage are distinct outcomes.

Source: `code/replication/05_mnrega.R`, `output/replication/mnrega_heterogeneous.csv`

The dagger marks p < 0.05 in the retained table.

| Year | Coef (BW=0.10) | SE | t-stat | N |
|------|----------------|-----|--------|-----|
| 2016 | -0.058 | 0.030 | -1.9* | 1,030 |
| **2017** | **-0.094** | **0.040** | **-2.3**† | **1,440** |


## Timing across outcomes

FY 2016–17 coverage interactions are positive (107–153); FY 2015–16 interactions range from −9 to −36. Total NREGA spending interactions are negative in 2014 (−0.46 to −0.88), and sanitation interactions are negative in 2016–2017. These outcomes and fiscal windows need separate interpretations.

Source: `code/replication/02_table3_robustness.R`, `output/replication/pretrends.csv`, `output/replication/mnrega_heterogeneous.csv`


## Muslim-share distributions and flexible specifications

The binned estimates are nonmonotonic, and the smoother allows effects to vary across Muslim share. Most observations lie at low shares: the median is 0.074, and 80.4% are below 0.20. High-share comparisons have less support. The listed linear-interaction contributions exclude the reservation main effect and must not be read as total effects. Flexible estimates and bin deletions describe functional-form sensitivity; they do not establish that the linear term is fitting noise. The survey tables separately describe toilet use and preferences.

Source: `code/replication/03_table3_dose_response.R`, `code/replication/01_table2.R`

Coverage differences by Muslim-share bin:

| Muslim Share | Female Effect (pp) |
|--------------|-------------------|
| 0.00–0.05 | -0.6 |
| 0.05–0.10 | -2.9 |
| 0.10–0.15 | -4.1 |
| 0.15–0.20 | -4.8 |
| 0.20–0.25 | **-18.8** |
| 0.25–0.30 | +6.0 |
| 0.30–0.35 | **+32.4** |
| 0.35–0.40 | -9.8 |
| 0.40–0.45 | +1.2 |

Uttar Pradesh preference differences by Muslim-share bin:

| Muslim Share | Female - Male Diff | N |
|--------------|--------------------|----|
| 0.0–0.1 | +0.01 | 1,716 |
| 0.1–0.2 | +0.01 | 356 |
| 0.2–0.3 | **-0.05** | 57 |
| 0.3–0.4 | **-0.12** | 135 |
| 0.4–0.5 | **-0.08** | 62 |
| 0.5–0.6 | +0.16 | 31 |
| 0.9–1.0 | 0.00 | 11 |

| Muslim Share | Linear interaction contribution | Cumulative % of Data |
|--------------|----------------|----------------------|
| < 0.10 | +10.7 pp | 60.7% |
| < 0.20 | +21.5 pp | 80.4% |
| < 0.30 | +32.2 pp | 88.5% |

| Muslim Share | Female Effect | 95% CI | Significant? |
|--------------|---------------|--------|--------------|
| 0.05 | -2.0 pp | [-5.6, +1.7] | No |
| 0.10 | -2.6 pp | [-6.3, +1.1] | No |
| 0.20 | -1.6 pp | [-6.6, +3.4] | No |
| 0.30 | +2.7 pp | [-3.7, +9.1] | No |
| 0.40 | +9.0 pp | [+1.0, +16.9] | **Yes** |
| 0.50 | +15.6 pp | [+5.9, +25.4] | **Yes** |

Survey toilet-use smoother:

| Muslim Share | Female Effect | 95% CI | Sig? |
|--------------|---------------|--------|------|
| 0.05 | +0.090 | [+0.067, +0.113] | Yes |
| 0.10 | +0.100 | [+0.063, +0.136] | Yes |
| 0.20 | +0.110 | [+0.062, +0.158] | Yes |
| 0.30 | +0.120 | [+0.066, +0.174] | Yes |

Survey preference smoother:

| Muslim Share | Female Effect | 95% CI | Sig? |
|--------------|---------------|--------|------|
| 0.05 | +0.019 | [-0.004, +0.042] | No |
| 0.10 | +0.035 | [+0.002, +0.067] | Barely |
| 0.20 | +0.040 | [-0.003, +0.084] | No |
| 0.30 | +0.011 | [-0.040, +0.062] | No |
| 0.40 | -0.018 | [-0.087, +0.050] | No |


## Changes in reported coverage

About 12.6% of GPs have lower reported coverage in FY 2016–17 than in the preceding year. Administrative revisions, denominator changes and changes in physical coverage are possible explanations. The decline alone does not establish prior over-reporting or its direction by treatment.

Source: SBM administrative data analysis

Source: `code/replication/02_table3_robustness.R` → `run_did_corrected()`, `output/replication/did_robustness_corrected.csv`

| Fiscal Year | % GPs with Coverage Regression |
|-------------|--------------------------------|
| 2013-14 | ~1% |
| 2014-15 | ~3% |
| 2015-16 | ~4% |
| **2016-17** | **~12.6%** |

| Metric | Value |
|--------|-------|
| % GPs with corrected baseline | 18.5% |
| Original FY14-15 mean | 8.8 |
| Corrected FY14-15 mean | 0.7 |
| Mean reduction | 8.1 pp |

| Bandwidth | Original Coef | Original p | Floor-baseline coefficient | Floor-baseline p | Change |
|-----------|---------------|------------|----------------|-------------|--------|
| 0.10 | 122.5 | 0.013 | 104.1 | 0.026 | -15.0% |
| 0.075 | 146.1 | 0.013 | 124.4 | 0.027 | -14.9% |
| 0.05 | 177.0 | 0.014 | 141.3 | 0.042 | -20.2% |

The floor-baseline sensitivity uses `min(coverage14_15, coverage15_16, coverage16_17)`. It changes 18.5% of baselines and reduces the fitted interaction by 15–20%. Because it incorporates post-treatment observations, it is an exploratory transformation, not an identified measurement-error correction. It does not establish that the original effect was overstated by that amount.


## Muslim-share bin exclusions

Removing individual share bins changes the interaction, including from 107.4 to 81.5 after excluding [0.55, 0.60). These deletions describe which sample regions contribute to the fitted coefficient; they do not identify a corrected estimate.

Source: `code/replication/02_table3_robustness.R`, `output/replication/leave_one_out.csv`

| Dropped Bin | Remaining N | Coefficient | Change from Full |
|-------------|-------------|-------------|------------------|
| Full Sample | 7,263 | 107.4 | — |
| [0.55, 0.60) | 7,213 | 81.5 | -24.1% |
| [0.65, 0.70) | 7,223 | 88.8 | -17.4% |
| [0.45, 0.50) | 7,186 | 89.5 | -16.7% |
| [0.00, 0.05) | 4,819 | 124.7 | +16.1% |


## Bandwidth and specification comparisons

All 50 listed specifications have p < 0.10; 23 have p < 0.05. Both point estimates and uncertainty vary with bandwidth. The specifications are related analyses of the same data, not independent replications.

Source: `code/replication/02_table3_robustness.R`, `output/replication/specification_curve.csv`

| Bandwidth | Significant (p < 0.05) | Significant (p < 0.10) |
|-----------|------------------------|------------------------|
| BW=0.05 | 0/10 (0%) | 10/10 (100%) |
| BW=0.075 | 5/10 (50%) | 10/10 (100%) |
| **BW=0.10** | **10/10 (100%)** | 10/10 (100%) |
| BW=0.125 | 8/10 (80%) | 10/10 (100%) |
| BW=0.15 | 0/10 (0%) | 10/10 (100%) |
| **Overall** | **23/50 (46%)** | **50/50 (100%)** |


## Power and selection scenarios

The reported minimum detectable interaction at 80% power is 133.2. Type M ratios condition on assumed true effects and selection for significance. They illustrate possible magnitude exaggeration under those assumptions, not an estimate of bias in the published coefficient.

Source: `code/replication/04_power_sensitivity.R`, `output/replication/power_analysis.csv`

| Metric | Value |
|--------|-------|
| Observed coefficient | 107.4 |
| Standard error | 47.6 |
| MDE at 80% power | 133.2 |
| Observed / MDE | 0.81 |
| Power at observed effect | 62% |

| True Effect | Power | Exaggeration Ratio |
|-------------|-------|-------------------|
| 100 | 56% | 1.34× |
| 75 | 35% | 1.67× |
| 50 | 19% | 2.38× |
| 35 | 11% | 3.31× |
| 15 | 6% | 7.48× |


## Reported confounding sensitivity

The saved diagnostic reports E-values of 8.08 and 1.72 and partial R² of 0.15%. Applying risk-ratio sensitivity interpretations to this continuous-outcome interaction requires checking the conversion and assumptions in the script. These quantities alone do not identify omitted confounding or resolve the design.

Source: `code/replication/04_power_sensitivity.R`, `output/replication/sensitivity_analysis.csv`

| Metric | Value |
|--------|-------|
| E-value (point estimate) | 8.08 |
| E-value (95% CI) | 1.72 |
| Partial R² of treatment | 0.15% |

