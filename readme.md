# Replication Analysis: Chaturvedi, Das & Mahajan (2023)

Replication and analysis of *When Do Gender Quotas Change Policy? Evidence from Household Toilet Provision in India*. The central question is whether the estimated sanitation response to women's reservations is explained by women's preferences, particularly in villages with larger Muslim populations.

## Main findings

1. **The preference evidence does not establish the proposed mechanism in Uttar Pradesh, where the main reservation comparison is estimated.** UP's three preference interactions are −0.30, −0.60 and +0.26, all imprecise. Madhya Pradesh has positive, more precise estimates of +0.99, +1.07 and +0.60. The pooled survey result therefore needs a state-specific justification before it can explain the UP policy result. [State comparisons](#preferences-by-state).
2. **The pooled preference pattern depends on the comparison being made.** Adding village fixed effects increases the three interactions from 0.16, 0.20 and 0.13 to 0.35, 0.46 and 0.37; the latter two then have p < 0.05. Toilet-use interactions remain positive across specifications. Within-village preference differences and aggregate preference differences are distinct empirical claims, and the mechanism needs to specify which drives governing decisions. [Covariate adjustment](#preferences-and-covariate-adjustment).
3. **NREGA sanitation spending provides no corroboration for a positive spending channel.** Its Female Reservation × Muslim Share interaction is −0.058 (SE 0.030) in 2016 and −0.094 (SE 0.040) in 2017. Explaining more toilet coverage through greater sanitation spending requires reconciling these signs and the programs' different funding channels. [Spending](#nrega-sanitation-spending).
4. **The positive coverage interaction is concentrated in FY 2016–17.** Estimates are 107–153 that year, −54 to −95 in FY 2017–18, and −32 to −74 in FY 2018–19. Coverage-change estimates remain positive (122–177, p ≈ 0.013–0.014), but the later years do not reproduce the positive point-estimate pattern. Reported coverage also falls in about 12.6% of GPs in FY 2016–17, raising a separate measurement question. [Timing](#coverage-by-fiscal-year) and [coverage revisions](#changes-in-reported-coverage).
5. **The size and shape of the interaction depend materially on sparse parts of the Muslim-share distribution.** Muslim share is below 0.20 for 80.4% of observations. Raw coverage differences are negative in each bin below 0.25, while higher-share differences fluctuate. Removing just 50 of 7,263 GPs in the [0.55, 0.60) bin lowers the fitted interaction from 107.4 to 81.5, a 24.1% change. Across 50 specifications, 23 have p < 0.05 and all 50 have p < 0.10. [Distribution and flexible fits](#muslim-share-distributions-and-flexible-specifications), [bin exclusions](#muslim-share-bin-exclusions) and [specifications](#bandwidth-and-specification-comparisons).

These findings concern the size, persistence and explanation of the estimated response. The positive coverage-change results are part of that evidence. The preference comparisons, spending results and measurement diagnostics need to be reconciled with it before attributing the response to women's sanitation preferences.

## Measures and comparisons

The policy analysis uses the 2015 Uttar Pradesh gram panchayat reservation design. The survey analysis uses the 2014 SQUAT survey across five states. They involve different respondents, geographic samples and outcomes.

- **Toilet coverage:** reported percentage of GP households with toilets in the SBM administrative data.
- **Latrine preferences:** three codings of survey item `e13_N`, implemented as `latrine_pref1`, `latrine_pref2` and `latrine_pref3` in `code/replication/00_utils.R`.
- **Female reservation:** whether the GP presidency is reserved for women. Survey comparisons instead use the respondent's gender.
- **Muslim share:** a proportion from 0 to 1. The policy and survey analyses use their respective data sources.

An interaction coefficient describes how the female-reservation contrast changes with Muslim share. It is not the reservation effect at every share: the corresponding main effect must also be included. Raw bin differences and the exploratory smooth fits below are descriptive comparisons, not replications of the instrumental-variable specification.

FY 2013–14 and FY 2014–15 precede the 2015 elections; FY 2015–16 spans the election year; FY 2016–17 is the first full subsequent fiscal year. The tables below report the saved estimates and identify their scripts and outputs.

## Coverage by fiscal year

None of the six pre-election level comparisons has p < 0.05. The FY 2016–17 interactions are positive (107–153), but the later-year point estimates reverse sign: −54 to −95 in FY 2017–18 and −32 to −74 in FY 2018–19. The observed pattern therefore offers no consistent positive replication across post-election years. Later estimates are imprecise, and a formal comparison across years is needed to establish changes in the effect. These separate level comparisons are not a test establishing parallel trends.

Source: `code/replication/02_table3_robustness.R`, `output/replication/pretrends.csv`

| Fiscal Year | Period | BW=0.10 p-value | BW=0.075 p-value | BW=0.05 p-value |
|-------------|--------|-----------------|------------------|-----------------|
| 2013-14 | Pre-treatment | 0.63 | 0.53 | 0.99 |
| 2014-15 | Pre-treatment | 0.39 | 0.49 | 0.33 |
| 2015-16 | Election year | 0.85 | 0.83 | 0.67 |
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

The main policy comparison is in Uttar Pradesh, but its survey preference interactions are negative for two measures and positive for the third, with substantial uncertainty. Madhya Pradesh has the clearest positive preference pattern. The pooled evidence does not establish that the proposed preference mechanism operates in the state supplying the policy estimate. A formal between-state comparison would be needed to establish that the state coefficients differ; the UP estimates also leave room for positive effects.

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

None of the three raw preference interactions has p < 0.05 (p = 0.202, 0.096 and 0.231). Adding village fixed effects roughly doubles their sizes, and the second and third then have p = 0.028 and 0.045. The sample also changes from 1,512 to 1,477 respondents. Thus the reported preference result depends on both the comparison and the estimation sample; it is not a uniform pattern across specifications.

This matters for the mechanism: an argument about within-village gender differences must explain how those differences translate into policy, while an argument about aggregate preference demand needs evidence at that level. Controls can legitimately increase coefficients. The increase alone does not establish a statistical artifact. Toilet-use interactions, by comparison, are positive throughout (0.13–0.19).

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

The reported Female Reservation × Muslim Share interactions are negative in both 2016 and 2017, opposite to a channel in which the reservation-induced spending response increases with Muslim share. The 2017 estimate is −0.094 (SE 0.040). These results require reconciliation with the positive coverage interaction if spending is offered as corroborating mechanism evidence.

NREGA spending and SBM toilet coverage involve different programs and measures, so a decline in this spending interaction does not by itself establish a decline in total sanitation provision. Nor does the interaction alone give the full reservation effect at a particular Muslim share.

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

The raw coverage differences are negative in every displayed bin below Muslim share 0.25, rise to +32.4 percentage points in the 0.30–0.35 bin, then fall to −9.8 in the next bin. The simple descriptive pattern does not trace a steadily increasing reservation contrast. Sampling noise can make bins nonmonotonic even when the underlying relationship is smooth; these are raw differences, not the paper's instrumental-variable estimates.

Most observations are at low shares: the median is 0.074 and 80.4% are below 0.20. The smooth fit gives contrasts of about −2 to −3 percentage points at shares 0.05–0.20, compared with +9.0 at 0.40 and +15.6 at 0.50. Thus the positive fitted contrasts occur in a much smaller part of the observed distribution. The bin-deletion results below show that those observations materially affect the linear interaction.

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

Women report similar or lower preferences in the displayed bins below 0.50; the positive difference at 0.50–0.60 rests on 31 observations. This descriptive pattern supplies little support for a steadily increasing female preference advantage in UP. It is distinct from the consistently positive gender differences in toilet use.

| Muslim Share | Female - Male Diff | N |
|--------------|--------------------|----|
| 0.0–0.1 | +0.01 | 1,716 |
| 0.1–0.2 | +0.01 | 356 |
| 0.2–0.3 | **-0.05** | 57 |
| 0.3–0.4 | **-0.12** | 135 |
| 0.4–0.5 | **-0.08** | 62 |
| 0.5–0.6 | +0.16 | 31 |
| 0.9–1.0 | 0.00 | 11 |

For scale, the table evaluates the interaction contribution at shares 0.10, 0.20 and 0.30 and reports the sample percentage below each value. These contributions exclude the reservation main effect, −11.68 at bandwidth 0.10. For example, the full fitted contrast at share 0.10 is approximately −11.68 + 107.44 × 0.10 = −0.94 percentage points.

| Muslim share evaluated | Linear interaction contribution | % of data below this share |
|--------------|----------------|----------------------|
| 0.10 | +10.7 pp | 60.7% |
| 0.20 | +21.5 pp | 80.4% |
| 0.30 | +32.2 pp | 88.5% |

| Muslim Share | Female Effect | 95% CI | Significant? |
|--------------|---------------|--------|--------------|
| 0.05 | -2.0 pp | [-5.6, +1.7] | No |
| 0.10 | -2.6 pp | [-6.3, +1.1] | No |
| 0.20 | -1.6 pp | [-6.6, +3.4] | No |
| 0.30 | +2.7 pp | [-3.7, +9.1] | No |
| 0.40 | +9.0 pp | [+1.0, +16.9] | **Yes** |
| 0.50 | +15.6 pp | [+5.9, +25.4] | **Yes** |

The coverage intervals above reproduce the saved output. The current script computes `sqrt(se0^2 + se1^2)` for the contrast, omitting the covariance between predictions from the same fitted model. They should not be treated as validated confidence intervals for that contrast. The point-estimate pattern remains a descriptive diagnostic.

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

About 12.6% of GPs have lower reported coverage in FY 2016–17 than in the preceding year, compared with approximately 1–4% in earlier years. That change makes the stability of the administrative outcome a substantive concern. Administrative revisions, denominator changes and changes in physical coverage are possible explanations; a coverage decline alone cannot distinguish them.

If revisions differ by reservation status and Muslim share, an estimated interaction could reflect reporting changes as well as construction. Differencing addresses a fixed additive reporting error, but not changing reporting practices. If earlier coverage was overstated, higher reported baselines also create more room for downward revision. These are explanations to investigate, not findings that the existing comparison identifies.

Source: `code/replication/02_table3_robustness.R` → `run_did_corrected()`, `output/replication/did_robustness_corrected.csv`

| Fiscal Year | % GPs with Coverage Regression |
|-------------|--------------------------------|
| 2013-14 | ~1% |
| 2014-15 | ~3% |
| 2015-16 | ~4% |
| **2016-17** | **~12.6%** |

| Metric | Value |
|--------|-------|
| % GPs whose baseline is changed by the floor rule | 18.5% |
| Original FY14-15 mean | 8.8 |
| Floor-baseline FY14-15 mean | 0.7 |
| Mean reduction | 8.1 pp |

| Bandwidth | Original Coef | Original p | Floor-baseline coefficient | Floor-baseline p | Change |
|-----------|---------------|------------|----------------|-------------|--------|
| 0.10 | 122.5 | 0.013 | 104.1 | 0.026 | -15.0% |
| 0.075 | 146.1 | 0.013 | 124.4 | 0.027 | -14.9% |
| 0.05 | 177.0 | 0.014 | 141.3 | 0.042 | -20.2% |

The floor-baseline sensitivity uses `min(coverage14_15, coverage15_16, coverage16_17)`. It changes 18.5% of baselines and reduces the fitted interaction by 15–20%. Because it incorporates post-treatment observations, it is an exploratory transformation, not an identified measurement-error correction. It does not establish that the original effect was overstated by that amount.


## Muslim-share bin exclusions

Removing only 50 of 7,263 GPs in the [0.55, 0.60) bin lowers the interaction from 107.4 to 81.5 (24.1%). Removing 40 GPs in [0.65, 0.70) lowers it to 88.8 (17.4%). These are substantial magnitude changes from small sample deletions. Other deletions increase the estimate: removing [0.60, 0.65), for example, raises it to 130.1 (21.1%). The fitted slope is sensitive to particular portions of the distribution, rather than uniformly driven upward by every high-share bin. Deletion estimates are diagnostics, not identified corrections.

Source: `code/replication/02_table3_robustness.R`, `output/replication/leave_one_out.csv`

| Dropped Bin | Remaining N | Coefficient | Change from Full |
|-------------|-------------|-------------|------------------|
| Full Sample | 7,263 | 107.4 | — |
| [0.55, 0.60) | 7,213 | 81.5 | -24.1% |
| [0.65, 0.70) | 7,223 | 88.8 | -17.4% |
| [0.45, 0.50) | 7,186 | 89.5 | -16.7% |
| [0.00, 0.05) | 4,819 | 124.7 | +16.1% |


## Bandwidth and specification comparisons

All 50 listed specifications have p < 0.10; 23 have p < 0.05. At bandwidth 0.10, all ten have p < 0.05, compared with none at 0.05 or 0.15. At the narrow bandwidth, estimates are larger but less precise; at the widest, estimates are smaller. The size and precision of the result therefore depend on bandwidth, even though the direction and the p < 0.10 pattern are consistent. These are related analyses of the same data, not independent replications.

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
| 50 | 18% | 2.38× |
| 35 | 11% | 3.30× |
| 15 | 6% | 7.52× |


## Reported confounding sensitivity

The saved diagnostic reports E-values of 8.08 and 1.72 and partial R² of 0.15%. Applying risk-ratio sensitivity interpretations to this continuous-outcome interaction requires checking the conversion and assumptions in the script. These quantities alone do not identify omitted confounding or resolve the design.

Source: `code/replication/04_power_sensitivity.R`, `output/replication/sensitivity_analysis.csv`

| Metric | Value |
|--------|-------|
| E-value (point estimate) | 8.08 |
| E-value (95% CI) | 1.72 |
| Partial R² of treatment | 0.15% |


## Interpreting the policy and mechanism evidence together

The coverage-change specification yields a positive interaction across all three reported bandwidths. The remaining questions concern its persistence, its sensitivity to the distribution of Muslim share, and whether the survey and spending measures explain it. Survey preferences, actual toilet use, construction and spending are different outcomes; showing one does not establish the causal link to the next.

Program targeting, economic change and SBM implementation are candidate explanations for time-varying sanitation patterns. Their correlation with Muslim share alone would not invalidate the reservation design. An alternative explanation would have to affect the identified reservation contrast or its measurement in a way the specification does not absorb. The existing diagnostics do not identify which explanation accounts for the FY 2016–17 pattern.

## Replication Files

### Code
- `code/replication/00_utils.R` - Shared utility functions (data loading, formatting)
- `code/replication/01_table2.R` - Table 2 analyses (by state, control sensitivity, dose-response preferences, GAM)
- `code/replication/02_table3_robustness.R` - Table 3 robustness (placebo, coverage temporal, leave-one-out, specification curve)
- `code/replication/03_table3_dose_response.R` - Table 3 dose-response (coverage, GAM interaction)
- `code/replication/04_power_sensitivity.R` - Power analysis (Type M errors) and sensitivity (E-values)
- `code/replication/05_mnrega.R` - MNREGA spending analysis (main effects + heterogeneous effects)

### Output
- `output/replication/table2_by_state.csv` - State-level Table 2 results
- `output/replication/table2_control_sensitivity.csv` - Table 2 with varying controls (raw, village FE, wealth, education FE)
- `output/replication/pretrends.csv` - Pre-trends test (coverage by fiscal year with interaction p-values)
- `output/replication/did_robustness.csv` - DID robustness (coverage change as outcome)
- `output/replication/did_robustness_corrected.csv` - DID robustness with floor-baseline sensitivity (uses post-treatment observations)
- `output/replication/mnrega_main.csv` - NREGA main effects (simple RD)
- `output/replication/mnrega_main_bw*.tex` - LaTeX tables by bandwidth
- `output/replication/mnrega_heterogeneous.csv` - NREGA heterogeneous effects (Female × Muslim interaction by year)
- `output/replication/dose_response_coverage.csv` - Toilet coverage by Muslim share bin
- `output/replication/dose_response_coverage.pdf` - Toilet coverage dose-response plot
- `output/replication/dose_response_preferences.csv` - Latrine preferences by Muslim share bin
- `output/replication/gam_interaction.csv` - GAM predicted effects for Table 3
- `output/replication/gam_interaction.pdf` - GAM plot for Table 3 (toilet coverage)
- `output/replication/gam_table2.csv` - GAM predicted effects for Table 2
- `output/replication/gam_table2.pdf` - GAM plot for Table 2 (toilet use and preferences)
- `output/replication/leave_one_out.csv` - Leave-one-out analysis results
- `output/replication/specification_curve.csv` - Specification curve results
- `output/replication/specification_curve.pdf` - Specification curve plot
- `output/replication/power_analysis.csv` - Power analysis and Type M errors
- `output/replication/sensitivity_analysis.csv` - E-values and sensitivity metrics

## Sources

Election timing documentation:
- [Aaj Tak - UP Panchayat Election 2015](https://www.aajtak.in/india/uttar-pradesh/story/uttar-pradesh-announces-panchayat-elections-in-four-phase--313437-2015-09-21)
- [State Election Commission UP](https://sec.up.nic.in/site/)
- [Ministry of Panchayati Raj](https://panchayat.gov.in/en/status-of-panchayat-elections-in-pris/)
