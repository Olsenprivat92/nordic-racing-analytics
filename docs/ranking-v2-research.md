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


## Empirical weight-bias backtest and going interaction hypotheses (2026-11-18)

Research-only audit of v86 manual ratings (18,387 manually validated rankings; unchanged). Source code and detailed results available in local reproducible package `Nordic_Racing_Vaegt_og_Baneforhold_Research_v1.zip`. Important distinction: race-time **going calibration compares raw, not weight-normalized, winner times** to class/distance standards; an individual-horse 59kg-equivalent historical performance rating may apply a *separate, calibrated* kg effect afterward.

Legacy ranking-time weight coefficient = **0.20 seconds/kg on every distance**. User suspects systematic overstatement for heavy-carried-weight horses; heavy-weight runners also win more often. The latter is expected confounding by assigned HCP and class, so do not infer the correct physical kg effect from naive winning percentages.

Retrospective chronological candidate comparison: 12,675 qualified graded horse starts after 8 research-only extreme-time exclusions (five courses with exact old standard curves). Each new race predicts from mean previous up to three rated runs **strictly earlier than race date**; no same-race outcome in predictors. However previous manually chosen meeting offsets are available, later course standards may contaminate true historical knowledge, and name matching/identity quality has limitations. This is **not yet a fully blind forward test**. Evaluation only races with at least three history-rated runners; all candidate coefficients evaluated on same horse-pairs.

| 2026 holdout metric | Existing 0.20 s/kg | Candidate 0.12 s/kg | Difference |
|---|---:|---:|---:|
| Pairwise correct ordering (11,815 pairs, 468 races) | 62.201% | 62.459% | +0.258 percentage points |
| Top-form candidate wins (442 races where winner history-rated) | 28.959% | 28.959% | no difference |

In-sample (historical, 2024/2025) paired concordance 0.12 vs 0.20: 61.576% vs 61.022% (2024) and 61.150% vs 60.648% (2025). The 2026 holdout favors smaller coefficients only marginally; **0.00 s/kg is also competitive** (2026 62.548% pairwise), so **0.12 is a research hypothesis, not a validated unique optimum**. Year-by-year win rate has non-monotonic behavior. Preserve baseline and evaluate uncertainty and independent future fixture data.

An exploratory race-and-horse fixed-effects model (12,481 starts, 1,330 horses, 1,673 races) estimated conditional *association* ~0.058 seconds/kg; by distance: <=1400 m ~0.040; 1401–2000m ~0.081; >2000m ~0.102. This is **not causally identified**; pre-race HCP, form, going, tactical pace, and changing distances matter. Use only to inform candidate ranges and systematic checks.

User-supplied MWP length/kg values at 1010,1200,1400,1600m correspond to **0.10 / 0.11 / 0.12 / 0.14 s/kg**, *if* one assumes 0.20 s/length; this seconds-per-length assumption is **not yet calibrated**. In new point scale, e.g. 1200m weight effect `0.55 / 0.40 = 1.375 rating points/kg`, which is **not identical** to 2 ratingpoints/off-HCP-point (ability-scale mapping). Avoid mixing these interpretations.

**Going hypothesis to test, not established:** `lengths per ratingpoint`, `lengths per kg`, `seconds per length` may change on soft/heavy going compared with firm. Do NOT use historical manual day offset as a proxy for *official going*, and do not infer effects from a single soft fixture. Collect official ground readings, surface, course, date, pace and distance strata, then test `weight × going` and `distance × going` interactions with chronologically held out meetings. Prioritize comparing performance within same race and horse (with HCP controls where possible), followed by out-of-sample predictive gain. Protect original manual times and overrides.

Klampenborg Oct 17 example revision: Biot official pre-HCP86, assigned weight63. MWP(HCP86)=123, while **weight performance adjustment** at 1200m is `(63-59)*1.375=5.5 points`, yielding nominal expected at carried weight **117.5 ≈ 118** rather than **117**, which came from treating HCP-point ↔ MWP mapping as a weight effect. Raw uncorrected time performance, using provisional seconds/length, remains ~62.75 ≈ 63. Thus an illustrative implied +55 model point gap, **not a validated going correction**. For 1800m, MWP lengths/kg are not yet established; don't invent a precise coefficient.

