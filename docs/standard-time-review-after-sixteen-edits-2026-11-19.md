# Nordic Racing — audit after 16 approved standard-time edits
**19 November 2026 · Research only. No source Google Sheets, original verified manual times, old day offsets or live Race Studio changed by this audit.**

## Verified latest live standards
[Original connected `index` Google Sheet](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit):
- Aalborg turf **1500m**, grade/class 2 **89.0 → 88.8 seconds** (−0.2). Current grade4 **91.2s**. **49 top-5 finishes / 10 ordinary numerical handicap races**. Top-5 average old rank **4.449 → 4.653**.
- Aalborg turf **1800m**, class 2 **109.2 → 109.3 seconds** (+0.1). Current grade4 **112.5s**. **130 top-5 finishes / 26 races**. Top-5 mean old rank **5.012 → 4.927**.
- The original programmatically verified v86 grade from the stored `ranking_time_original` matches all original ranks before applying the changes; day offsets remain untouched.

## Study scope
**10,566** approved manual-ranked historical starts, **1,327** standard numerical handicap races (2024–2026), **6,577** top5 starts, **64** track×surface×distance cells, **318** track×surface×distance×handicap class groups. Excludes winner/age-limited/maiden/amateur/capped handicap races. Old ranking is **lower-is-better**. Recompute the discrete 0.5-step historical grade with all 16 approved standard-time modifications, then add archived manual day offset unchanged. No new kg model, no MWP rating, no official going measurement used.

Across all 16 adjustments, original manual rank times and original manual day offsets remain immutable. The distance-control residual is adjusted for numeric handicap class, year, finish percentile and field size (NOT weight). Secondary checks compare other distances at the same meeting and the same horse across distances (within 120 days, max one class apart). These are retrospective diagnostic associations, not causally identified standard-time errors.

## Aalborg: both user edits improve local consistency
| Turf distance | Previous top5 residual vs other Aalborg distances | New residual |
|---|---:|---:|
| 1500m | −0.437 | **−0.179** |
| 1800m | +0.418 | **+0.249** |
| 2000m | −0.129 | **−0.126** |

Target strength vs Bro Park turf: Aalborg's standardized top5 difference **+0.693 old points**, versus user's illustrative target **+1.0**. Do **not** force an extra blanket shift to reach target: the strength gap varies with class, and user expects Aalborg class4 to be weaker than Bro Park.

Key caution: within-Aalborg residuals in 2024/2025/2026 after updates:
- 1500m **+0.440/−0.629/+0.095**.
- 1800m **−0.440/+0.576/+0.226**.
A further uniform shift would overcorrect certain years/classes. No new Aalborg change recommended.

## Largest unresolved track-distance differences after 16 edits
| Track / distance | top5 / races | top5 residual | same-day residual | 2024 / 2025 / 2026 residual | Decision |
|---|---:|---:|---:|---|---|
| Øvrevoll turf 1800m | 45 / 9 | −0.562 | −0.418 | +0.230 / −0.683 / −0.911 | **Defer**: nine races, strong class/season mix |
| Aarhus turf 2000m | 154 / 31 | +0.395 | +0.329 | +1.141 / +0.083 / −0.015 | **Defer**: 2024 alone drives magnitude |
| Øvrevoll turf 1980m | 53 / 11 | +0.368 | +0.622 | +0.461 / +0.562 / +0.013 | **Defer**: recently adjusted twice, 2026 now nearly neutral |
| Øvrevoll turf 2400m | 115 / 23 | −0.355 | −0.461 | −0.744 / −0.242 / +0.008 | **Defer**: 2026 nearly neutral |
| Øvrevoll turf 1170m | 155 / 31 | +0.312 | +0.334 | +0.709 / +0.190 / −0.106 | **Defer**: 2026 opposite; within-horse mean only +0.038 |
| Klampenborg turf 2400m | 60 / 13 | +0.219 | +0.519 | +0.042 / +0.116 / +0.639 | **Small +0.1s scenario tested but no new approval recommended** |

### Klampenborg 2400m: why do not add another increment yet
Under a hypothetical additional **+0.1s** at all populated grade1–11 levels, average top5 would improve from 3.500→3.425 and residual +0.219→+0.144. However 2024's residual goes +0.042→−0.041; more importantly class2, already −0.114, becomes −0.239 (worse). Class 2.5/3.5 improve, but not consistently enough to justify another entire-row edit.

### Examples explaining seasonal bias
- Aarhus 2000m historical 2024 meetings include top5 average **6.1** on **2024-05-05 (race 4, class 2.5)** and **6.9** on **2024-06-29 (race 9, class 3)**. In later years, 2000m meets average close to the track's other distance-adjusted standards. A blanket +0.2s may improve the 3-year average but introduce a 2025–26 bias.
- Øvrevoll turf 1800m has just 9 numeric HCP races; 2024 includes conflicting class1.5 and class2 races, 2025–26 lean toward very fast old rankings. This is worthy of individual meeting/pace review, **not an automatic course time shift**.

## Recommendation
**Do not change more whole-distance standards yet.** Freeze the current 16 verified adjustments for this stage, check the 2024 Aarhus 2000m outlier meetings and the Øvrevoll 1800m class/season cohorts, then decide if race-day-specific or class-specific effects explain remaining differences. Averages alone, with multiple exploratory comparisons and unequal class/season composition, will overfit if tuned repeatedly.

Continue to preserve user's deferred questions: Klampenborg 1100m may be too easy but has only 3 ordinary numeric HCP races and has already received a −0.2s change; and Klampenborg's seconds-per-half-grade by distance (0.5/0.6/0.7/0.8/0.9/1.0) may relate to lengths/kg (0.5 at sprint to ~1 at 2400m). Revisit explicitly during distinct **MWP/weight/distance** calibration; do not confuse seconds per half-old-grade with lengths per kg. No official going measurement is used.

**Reproduction:** attached conversation research ZIP `Nordic_Racing_Standardtider_Efter_16_Rettelser_Research.zip` contains the new scripts and source derived CSVs. The large user-owned frozen v86 history is not replicated in this small ZIP.
