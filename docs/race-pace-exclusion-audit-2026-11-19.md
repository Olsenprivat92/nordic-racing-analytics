# Nordic Racing — pace annotations and exclusions from base-time calibration
**19 November 2026. Research only: no original manual times, rankings, offsets, Google Sheet standard times or live model altered.**

## Decision proposed
User notes that unusually slowly run tactical races can make a distance look slow when standard time is in fact fine. **Exclude explicitly race-pace-flagged races from the reference *calibration* sensitivity test**, never erase the races from horses' history. Do not conflate slow *race pace* with a slow *racing surface* or official going measurement. Continue without separate weight or MWP calibration at present.

## What the historical comments actually say
From v86 `starts.comments` joined by `start_id` to the 10,566 manually ranked starters in 1,327 ordinary numeric HCP races (2024–2026):
- Explicit **"Langsomt løb"**, e.g. **"1 Langsom løb"**, including decimal-prefixed variants: **37 races**, 280 starters (2026).
- **"Kunstigt løb"**: **65 races**, 453 starters (39 in 2024, 25 in 2025, one in 2026).
- Additional overpaced-type notes: two races, nine starters, one overlapping an existing flag.
- **Combined distinct race-pace candidates: 103/1,327 races (7.8%), 740 starters and 500 top-five finishes**, spread **39/25/39 races in 2024/2025/2026**.
- A separate **"TIDEN KAN IKKE VERIFICERES"** label occurs on **32 races**, 251 starters; this is time QA, NOT proof of a pace problem.
- Individual **"langsom fra start"** or a horse being detached should not exclude the whole race.

## Preliminary exclusion sensitivity (archived pre-16-edits rankings)
These are *diagnostic only*, taken from frozen manual old rankings *before the 16 later time-standard edits*. They are NOT the final re-ranked current-table comparisons:
| Course/distance | flagged races / all | top-five old mean all | mean excluding flagged races |
|---|---:|---:|---:|
| Aarhus turf 2000m | 4 / 31 | 4.82 | 4.59 |
| Göteborg turf 2400m | 5 / 14 | 4.26 | 3.83 |
| Jægersro dirt 2400m | 5 / 31 | 3.46 | 3.23 |
| Bro Park turf 1200m | 1 / 13 | 3.59 | 3.42 |
| Klampenborg turf 2400m | 3 / 13 | 3.61 | 3.46 |

**Aarhus 2000m outliers:** 2024-06-29 race 9: all six runners explicitly noted **"Kunstigt løb"**. Candidate exclude from base standard. 2024-05-05 race 4: abnormal raw-time grades but **no pace annotation**; flag for human review, do NOT silently assume "normal". For 2024 Aarhus 2000m top five, full mean 5.47 vs pace-filtered 4.96 on archived old rank.

## Correct methodology next
1. Store race-key-level audit flag with source text, original source row, reason category and reviewer status: **explicit slow race**, **artificial race**, **overpaced/review**, **measurement not verifiable**, **horse-only comment**, **statistical outlier without note**.
2. Make parallel analyses including all races vs excluding confirmed race-pace candidates, by **track×surface×exact distance×numeric HCP class**, and display runner, top-five, winner and race counts *after exclusions*, plus year coverage.
3. Analyze whether any of the **16 already-user-approved standard-time changes** should be **reviewed**, but do not automatically revert anything. Require robust same-horse/within-meeting and year checks before proposing more standard updates.
4. Review timed but unannotated outliers without guessing their pace, including Aarhus May 5 race4, and treat `TIDEN KAN IKKE VERIFICERES` as separate QA.
5. In eventual higher-is-better MWP-style **NEW rating** day-going correction, do not let tactical-slow races determine the meeting-wide variant. A race's tactical pace and the day's track-speed correction are different effects. Historical scores and original notes remain unchanged. Avoid official going measurements, per user's earlier decision.

**Status:** Screening flags are a **candidate list**, not permanently accepted exclusions. Don't apply them automatically to production calculations or research with inadequate filtered sample sizes.

Reproducible CSVs and the screening Python code are in conversation artifact `Nordic_Racing_Tempo_og_Kunstige_Loeb_Kontrol_2026-11-19.zip`. Requires user-owned v86 database and manually ranked history source.
