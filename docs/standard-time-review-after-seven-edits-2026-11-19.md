# Standard-time audit after SEVEN verified user edits, 19 November 2026
**Research only. No modifications to sheet/ranking history.**

## Current Google Sheets standard rows (verified live)
- Jægersro dirt 1200m +0.3s to archived baseline; 1600m −0.4s.
- Göteborg turf 2200m +0.9s, **1600m +0.2s**, **2400m +0.4s**.
- Øvrevoll turf 1980m +0.4s.
- Klampenborg turf 2400m **+0.2s** (grade1 145.8s, class2 147.8s).
- These are the **actual current**, not earlier temporarily transposed Göteborg values. [Original Google Sheet](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit).
- Original manual times, offsets and rank history in v86 immutable.

## Scope and method
10,566 manually ranked starts in 1,327 ordinary numeric handicap races, 6,577 top-5 starts in 2024–26. Excludes maiden/winner/2yo/3yo/amateur/capped handicap races. Reproduce historical discrete 0.5 legacy ranking steps with seven adjusted time standards and preserved original day offsets. Compare all/top5/winners, within class/finish percent/field/year, with additional within-meeting check. No new weight adjustment, no official going inputs, no MWP rating calculation.

### Current effects in top 5
| Track | Distance | Top 5 / races | Old average | Current average |
|---|---:|---:|---:|---:|
| Göteborg turf | 1600m | 120/24 | 4.338 | **4.167** |
| Göteborg turf | 2400m | 70/14 | 4.257 | **4.021** |
| Klampenborg turf | 2400m | 60/13 | 3.608 | **3.500** |

### Next incremental proposals for user's consideration
1. **Klampenborg turf 2200m +0.2s** across old ranks grade 1–11; grade 0 unchanged. Grade1 **137.1→137.3s** and class2 reference **138.9→139.1s**. 74 top5 / 15 races; mean top5 **4.595→4.486**; class/year/finish adjusted internal contrast against other Klampenborg distances **+0.274→+0.168** old rankpoints and within-same-meeting contrast **+0.309→+0.201**. Class 3.5/4/4.5 each improves. Years 2025/26 improve; 2024 slightly overcorrects (−0.007→−0.143), so **no larger initial shift**.
2. **Bro Park dirt 1200m −0.1s** across grade 1–11; grade0 unchanged. Grade1 **71.4→71.3s**, class2 standard **72.4→72.3s**. 186 top5 / 38 races; mean top5 **3.624→3.739**; internal contrast **−0.271→−0.156**, same-meeting **−0.250→−0.138**. Year differences improve in all 3 years. Important tradeoff: class 2 is already relatively weak while 3.5 and 4 overly strong, so **provisional test only** and review class outcomes before user applies; do not auto-change −0.2 or −0.3.

**Candidates deferred:** Øvrevoll dirt 1100m −0.246 old points internally but class4 would be made worse by uniform shift; Øvrevoll turf1170 inconsistent in 2026; Øvrevoll turf1980 only 11 races; Göteborg turf2400 just updated; Odense1800 opposite sign in 2026; Aalborg1800 apparent weak times conflict with user requirement that Aalborg should be materially weaker than Bro Park; Aarhus2000 mostly driven by 2024.

## Important user notes recorded for later, not acted on
- **Klampenborg turf 1100m is suspected far too easy**; sample in numeric handicap 2024–26 only **3 races /15 top5 starts**, with a descriptive residual about **−0.57 old points**, so investigate later in **complete within-track all-distance** check rather than changing now.
- Klampenborg old time-table spacing (seconds **per 0.5 old ranking-grade**, *not per kg*): 1100–1300 **0.5s**, 1400 **0.6s**, 1600 **0.7s**, 1800 **0.8s**, 2200 **0.9s**, 2400 **1.0s**.
- User's observation/hypothesis: perhaps this relates to a distance-dependent *lengths-per-kg* factor (~0.5 lengths at 1100–1300m, ~1 length at 2400m). **Revisit explicitly during later new MWP point/kg/time calibration**. They are not equal units: seconds per half-grade cannot simply be identified with lengths/kg without separately validating seconds-per-length and handicap-grade scaling.
- **Keep weight analysis and MWP entirely separate from the present standard-time audit**, and do not use official going measurements to calibrate future variants.

Full reproducible CSV tables and Python research scripts from this control are in conversation artifact `Nordic_Racing_Tidstabeller_Kontrol_7_Rettelser_og_Noter_2026-11-19.zip`.
