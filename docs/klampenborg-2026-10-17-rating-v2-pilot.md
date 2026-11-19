# Klampenborg 17 October 2026 — MWP-inspired ranking v2 calibration pilot

> **IMPORTANT 2026-11-18 REVISION — supersedes the provisional +48 headline below:** The original pilot used `MWP(HCP - (weight - 59))`, which effectively assumes ~2 new rating points per kg. This mixes the separate HCP-to-ability and kg-to-performance scales. User's MWP observations imply **1.375 new rating points/kg at 1200m**; 1800m point/kg is uncalibrated. Using the corrected separation for Biot alone yields **expected ~118**, raw-time ~63 and **provisional +55** (still assuming unverified 0.20 sec/length). Therefore **the 5-race +48 is NOT a valid approved meeting correction** and must be fully recalibrated after obtaining appropriate distance/going-specific kg and length/speed coefficients. See [weight-and-going research](weight-and-going-research-2026-11-18.md).

Status: **RESEARCH ONLY — not validated, not approved, no production changes** (2026-11-18)

## Sources / precedence
- User's connected Google Sheet **index**: [Races](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit#gid=0&range=A32330:U32392), [Klampenborg – Græs time table](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit#gid=1284952366) and [Handicap class bands](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit#gid=1329435406). Manual times are the observed times; no pre-comparison weight adjustment.
- Audited `Nordic_Racing_v43_candidate.sqlite/off_hcp_by_start`: 63 strict-matched Klampenborg 2026-10-17 starts, 59 pre-race numeric HCP, 4 without assigned HCP (including the 2yo winner). Sources in DB generally cite [official Danish gallop startlists](https://api.danskhv.dk/webapi/gallop/raceinfo/535825/startlists).
- [Official Dansk Galop judges' report](https://www-static.danskgalop.dk/wp-content/uploads/2026/10/Dommerrapport-Offentlig-2.pdf) confirms going **4.9 Blød**, cloudy/dry ~12°C. Notes AFIRE LOVE lost lengths, PHILIANGO shoe issue, etc.
- User-confirmed MWP-like conversion: HCP79->111, HCP83->119, HCP84.5->120, HCP85->121, HCP88->127. For exploratory HCP below 79: `R=2*HCP−47`; above 84.5: `R=2*HCP−49`; interpolate 83..84.5. Historical 121↔83.5 example is superseded by newest agreed lookup (121↔85).

## Definitions
- User custom class midpoint from sheet: class 2 = HCP−59 between 22..26 ⇒ nominal HCP 83 ⇒ rating119; class2.5 centre77.5⇒108; class3.5 centre67⇒87; class4 centre61.5⇒76; class5 centre49.5⇒52.
- **Expected winner rating for 59kg-equivalent**: `R_expected = MWP(HCP_official_pre_start − (actual_weight_kg − 59))`. This is an expectation/reference, not a post-race achieved rating.
- **Raw time grade**: `R_raw = class_nominal_rating − (manually_verified_winner_seconds − class_standard_seconds) / (seconds_per_length * MWP_lengths_per_point_distance)`.
- **Point going candidate**: `proposed_delta = R_expected − R_raw`, positive for slow-going underperformance. Race-specific raw manual time is never weight-adjusted before comparison. Weight only affects *expected relative class benchmark*, not the independent time-standard reference.
- **Experimental assumption only**: `seconds_per_length = 0.20` all distances; at 1200m 0.4 lengths/point, at 1800m **interpolated** 0.725 lengths/point. THIS IS NOT YET EMPIRICALLY CALIBRATED. User explicitly requested not using universal seconds per 1000m; model output remains signed **rating points**, not seconds/1000m.

## Results (five eligible numeric-class races)
| Race | Winner | Dist | User class | Official HCP | Wt kg | HCP@59 | Expected rating | Raw manual time | Class standard time | Time shortfall | Experimental +points |
|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | Biot | 1200 | 2 | 86 | 63 | 82 | 117 | 76.0 | 71.5 | +4.5s | **+54.3** |
| 4 | Wolis Hamoriko | 1800 | 4 | 69 | 66 | 62 | 77 | 117.8 | 110.8 | +7.0s | **+49.3** |
| 5 | Mumbo Jumbo | 1800 | 2.5 | 76 | 57 | 78 | 109 | 114.8 | 108.4 | +6.4s | **+45.1** |
| 7 | Bianca | 1800 | 5 | 57 | 62 | 54 | 61 | 118.1 | 112.4 | +5.7s | **+48.3** |
| 8 | Finn Ind Forever | 1800 | 3.5 | 66 | 58 | 67 | 87 | 116.8 | 110.0 | +6.8s | **+46.9** |

Robust median five races: **+48.3 (show integer +48) NEW MWP-like rating points** at 0.20 s/length. 1800m subgroup median: +47.6; 1200m only one race +54.3 (do not conclude sprint-specific correction from N=1). Range +45.1..+54.3.

Sensitivity to *unvalidated* seconds/length:
- 0.18 → median **+52.7**
- 0.20 → median **+48.3**
- 0.22 → median **+44.7**

This is a wide model uncertainty; do not approve +48 as a real calibrated going variant yet. These are **NEW** rating points, not the legacy negative 0–11 rank offset. User's old `−4` is a comparison label only; it was not used as a model input.

## Three provisional exclusions
| Race | Winner | Distance | Why not in consensus |
|---|---|---:|---|
| 2 | King To Be | 2800m | 3-year-old St. Leger, no applicable 2800m Klampenborg class time standard in index; old ranking was user-judged |
| 3 | Centurion Bling | 1400m | 2-year-old winner has **no assigned official handicap**; cannot establish an independent winner HCP anchor |
| 6 | My Fortune | 1800m | Skandinavisk Grand Prix, no numeric class standard in user's Races class field; do not invent class for race type; inspect separately |

**Important discrepancy to review:** Race 5 is described officially as Handicap **klasse 2** in the judges' report but user's analysis sheet stores **2.5**. Race 8 is officially Autumn Handicap **klasse 3** but sheet stores **3.5**. The calculation *deliberately* follows the user's analysis sheet because it selects the internal reference standard. These differences move the point candidate; require explicit schema rule distinguishing official race class vs custom analytical class before calibration is finalized.

## Guardrails before acceptance
1. Obtain/verifiably calibrate `seconds_per_length` from actual Nordic racing distance/surface/going evidence; avoid assuming the same sec/length all distances.
2. Verify class midpoints and the intended meaning of `Handicap` tab; choice of individual winner HCP is **not** necessarily the whole race's expected class performance. Compare field-rated alternatives, not just winning horse's retrospective result.
3. Evaluate pace exceptions, losing horses, carried-vs-assigned weights (apprentice claim), and whether race-5 class 2 versus 2.5 and race-8 3 versus 3.5 materially affect model output.
4. Stratify sprint vs middle and long distances only with adequate sample.
5. Use the 2024–2025 archive for calibration and 2026 chronologically for validation, with no same-day manual offset leakage. Preserve manual times, original historical rankings and synced user analysis.
6. Do not deploy a new going adjustment or publish historical horse ratings from this first-day pilot.

This report is stored only on a research branch.
