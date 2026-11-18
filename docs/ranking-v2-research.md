# Nordic Racing — Ranking v2: source audit and calibration plan
Date: 2026-11-18. **RESEARCH-ONLY**. No modification of original rankings, manual times, live model, or synced user edits.

## Evidence audited
- Old historical master: `Nordic_Racing_v86_Godkendt_Ranking_Import_og_Manuelle_Offsets.zip`, `starts` table, 110,670 starts total, 18,387 numeric manual rankings in 2024–2026 (min 0, max 12, 25 distinct half-step values). 26 intentionally manually overridden cells must retain priority.
- All 18,387 manual-ranked rows have verified manual time, ranking time, and `weight_original_kg`.
- **Exact identity across all 18,387** (machine epsilon tolerance):
  `ranking_time_original = verified_manual_time_seconds + (59 - weight_original_kg) * 0.2`.
  This is 0.20 seconds per kg, at **all distances**. Do not accidentally apply the proposed new weight adjustment to `ranking_time_original` again; start from untouched `verified_manual_time_seconds`.
- The legacy ranking is assigned by course × surface × distance thresholds plus individual `ranking_offset` (source `v85_formula_reference.py`). Thresholds introduce quantization at 0.5 rank units and exceptional manual values.
- Joined on exact `start_id` to `Nordic_Racing_v43_Ovrevoll_Official_HCP.zip`, table `off_hcp_by_start`: 16,350 manual-ranked starts with `status='official_pre_start'` and official handicap >0. Raw Pearson correlation of manual ranking versus pre-race HCP ~-0.643. This is a sanity check, **not** a mapping from race performance to ability. A rating of 121 corresponding to HCP 83.5 for one observed runner is insufficient to derive a universal formula.
- External conceptual reference: https://www.mrworldpool.com/learn/article/understanding-the-rating — standard times per course/distance/surface; daily track-speed variant; historical race figure incorporates carried weight; horse-independent race-day correction. These principles are reference, not evidence that Nordic Racing has the same algorithm.

## User-provided Mr World Pool conversion observations (unverified externally)
| distance m | lengths / point | lengths / kg | points / kg |
| --- | ---: | ---: | ---: |
| 1010 | 0.35 | 0.50 | 1.4286 |
| 1200 | 0.40 | 0.55 | 1.3750 |
| 1400 | 0.50 | 0.60 | 1.2000 |
| 1600 | 0.65 | 0.70 | 1.0769 |
| 2000 | 0.80 | unknown | unknown |
| 2400 | 0.90 | unknown | unknown |

## Proposed next experimental design
1. Keep original `ranking_original`, verified manual time, manual offsets, 26 overrides exactly as they are. Write all derived features with `rating_method='v2_candidate'`, `calibration_version`, and source identifiers. No automatic activation.
2. **Performance figure (after race):** start from verified manual race times. For each race, use one common track/time variant and course × surface × distance par standard. Convert observed time difference into seconds per length and then rating points; adjust from analysis/base weight (pre-apprentice relief) using distance-specific lengths/kg. Keep exact weight-provenance QA. Never alter manual source time. For within-race deltas:
   `delta_points_i_vs_ref = -(time_i-time_ref) / seconds_per_length / lengths_per_point + (base_weight_i-base_weight_ref) * lengths_per_kg / lengths_per_point`.
   **Important:** Higher performance rating is better. Seconds-per-length must be calibrated by course × distance × surface/going; any approximate race-speed method must be tagged as provisional. Provisional interpolation allowed only with explicit source and confidence; no guessed weights for 2000/2400.
3. **Absolute scale:** within-race `delta_points` requires a robust race-day/inter-race anchor. Use established runners' prior ability, vetted official HCP and standard times to calibrate, with strict past-only training. Do not assign a universal `HCP + 37.5` or rebrand the 0–12 ranking.
4. Use a separate `predicted_rating_today` for the next race. Do not confuse an adjusted historical performance with a projection at today's weight/conditions.
5. Backtest using 2024–2025 for calibration, 2026 chronological holdout, compare score and race ordering to baseline, and stratify by course, surface, distance and field size. Confirm absence of future-outcome leakage, including official HCP published after the subject race.
6. Show a dual-rating history during pilot: original manual ranking, candidate new absolute rating when calibrated, and explicit `not calibrated` otherwise. Class/going/pace exceptions get QA flags, not guessed figures.

## Stopping criteria
Do not deploy new rating scale until:
- time/weight raw inputs and manual override protections pass QA,
- enough anchored races exist for track variants,
- cross-track comparison works on independent held-out races,
- fractional score differences are stable and predictive,
- model, course, surface and projection semantics are documented.

Current live Race Studio is intentionally unchanged.