Implementation gates: 1) calibrate time-per-length against independently checked manual finish times/placements by distance/surface/going, 2) estimate going interactions from officially recorded ground state across multiple race days, 3) pick weight coefficient using training years only and test on untouched later dates, 4) compare win and pairwise rank outcomes against old method; 5) only then consider new historical integer rating conversion or live rollout.


## 2026 Klampenborg winner-clock / official going empirical checkpoint
See [2026 going and weight validation](klampenborg-2026-going-and-weight-v2-validation.md) for the worked proof and reproducer.

**Confirmed, no weight adjustment before winner-time/table comparison:** with 5 matching handicap winners on Klampenborg 17 October, distance-specific legacy time table implies **−4.25 old ranking points** versus user's original **−4.0**. Winner clock and class/time table alone, no legacy offset model input.

Across 15 officially measured 2026 Klampenborg dates (907 manually timed starts / 122 races), 53 eligible winner-time standards produce day suggestions with mean absolute difference **0.378 legacy points** versus user's historic day offsets; 11/15 within 0.5 and all 15 within 1.0. This validates reproducing the *old workflow*, not new predictive accuracy.

**Official going is now grounded for 15 dates** in Dansk Galop's report, numerical going 3.0–5.0. Raw time vs class standard *without old offsets* has medians +2.05s (good/light), +3.40s (mixed) and +5.80s (soft/deep). The new going vs kg interaction remains inconclusive; overlapping race-cluster uncertainties.

**Kg holdout (2026):** legacy .20 s/kg 62.192% vs research .12 s/kg 62.442% for pairwise finish order, improvement +0.250 percentage points (95% race bootstrap CI −0.153 to +0.689); no statistically established win. Distance-varying candidate trained on 2024–25 did not improve 2026 relative to fixed 0.12.

**DO NOT directly map −4.25 old points to a fixed NEW-point correction.** The current handicap class-step to MWP-rating relation and unvalidated seconds/length conversion imply incompatible seconds per NEW rating point; use new integer scores only after separate empirical calibration. Keep live mode and historical manual inputs unchanged.


## OVERRIDING model decision: NEW rating points, distance-corrected weight, NO official going measurements (2026-11-18)
**This supersedes all prior drafts that proposed showing or fitting a legacy 0–11 point day-offset in the rating-v2 workflow, or using official going-stick/going-number measurements for variant inference.** The user explicitly rejected both. The v2 going correction must be computed directly on the new MWP-inspired **higher-is-better** integer rating scale. Existing legacy offsets remain immutable archival data *only*, not inputs to the v2 correction model. Similarly official going numbers are not inputs, labels, priors, or validation targets for v2. They may be preserved in raw meeting metadata, but must not influence correction.

**Distance-aware kg effect:** MWP-confirmed length/kg: 1010m .50; 1200m .55; 1400m .60; 1600m .70. Corresponding length/new-rating-point .35, .40, .50, .65. For 1800m and beyond length/kg is NOT yet user-confirmed; use sensitivity scenarios with prominent uncertainty (1800m temporary .75, interpolate .725 length/new-rating-point between 1600 .65 and 2000 .80). Do not apply uniform .20 sec/kg.

**New direct pilot, Klampenborg 17 October 2026:** Use verified raw manual winner time compared to fixed class time at course+surface+distance (no pre-weight adjustment). Expected new rating `R(official_pre_race_hcp) - (analysis_base_kg-59)*lengths_per_kg/lengths_per_new_ratingpoint`. Raw observed new rating `R(numeric_analysis_class_midpoint_hcp) - (manual_seconds - class_standard_seconds)/[(2.50m*manual_seconds/distance_m)*lengths_per_new_ratingpoint]`. Then race correction = expected minus raw, day proposal = median across five valid handicap races. Assumed effective length 2.50m is *not measured*, and total race average speed may differ from speed at the finish; sensitivity 2.35–2.70m. No official going values or legacy negative offset used.

