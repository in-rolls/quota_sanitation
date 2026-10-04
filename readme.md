# Gender Quotas and Sanitation Provision

Replication and analysis of Chaturvedi, Das and Mahajan (2023), *When Do Gender Quotas Change Policy? Evidence from Household Toilet Provision in India*.

The repository examines the Uttar Pradesh reservation comparison, sanitation preferences in the SQUAT survey, and administrative coverage and spending measures. These sources measure different stages of the proposed relationship between women's representation and sanitation provision.

## Coverage and election timing

The 2015 elections occurred in October, so FY 2015–16 contains both pre- and post-election months. The Female × Muslim Share coverage interaction is positive in FY 2016–17; later-year estimates are negative and imprecise. None of the six earlier level comparisons has p < 0.05, which does not by itself establish parallel trends.

Using coverage change from FY 2014–15 to FY 2016–17 gives:

| Bandwidth | N | Interaction | SE | p-value |
|---|---:|---:|---:|---:|
| 0.10 | 7,263 | 122.5 | 49.1 | 0.013 |
| 0.075 | 5,488 | 146.1 | 58.7 | 0.013 |
| 0.05 | 3,707 | 177.0 | 72.1 | 0.014 |

The interaction describes a change in the reservation contrast across Muslim share, measured from 0 to 1. It is not the average reservation effect. [Yearly and change estimates](docs/results.md#coverage-change-estimates).

## Preferences and governing decisions

Uttar Pradesh preference interactions are imprecise; Madhya Pradesh estimates are positive and more precise. Pooled preference coefficients increase after village fixed effects are added. Those facts call for distinguishing unadjusted, within-village and state-specific comparisons; they do not establish that a mechanism is absent or that covariate adjustment creates an artifact.

NREGA sanitation-spending interactions are negative in 2016 and 2017 (−0.058 and −0.094 at bandwidth 0.10). Spending, survey preferences and toilet coverage are distinct measures. Their connection to a common mechanism requires evidence about governing decisions. [Preferences and spending](docs/results.md#preferences-by-state).

## Measurement and sample support

About 12.6% of GPs report lower coverage in FY 2016–17 than a year earlier. Administrative revisions, denominator changes and physical changes are possible explanations. The available comparisons do not identify which occurred. Taking the minimum of pre- and post-election coverage reduces the interaction by 15–20%, but that transformation uses post-treatment outcomes and is not a validated correction.

Muslim share is below 0.20 for 80.4% of observations. Flexible specifications and bin exclusions show how the fitted interaction depends on this support. Across 50 specifications, 23 have p < 0.05 and all 50 have p < 0.10. These results describe specification sensitivity without resolving the causal assumptions. [All detailed tables and definitions](docs/results.md).

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
