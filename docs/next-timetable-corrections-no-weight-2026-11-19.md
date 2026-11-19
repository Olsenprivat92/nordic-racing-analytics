# Tidsstandarder: genkontrol efter tre rettelser — 19. november 2026
**RESEARCH ONLY; NO SOURCE OR LIVE MODEL EDITS.** Full reproducible CSVs, code and workbook are contained in the conversation deliverable `Nordic_Racing_Tidstabel_Naeste_Forslag_2026-11-19.zip`.

## Scope and constraints
10,566 manually ranked starts in 1,327 ordinary numeric handicaps (2024–2026), of which 6,577 finish in top five. Excludes maiden, age-restricted, older-winners, amateur and capped handicaps. Simulates user-edited live standard rows Jægersro dirt 1200 +0.3s, 1600 −0.4s and Göteborg turf 2200 +0.9s relative to **frozen actual historical** v86 thresholds. Original ranking/time/offset remain unchanged. Analysis controls **race class, year, finish percentile and field size**, explicitly **no new adjustment/variable for weight** (old rankings continue to include their historic original formula). It also compares race averages to other distances **on the same race day** to reduce common track/day influence. No official going numbers used.

### Three edits — retain
| Track | Distance | Top 5 starts | Original top-5 mean | Simulated current top-5 mean |
|---|---:|---:|---:|---:|
| Jægersro dirt | 1200 | 354 | 3.825 | 3.525 |
| Jægersro dirt | 1600 | 128 | 3.145 | 3.398 |
| Göteborg turf | 2200 | 160 | 4.728 | 4.231 |

Jægersro 1200/1600 top-five gap falls from 0.68 to ~0.13 old points. Göteborg 2200 is no longer the major residual outlier. Do not apply the Göteborg 0.9s a second time.

## Next three *review-only* candidate edits (shift table grade 1–11; leave grade 0 unchanged)
| Course/distance | Top5/races | Current top5 | Scenario new top5 | Proposed extra seconds | Evidence |
|---|---:|---:|---:|---:|---|
| Øvrevoll turf 1980 | 53/11 | 5.132 | 4.858 | **+0.4 s** | Top5 class/year-adjusted residual +0.756 old points vs other track distances; same-meeting +1.003. Classes 3,4.5,5 share positive direction, three calendar years positive (one year only 13 top5). 1 archived formula exception, explicitly preserved |
| Göteborg turf 2400 | 70/14 | 4.257 | 3.971 | **+0.4 s** | Adjusted residual +0.407, same-meeting +0.654. Classes 2.5,3,3.5 all positive; 2025–26 persistent, 2024 near neutral |
| Göteborg turf 1600 | 120/24 | 4.338 | 4.167 | **+0.2 s** | Adjusted residual +0.242, same-meeting +0.207. All 3 years positive, weaker evidence for class 4.5 |

Effects above were simulated with the original discrete half-rank timetable thresholds, not assuming one linear time→rank conversion. Changing all threshold grades can overshoot particular classes. Use the specified small magnitudes and recalculate before additional adjustments.

## Hold rather than applying a flat correction
- **Bro Park dirt 1200**: adjusted residual −0.270; 186 top5/38 races. Class 2 is +0.417 (opposite to class 3.5 −0.540 and class 4 −0.714). A flat −0.2s scenario raises top-5 mean 3.624→3.858, but likely harms stronger classes. Review class/pace splits.
- **Øvrevoll dirt 1100**: overall −0.246 but class 4 +0.274, class 5 −0.778; not homogeneous.
- **Øvrevoll turf 2400**: overall −0.384 but 2026 difference −0.028 and class 2 points the other way; do not modify.
- **Klampenborg turf 2400**: +0.318, partly year-dependent; only 13 races; do not modify yet.
- **Aalborg turf 1800**: +0.479 relative to other distances, but track-wide target is a materially *weaker* field than Bro Park; moving the table to rank horses better may violate user-stated course quality goals; do not blindly modify.
- **Aarhus turf 2000**: large 2024 difference +1.136, but 2025 +0.078, 2026 −0.012, thus not persistent.

## Course targets after 3 changes (no new weight control)
Top5 adjusted old-ranking difference to turf Bro Park: Klampenborg +0.123 (target +0.10), Göteborg +0.382 (target +0.25), Aarhus +0.594 (target +0.60), Odense +0.415 (target +0.80), Aalborg +0.661 (target +1.00), Øvrevoll turf +0.277 (target +0.10). For dirt relative to Jægersro: Bro Park +0.106 (target +0.30), Øvrevoll +0.291 (target +0.50). These are **descriptive adjusted ranking associations** not objectively measured physical track quality; changing course targets may inappropriately absorb horse quality and pace.

## Review protocol
Keep 3 already user-edited tables; propose only the 3 small candidates; if approved, user or explicit separate edit modifies respective current Google Sheet **time thresholds from grade 1 through 11, not grade 0**. Then validate all 318 course-distance-class combinations and year-specific top5/winner/all summaries again, without mutating historic manual times/rankings/offsets. Do not move to NEW MWP-inspired higher-is-better scores until the old timetable audit is coherent. The v2 going model will use +/− **NEW rating points**, never translated legacy day offsets. 