Preliminary NEW-point calculations (round only for display):
- R1 Biot 1200m: expected 117.50, raw 47.95, suggested +69.55 ≈ **+70**.
- R4 Wolis Hamoriko 1800m: expected 83.76, raw 16.99, +66.77 ≈ **+67**.
- R5 Mumbo Jumbo 1800m: expected 107.07, raw 52.64, +54.43 ≈ **+54**.
- R7 Bianca 1800m: expected 63.90, raw 4.07, +59.83 ≈ **+60**.
- R8 Finn Ind Forever 1800m: expected 86.03, raw 29.18, +56.85 ≈ **+57**.
- **Median +59.83 -> +60 NEW rating points**. Sensitivity for assumed effective length 2.35–2.70m and 1800m weight factor .70–.80 lengths/kg: approx **+56..+63 NEW points**. It is a *research proposal*, not an approved track variant; original 2026 race data unmodified. R2 lacks 2800m class standard; R3 2yo winner no HCP; R6 nonnumeric class — exclude with reasons.

**Additional distance-specific kg holdout**: re-rank each past manually timed performance using its own race distance and time: `secPerKg ≈ effective_length_m * manual_time_sec / distance_m * lengths_per_kg(distance)`. The lengths/kg estimates above 1600m are unverified extrapolations, not new empirical facts. 2026 next-start out-of-sample pairwise finish order: 0.20 sec/kg baseline 62.192% vs fixed .12 sec/kg 62.442% vs distance+speed proxy 62.425% over 11,815 pairs / 468 races; distance proxy gain +.233 percentage points, race bootstrap 95% CI approx −.232..+.707, **not statistically significant**. For pairs using only 1010–1600m prior MWP-confirmed distances, 62.883% vs 63.075%. Users should not interpret these as causally measured kg effects or a final weight factor.

**Output available:** separate public research review `https://olsenprivat92.github.io/nordic-racing-analytics/klampenborg-new-rating-v2-review.html`. It has a slider for effective length and 1800m kg assumption, exclusion toggles, proposed +/− NEW rating points, local-only manual override and JSON export. **No sync to Supabase and no changes to active Race Studio.** It is a calibrated research UI, not the production rating engine.

**Further calibration needed:** physical length/time conversion using independent end-of-race margins or sectionals; robust pace outlier exclusions; more dates for distance bands and independent horse-class race standards; reliability of numeric class HCP midpoint to rating. The model may be adjusted before approved output.

## Dependency before further v2 calibration: audit course × distance bias in legacy ratings (2026-11-19)
Per user direction, investigate whether old ranking is systematically easier/harder to obtain at certain courses/distances **before** setting the new absolute performance calibration. Research is in [legacy course/distance audit](legacy-ranking-course-distance-bias-2024-2026.md).

In 9,592 manual-ranked 2024–26 starts from 1,140 horses, with numeric race class and verified pre-start official handicap, a **within-horse** fixed effects comparison controlling handicap/class/finish percentile/weight/age/year shows:
- Göteborg turf 2,200 m worse (higher old rank) than 1,400 m by about +0.77 old points, same sign all 3 years.
- Jægersro dirt 1,200 m worse than 1,600 m by about +0.69 old points, same sign all 3 years.
- Øvrevoll dirt 1,600 m worse than 1,100 m by about +0.39 old points, same sign all 3 years.
- Other contrasts are less stable by year; no blanket automatic normalization.

**Use legacy points for the diagnostic audit only.** The v2 production design stays MWP-inspired higher-is-better whole rating numbers. Do not transplant old relative biases or −4 meeting offsets into the v2 numerical unit. Keep manual times and official pre-race HCP sources, **do not use official going measurements as a correction input**, maintain distance-specific weights, assess race-day going in **new points** and solicit user's approval before applying any correction.

Next quality gate: review standards and pace/track preferences for those three reproducible contrasts, evaluate whether recalibrating base course-distance time standards produces more stable rating equivalence in held-out 2026 days. Leave original raw/ranked data untouched.


