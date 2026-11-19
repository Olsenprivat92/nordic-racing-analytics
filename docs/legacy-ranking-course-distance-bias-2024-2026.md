# Audit: existing ranking comparability across course × distance (2024–2026)

**Research only. Legacy scores, manual times, and the live/new rating model are unchanged.**

## Recommendation
Audit **now**, before calibrating the new MWP-inspired rating scale. This is a diagnostic analysis **in old points only**, not a proposal to continue using legacy offsets for the future rating.

## Scope and controls
The frozen v86 historical archive has 18,387 manual-ranked starts (2,422 races, 1,653 horses) over 2024–2026 and 12 course/surface combinations. Join official pre-race handicaps from v43. The within-horse model compares 10,403 starters with official HCP and numeric race class, across 33 course × distance-band groups. The exact-distance model uses 9,592 starters from 1,140 horses across 40 course×distance groups (minimum 95 starters/group), controlling for **same horse** (fixed effect), official pre-race handicap, numeric race class, finish percentile, field size, carried/analysis weight relative to field median, age, and calendar year. Standard errors are clustered by horse.

**Lower old rank is better.** A positive contrast means the second distance is **harder to obtain a low/good legacy ranking on**, after specified controls.

## Uncorrected vs user-offset winner averages (descriptive, not causal)
| Course | Before original manual offset | After original manual offset |
|---|---:|---:|
| Jægersro dirt | 2.85 | 3.19 |
| Bro Park dirt | 3.34 | 3.52 |
| Klampenborg turf | 5.39 | 3.75 |
| Göteborg turf | 6.21 | 4.21 |
| Øvrevoll turf | 4.80 | 3.60 |

## Exact-distance contrasts after existing user offsets
| Same course/surface | Better old rank on | Worse old rank on | Estimated difference in old points | 95% cluster-robust interval |
|---|---|---|---:|---|
| Göteborg turf | 1400m (129 starts) | 2200m (270) | +0.77 | [+0.59,+0.95] |
| Jægersro dirt | 1600m (189) | 1200m (535) | +0.69 | [+0.55,+0.83] |
| Øvrevoll dirt | 1100m (532) | 1600m (533) | +0.39 | [+0.24,+0.55] |
| Klampenborg turf | 1200m (156) | 2200m (112) | +0.36 | [+0.13,+0.59] |
| Bro Park dirt | 1200m (265) | 2350m (175) | +0.47 | [+0.22,+0.72] |
| Aarhus turf | 1550m (218) | 2000m (252) | +0.39 | [+0.22,+0.57] |
| Øvrevoll turf | 2400m (181) | 1730m (171) | +0.50 | [+0.29,+0.71] |

The intervals are exploratory **not multiple-comparison adjusted**, and selecting extremes inflates apparent certainty.

## Year-to-year sensitivity check (separate within-horse-adjusted residual analysis)
Values below are **second minus first** old-ranking residual.
| Contrast | 2024 | 2025 | 2026 |
|---|---:|---:|---:|
| Göteborg 2200m vs 1400m | +0.35 | +0.77 | +0.44 |
| Jægersro 1200m vs 1600m | +0.19 | +0.60 | +0.65 |
| Øvrevoll dirt 1600m vs 1100m | +0.22 | +0.23 | +0.35 |
| Klampenborg 2200m vs 1200m | +0.07 | +0.44 | +0.19 |
| Aarhus 2000m vs 1550m | +0.94 | −0.05 | −0.02 |
| Bro Park dirt 2350m vs 1200m | +0.28 | +0.58 | −0.06 |

Therefore the Göteborg, Jægersro and Øvrevoll dirt patterns are the strongest **priorities for standard-time QA**, not proven corrections. An alternative distance-interaction model also found same signs (respectively +0.93,+0.44,+0.60), but not identical magnitudes.

## Critical interpretation
- Existing day offsets have substantially reduced inter-course raw winner differences but have **not** fully equalized all track×distance combinations.
- Differences could be residual **standard-time calibration error**, *horse preferences*, tactical pace, meeting going, race composition, or class approximation. Controls reduce but cannot isolate the true cause.
- The old 0–12-point ranking and new 20–160-ish **higher-is-better** rating have incompatible units; **do not mechanically translate** a +0.77 old discrepancy to +0.77 new rating points.
- This audit **does not use official going measurements** to calibrate corrections; user's prior decision stands.
- The proper next step is targeted manual review of the old standard times for the three stable track/distance pairs, followed by independent calibration of the new scale against verified manual times and handicap anchors; the new going model uses +/− NEW rating points only and distance-specific kg factors.

## Reproducibility
Standalone research archive created in the conversation: `Nordic_Racing_Ranking_Bane_Distance_Audit_2026.zip`, with Python code, group estimates, and year checks. Requires extracting existing user-owned v86/v43 SQLite files as `data.sqlite` and `v43.sqlite`; these very large databases are **not** copied into the archive. The audit is observational and retrospective, not a pre-race predictive improvement claim.
