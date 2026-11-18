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


## Confirmed design decisions — 2026-11-18
- **Keep existing track-specific time tables**, split by course × surface × distance. Do not replace them with a one-size-fits-all continuous par model. Upgrade the conversion of timed performance into finer rating points, using verified manual source times.
- **Use a meeting-specific going/time allowance** for firm/good/soft/heavy days. The official going description is an initial categorical input; validate the actual clock-speed effect with multiple races on the card and known historic standards. Do not infer a whole-day offset from one tactical/slowly run race.
- Treat going as a `meeting × surface` rating correction with optional distance-family/track-section departures if data support them. Express the correction primarily in **signed ranking/rating points**, not a blanket seconds-per-1000m adjustment. Consult course × surface × distance-specific standard-time-to-points conversion; flag insufficient and mixed evidence.
- **Display final rating as integer only**, e.g. 121, not 121.4. Compute with full precision internally and round **only at the end** (prefer documented deterministic rounding), not at each intermediate stage.
- **High = better** in the new rating. User's observed Mr World Pool 121 ≈ official HCP 83.5 is a single illustrative anchor, not a constant mapping.
- Preserve old ranking (0–12 half-step, low=better), manually timed results, user overrides, sync values, and original model unchanged during research. A new `v2_rating_integer` is separate.
- Distinguish **historical performance ratings computed after the meeting** (going allowance may use the day's race times) from **pre-race projections** (must only use information available before the respective race; never use same-day future results).
- Later compare two day-correction candidates: A) categorical going-only, B) categorical + robust meeting-time variant; stratify on course, surface, distance and validate by chronological holdouts. Keep B only if out-of-sample improvement is demonstrated.


## Confirmed revision — 2026-11-18: winner raw-time versus handicap-anchored expectation
Source read: Connected Google Sheet `index` spreadsheet ID `1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8`, tab `Handicap` (gid=1329435406): grade 2 => "22-26", interpreted using user's signed class convention as −22 to −26. User example: official HCP 83.5, weight 59kg -> W−H = −24.5 -> class 2, *illustrative* MWP-like expected score about 121 at standard conditions.

**Corrected approach supersedes any earlier instruction to normalize winner's manual time to 59 kg before consulting the class standard table:**
1. Compare winner's **unadjusted verified manual race time** directly to course × turf/dirt × distance **fixed class winner-time standards**, whose standard does not vary with winner's actual carried weight.
2. Separately construct the **expected 59kg-equivalent class / target performance rating**, using *pre-race* official handicap plus race's declared weights; ensure no apprentice-claim ambiguity. User's current signed proxy for an individual horse is `carried_weight_kg - official_pre_start_hcp`, with −24.5 indicating a class-2 reference. The original single example 121↔HCP83.5 is a provisional anchor, *not* an established general mapping.
3. Convert raw time-versus-standard into provisional **integer-scale observed score**, with a *fractional* internal value before last-step rounding. If expected 121 and observed 116, the preliminary shortfall is `+5 rating points of required positive going correction`.
4. Estimate the `meeting × surface` going/day variant **in ranking/rating points** from multiple races (winner-first, considering other runners where reliable). Use a robust central estimate of `expected_rating − observed_raw_time_rating`, after each race has been evaluated against its own course × surface × distance standards and handicap-anchored expected level. Stratify/split by distance family where the point gaps differ systematically; do **not** impose universal seconds per 1000 m or assume long- and short-distance pace is proportional. Flag tactical pace, unreliable winners, 2yo/maiden, implausible HCP, non-comparable distances, and insufficient races. Calibrate no double-counting of weight.
5. Provisional score for each horse = **observed** raw-time score + estimated **same-day correction** on corresponding distance, then apply correctly defined horse-level weight/race performance adjustments separately if needed for a published 59kg-equivalent figure; prevent double counting. Keep *observed* and *standardized* ratings distinct.
6. Display: per-race expected level, raw score, **signed point difference** and confidence/exclusion reason; per-day proposed **+/− rating correction** and, where supported, distance-specific departures; permit user override and capture model/user values with provenance. Time differences can remain an internal diagnostic but are not the user-facing going unit.
7. The proposed +/− day correction is a **robust summary of race-level rating gaps**, not a blind uniform time adjustment; inspect short/long-distance residuals and separate or exclude non-comparable races. A race-time gap can reflect pace or horse ability, not only going; evaluate on chronological holdouts.

No live model or original manual time/rating data changes.


## Agreed race-day operating workflow — manual timings and point-based going (2026-11-18)
This section **supersedes** any earlier draft references to using a universal seconds-per-1000m day correction or relying on official times as the definitive timed performance.

1. **Assistant prepares the meeting:** collect all official material in advance/after results as available: programme, date, race distance, surface/going, class, runner IDs, pre-race HCP, assigned/base weight and apprentice allowance separately, results, **official recorded times**, scratched runners, and source links. Mark missing/unverified fields. Official timing is for preliminary context and discrepancy checks, **not a substitute** for manually verified times.
2. **User checks and supplies/approves manual times** for the races; these are the authoritative timed inputs for the rating pilot. Never silently promote official times to manual verified. Retain manual time provenance and version.
3. **Model analyzes** manual winners' *raw unadjusted* times against course × surface × distance × relevant class standard, with independently anchored expected level from the contemporaneous handicap profile. The actual weight does not change the fixed standard winner time. Weight can inform expected-level conversion and later horse-specific standardized rating, without double counting.
4. **Model calculates a preliminary signed correction in rating points for each race**, then a robust meeting correction in **+/− ranking/rating points**; short versus long distances use their distinct time-to-rating conversion tables and are checked for systematic differences, rather than assuming 1000m and 2800m pace scale linearly. Avoid over-weighting races with tiny or anomalous fields. Show both model proposal and constituent race differences.
5. **Flag unusual races**, e.g. tactical pace, unreliable timing, unexpected winning class strength, maiden/juvenile races or extreme distances, as possible exclusions with an explicit reason. Do not remove automatically without recording why.
6. **User reviews** and accepts or adjusts the per-race exclusions and proposed overall **+/− points correction**, optionally distance-family-specific if evidence supports it. Store model candidate, user override, timestamp, author and reason.
7. **After approval**, calculate new *candidate* historic integer performance ratings; preserve all legacy 0–12 rankings, the old negative `ranking_offset`, original times and approved exceptional overrides. Do **not** activate live ranking until independent validation passes.

**Sign convention:** new v2 higher-is-better observed score 116 versus expected 121 → proposed going improvement **+5 new rating points**. In legacy low-is-better ranking, a slow day commonly used a **negative** offset (e.g. `−4`); signs **cannot be copied** between the two scales. Show the old vs new convention explicitly when comparing. The user-facing going control is points, **not seconds/1000m**. The new point-based correction must still be validated across distances.

**Future aspiration only:** automation may later extract reliably verifiable manual-equivalent times directly from race video or other sources. Until experimentally demonstrated, human checked times are required. No change to the live Race Studio scoring or existing cross-device edits in this phase.