## 2026-11-19 user notes to revisit AFTER standard-table audit: distances, class steps, length and kg
The user has explicitly asked to **record, not yet act on**, these two observations while the current standard-time audit continues:
1. **Klampenborg turf 1,100m seems far too easy to achieve a good legacy ranking**. After finishing the current round of course × handicap-class standard-time adjustments, conduct a systematic **within-course comparison of every distance**, including Klampenborg 1,100m. Its current numeric-handicap 2024–26 sample is only **3 races / 15 top-5 starters**, so do not pre-emptively change it.
2. The user observes the following **seconds per adjacent half-class/grade** in their existing Klampenborg standard times: 1,100–1,300m **0.5s**, 1,400m **0.6s**, 1,600m **0.7s**, 1,800m **0.8s**, 2,200m **0.9s**, 2,400m **1.0s**. They hypothesize a potentially valuable connection to **lengths-per-kg**, saying (conceptually) about 0.5 lengths/kg at 1,100–1,300m and 1 length/kg at 2,400m. **Bring this observation back up when calibrating distance/weight/MWP conversion**. It is an interesting hypothesis **not an established mathematical equality**: the table column increment is *seconds per 0.5 old rank/grade*, while length/kg is a physical/handicap scale; they have different dimensions and must be validated with separate distance-specific seconds/length. Do not silently infer seconds == lengths or make an automatic kg update.
3. User says they updated **Göteborg 1,600m +0.2sec and 2,400m +0.4sec** (relative to frozen original standard). Respect their expressed intent; **verify actual current live Google Sheet values before analyzing**, since a prior read showed opposite deltas (+0.4 at 1600 and +0.2 at 2400). Do not repeat a +0.2 recommendation for 2400 if +0.4 is already present.
4. **Keep weight effects and MWP out of the current standard-table audit**. Continue using original manual times, original recorded day offsets and ordinary numeric handicap races, examining all starters / top 5 / winners by class, year and within-track distance; present proposals for approval. Do not edit source sheets or original ranking history.


## Pace-aware eligibility before further standard-time calibration (2026-11-19)
User insight: some races are tactically extraordinarily slow, and their **"Langsomt løb"** or **"Kunstigt løb"** comments should probably mean the race **must not determine the normal-distance standard**. This must be a race-level selection rule in the calibration review, **not a deletion of horse times, recorded old rankings or original day offsets**. See the [pace-annotation audit](race-pace-exclusion-audit-2026-11-19.md).

In 10,566 manually ranked standard handicap starts, explicit source comments mark **103 unique races** as candidate unusual pace (37 slow, 65 artificial, plus other overpaced), together **740 starters and 500 top-5**. An independent *time unverifiable* flag affects **32 races**. Removing flagged races from the **frozen historic old scores** changes some distance-level mean ranks materially: e.g. Göteborg turf 2400 4.26→3.83, Aarhus turf 2000 4.82→4.59. These are pre-16-adjustment screening values; rerun all approved current standards with exclusions before recommending further modifications.

Important QA: **Aarhus 2024-06-29 race 9** is explicitly marked "Kunstigt løb" by all six starters; the other anomalous Aarhus **2024-05-05 race 4** has no pace note, so flag for manual outlier review rather than assuming normal. Individual "langsom fra start" must not exclude the whole race. For new MWP meeting-wide variant estimation, do not let tactical pace masquerade as the day's racing surface speed; no official going measurements are used.


## Approved calibration filter: exclude slow/artificial RACES (2026-11-19)
User explicitly decided that all entire races with manual comments **\"Langsomt løb\"** (including number-prefixed variants) or **\"Kunstigt løb\"** must be excluded from **standard time calibration** across ALL tracks/distances/classes. Do **not** delete individual starts, manually verified times, original scores or existing offsets. Individual horse-only slow starts do not mark the entire race. Original 2024–2026 numerical handicap cohort: 1,327 races and 10,566 starts; precisely **102 distinct races**, 733 starts and 495 top-five starts excluded; remaining **1,225 races / 9,833 starts / 6,082 top-five**. The earlier 103 includes one further overpaced note **not** in user's exact exclusion. Separate \"Tiden kan ikke verificeres\" QA not automatically excluded.

Re-evaluated 16 approved current Google Sheet table updates covering 15 distinct track/distance rows. On this filtered historical cohort, 14 of 15 updates reduce the absolute adjusted within-track distance residual; **Göteborg turf 2400m +0.4 sec** now over-corrects and should be reconsidered (filtered local -0.185 old points, return -0.2sec to +0.2total yields approx -0.085). Other candidate: **Øvrevoll turf1170m +0.1s**, filtered local +0.401→+0.301 (26 races) and same-horse test supports direction. **Do not automatically change live tables.** See [full filtered research](pace-filtered-review-after-sixteen-standard-time-edits-2026-11-19.md). Check numeric/age/ordinary handicap scope, year/class counts, same-day and same-horse evidence before next proposal. No fresh weight/MWP adjustment or official going inputs in this phase. For eventual MWP meeting variant, keep unusual tactical pace distinct from daily track speed and exclude confirmed slow/artificial race from the meeting correction consensus (not from historical horse starts).
