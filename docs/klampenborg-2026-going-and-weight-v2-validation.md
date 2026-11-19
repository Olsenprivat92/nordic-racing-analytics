# Ranking v2 — Klampenborg going, weight and point correction (2026-11-18)
**Research only. No live ranking, original manual time, source spreadsheet or user offset changed.**

## Verified sources
- Original manually checked times, numeric *analysis* race class, historical offsets and course-specific standard-time matrix: `index` Google Sheet, `Races` and `Klampenborg - Græs` tabs, plus v86 frozen archive: https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit
- Official 2026 going measurements, independent of users' historic offsets: [Dansk Galop stewards' report](https://www-static.danskgalop.dk/wp-content/uploads/2026/11/Dommerrapport-Offentlig.pdf). 15 Klampenborg dates from Apr 11 to Oct 17 joined to **907 manually timed starts / 122 races**; only 53 numeric-class race winners with exact course/distance table are eligible for simple winner-based comparisons.
- Earlier v43 official *pre-start* HCP available separately for HCP-related scenario work. Official recorded race times do not replace manually checked times.

## New winner-first point method reproduces historic day offsets without using them as inputs
For each eligible handicap race, compare the winner's **unadjusted raw manual time** to the user's fixed course × surface × distance × analysis-class winner standard. Convert the measured seconds gap to **legacy ranking-point gap** with *that distance's* own seconds per half-ranking step; do NOT divide by 1000m or apply a universal seconds/km correction. Take a robust median across qualifying races. The saved historic `ranking_offset` is read *only after* the model's proposal to evaluate agreement.

### Klampenborg 2026-10-17, official 4.9 soft
| Race | Winner | Metres | Manual s | Class standard s | Gap s | Computed old rank-gap |
|---:|---|---:|---:|---:|---:|---:|
| 1 | Biot | 1200 | 76.0 | 71.5 | 4.5 | 4.500 |
| 4 | Wolis Hamoriko | 1800 | 117.8 | 110.8 | 7.0 | 4.375 |
| 5 | Mumbo Jumbo | 1800 | 114.8 | 108.4 | 6.4 | 4.000 |
| 7 | Bianca | 1800 | 118.1 | 112.4 | 5.7 | 3.5625 |
| 8 | Finn Ind Forever | 1800 | 116.8 | 110.0 | 6.8 | 4.250 |

Median = 4.25 ⇒ **proposed legacy offset −4.25** versus user's saved **−4.0**. If old offsets must occur in half-point steps, −4.25 is an exact tie; user or a documented rounding rule should decide. Race 2 (2800m missing matching standard), race 3 (juvenile nonnumeric class) and race 6 (older winners' race nonnumeric class) are explicitly excluded from day consensus, not assigned guessed figures.

### Cross-day evaluation, 15 official 2026 dates
- Mean absolute disagreement with user's original day-median offset: **0.378 old ranking point**.
- **11/15** within 0.5 old point and **15/15** within 1.0.
- **This is methodology reconstruction**, not proof of independent predictive ability or the right absolute MWP-like score. User's original analysis classes and table standards encode their previous choices; some dates have only 2–3 eligible winner races, and need low-confidence flags.

## Official going: raw clock signal, no old offsets used
Across 53 numeric-class winners:
| Going | Race winners | Median raw time minus class standard |
|---|---:|---:|
| Official number <=3.9 (good/light) | 22 | +2.05 s |
| 4.0–4.3 (mixed) | 10 | +3.40 s |
| >=4.5 (soft/deep) | 21 | +5.80 s |

At fixed distance, good/light→soft/deep: 1400m +1.55→+5.50s (4 vs 5), 1600m +1.40→+6.40s (6 vs 3), 1800m +2.45→+6.60s (8 vs 6). This is a strong **descriptive** association, not controlled for horses' differing ability, race-day tactical speed or season. Spearman correlation going number vs per-day median *raw* class-standard time gap ≈ **+0.880**, p≈1.5e-5, over 15 days.

## Weight: distance/backtest results and uncertainty
- The original ranker uses constant **0.20 sec/kg**, regardless of distance. The source user's MWP observations imply a lower point/kg allowance (e.g. 1200m: 0.55 lengths/kg / 0.40 lengths/new-point = 1.375 new-points/kg).
- Strict historical prior-start backtest: 2026 **11,815 scored pairs in 468 races**. Fixed 0.20 sec/kg correctly orders **62.192%**, experimental 0.12 sec/kg **62.442%**. Clustered race-bootstrap 95% confidence interval for +0.250 percentage-point difference: **[-0.153,+0.689]**. Improvement **not statistically established**.
- 2026 by distance of **upcoming** race: <=1400m 63.60→64.24%; 1401–2000m 62.24→62.41%; >2000m 59.89→59.72%. Distanced three-coefficient model chosen only using 2024–2025 (`0.09 / 0.09 / 0.12 sec/kg` for past races at <=1400/1401–2000/>2000) reaches **62.374%** in 2026, hence does not improve on simple fixed 0.12.
- Official-going exploratory race-demeaned 2026 Klampenborg test: **195 eligible starters** on 7 good/light days yield ~0.071 sec/kg association (race-cluster SE ~0.023); **136 starters** on 5 soft/deep days ~0.069 sec/kg (SE ~0.049). The difference is undetectable; strong collinearity between race HCP and assigned weight makes causal inference inappropriate. Do not introduce a going-dependent per-kg bonus on this evidence.
- BHA contextual reference: [Performance Figures](https://www.britishhorseracing.com/regulation/performance-figures/).

## New 121-style absolute rating: open calibration problem
- Keep HCP→expected-ability scale (121↔HCP85 by the latest user-approved lookup) separate from physical **weight→performance** effects.
- Biot (1200m) HCP86→123, 63kg→expected ~117.5 at MWP 1.375 points/kg; raw time 76s versus class-2 71.5s ⇒ under unverified 0.20 seconds/length and 0.40 lengths/new-ratingpoint raw rating ~62.75, proposed +54.75 **NEW** points. **Not approved**.
- 1800m weight ratio is unknown. Scenario grid 0.85–1.2 new points/kg and 0.18–0.22 seconds/length produces a median across five races of **+47 to +56 NEW ratingpoints**, depending on unproven parameters. These do **not** convert mechanically from the old −4.25.
- **Scale mismatch that must be resolved:** the user's class-2 to 2.5 handicap midpoints differ by ~11 NEW ratingpoints, while their time table class-step is 0.5s at 1200m (0.045 sec/newpoint) and 0.8s at 1800m (0.073 sec/newpoint); unproven 0.20sec/length with user MWP lengths/point implies 0.080s and ~0.145s. These cannot both be imposed as exactly equivalent. Calibrate the absolute scale independently before deploying MWP-like integer ratings.

## Next implementation gate
(1) Prototype the now-verified old-point median + confidence/exclusion review on more days without modifying legacy ranker; (2) obtain independent official going for 2024–2025 and enough races for track × going × distance × kg testing; (3) calibrate absolute time-to-new-point conversion, with documented sensitivity and field-HCP quality checks; (4) only after user approval compute candidate new historic integer horse ratings.

Full reproducible code, all 15 day rows, 53 win comparisons, 2026 holdout and new-scale scenario CSVs are bundled in the ChatGPT research ZIP. No original data changed.
