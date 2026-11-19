# Nordic Racing — kontrol efter ni tidstabelrettelser (19. november 2026)

**Status: forskning og næste forslag til brugerens godkendelse. Ingen ændringer i live Google Sheet, ældre rangeringer, manuelle tider, dagsoffsets eller Race Studio fra denne analyse.**

## Kilder og metode
- Brugerens levende `index` Google Sheet: Klampenborg græs 2200m klasse2 **139.1s** (grad1 137.3s), Bro Park dirt 1200m klasse2 **72.3s** (grad1 71.3s). Begge præcist **+0.2s** / **−0.1s** mod tidligere.
- Frozen v86 manual time and original old-rank/offset records: 10,566 manually ranked starts in 1,327 ordinary numeric handicaps, 6,577 top-5 placements from 2024–26. Excludes capped handicaps, amateur, 2yo, 3yo, winners races, maiden.
- Recompute discrete **0.5-step legacy rankings** from archived `ranking_time_original` and nine live standard changes (grade 1–11 only; grade0 untouched), preserve original offset unchanged. Adjust analytical residuals for numeric race class, finish percentile, field size and year, **but do not adjust or re-estimate weight**. Same-day contrasts remove shared meeting-level pace/going offsets without using official going figures.
- All original values remain immutable; testing has **no effect on new MWP-inspired ratings**.

## Nine live standard-time changes validated
| Course | Dist | Change versus frozen original | top-5 N / race N | Archived top-5 old rank -> recalculated |
|---|---:|---:|---:|---:|
| Jægersro dirt | 1200 | +0.3 s | 354 / 72 | 3.825 → 3.525 |
| Jægersro dirt | 1600 | −0.4 s | 128 / 26 | 3.145 → 3.398 |
| Göteborg turf | 2200 | +0.9 s | 160 / 32 | 4.728 → 4.231 |
| Øvrevoll turf | 1980 | +0.4 s | 53 / 11 | 5.132 → 4.868 |
| Göteborg turf | 2400 | +0.4 s | 70 / 14 | 4.257 → 4.021 |
| Göteborg turf | 1600 | +0.2 s | 120 / 24 | 4.338 → 4.167 |
| Klampenborg turf | 2400 | +0.2 s | 60 / 13 | 3.608 → 3.500 |
| **Klampenborg turf** | **2200** | **+0.2 s** | **74 / 15** | **4.595 → 4.486** |
| **Bro Park dirt** | **1200** | **−0.1 s** | **186 / 38** | **3.624 → 3.739** |

The last two updates improve top-5 class/year/finish-adjusted contrasts within their own courses:
- Klampenborg 2200m **+0.274 → +0.166** old point; same-day **+0.309 → +0.199**.
- Bro Park dirt 1200m **−0.271 → −0.156** old point; same-day **−0.250 → −0.137**.

## Next proposal: Øvrevoll dirt 1100m **−0.1 second** (tentative)
- Current grade1 **66.2s**, numeric analysis class 2 **67.2s**. Test: 66.1s / 67.1s, and shift **all standard grade1–11 columns −0.1s**, grade0 unchanged.
- 345 top5 finishes / 70 ordinary handicap races; current top5 average old rank **4.214**. After simulated −0.1s: **4.320**.
- Top5 residual versus other dirt distances on same course: **−0.245 → −0.140**, all-vs-all course residual is also negative before adjustment (−0.264), same-day contrast **−0.297 → −0.193**.
- Year-by-year top5 residual sign: 2024 **−0.397 → −0.287**, 2025 **−0.035 → +0.061**, 2026 **−0.336 → −0.224**. 2025 would flip slightly positive. A −0.2s sensitivity is too aggressive and flips 2025 to +0.170.
- **Class-level risk, important for user review:** class 2 current already +0.08 (slightly worse than other dirt distances of same class); class 4 current **+0.27** (worse) and would be roughly **0.13 old rankpoints worse** after −0.1s. Classes 2.5 and 5 are currently much better than other dirt distances (respectively −0.62 and −0.78). This is a *compromise*, not a clean all-class fix; do not alter classes separately without checking table monotonicity. User may choose to defer if consistency is preferred.
- Track strength preference: Øvrevoll dirt should be about +0.5 old relative to Jægersro. Current no-weight-adjusted track comparison from prior audit about +0.29, so making part of the Øvrevoll dirt table harder would move in desired direction. Track-level preference is only a secondary constraint, not a reason alone to change standards.

## Defer further action on other distances
- **Øvrevoll turf 2400m**: current within-course −0.363, but 2026 ~−0.005; −0.2s scenario pushes 2026 +0.127 (overcorrect). Avoid uniform shift for now.
- **Aalborg turf 1800m**: +0.482 relative within-course; +0.2s shift improves internal balance to +0.333, but improves Aalborg relative to Bro Park when user explicitly expects weaker Aalborg; 2024 is already fast/easy. Requires separate track-class strength comparison.
- **Øvrevoll turf 1170m**: +0.299 overall; 2026 already negative (~−0.123), so blanket +0.2s would worsen 2026; defer.
- **Göteborg turf 2400m**: current +0.214 residual; 2024 already negative ~−0.154 and user recently added +0.4s; do not adjust further immediately.
- **Klampenborg turf 2200m**: current +0.166 after recent +0.2s; 2024 now −0.146; no further shift.
- **Bro Park dirt 1200m**: residual −0.156 after recent −0.1s; class 2 / 3.5 / 4 differ in direction; no further shift.

## Remember for later
User suspects **Klampenborg 1100m rankings are far too easy**, but only 3 standard numeric HCP races / 15 top5 in current window; revisit during full distance-per-track QA after present priority review. User notes old Klampenborg standard-time grade steps by distance: 1100–1300m .5s; 1400 .6s; 1600 .7s; 1800 .8s; 2200 .9s; 2400 1.0s. Hypothesis this may relate to distance-specific lengths/kg from 0.5 at sprint to ~1 at 2400m; **revisit during separate MWP/weight calibration** and avoid interpreting time-grade step as automatically equal to length/kg.

## Reproducing
- `22_recheck_after_nine_no_weight.py` and tables `22_current_all_318_track_distance_class.csv`, `22_current_class_specific_distance_checks.csv`, `22_current_distance_review_with_year_meeting.csv`, `22_same_meeting_distance_contrasts.csv`, `22_live_three_edits_comparison.csv`
- `23_scenarios_after_nine.py`, `23_scenario_summary_after9.csv`, `23_scenario_by_class_after9.csv`
- Requires frozen v86 user-owned source dataset `manual_ranked.pkl` extracted from existing historic records. All recomputation in-memory, **no writes to source**.
