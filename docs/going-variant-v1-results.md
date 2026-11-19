# Nordic Racing — Banekorrektion v1 (research, 18. november 2026)

## Resultat
- Input: historiske manuel-tid/rankings fra v86 og officielt handicap fra v43, ingen ændringer i nogen af kilderne.
- Grundtabellerne er eksisterende bane × underlag × distance-tider (v85_formula_reference.py).
- 2.422 løb har manuelle tider; 1.278 løb bestod de konservative filtre for sikker tabeldækning, officiel handicap på vinderen og troværdig tid.
- Kalibreret på 950 løb i 2024–2025, fordelt på 26 støtte-udsnit for bane/underlag/distance, hvoraf 934 har dækkede referencegrupper.
- Foreløbige løbsdagsestimeringer: 246.
- I 2026 er 63 dato/banekombinationer dækket. 51 har mindst middel datakvalitet (25 høj, 26 middel), 12 har lav/utilstrækkelig.
- På de 51 dage er median absolut afvigelse fra dine tidligere manuelle offsets 0,167 sekunder pr. 1.000 m. 49/51 er inden for 0,75 s/1.000 m. Korrelationen er 0,966. Dette måler overensstemmelse med en retrospektiv brugerbaseline, **ikke** automatisk race prediction accuracy eller reelle fysiske baneforhold.

## Sådan skal tallet forstås
+1,0 s/1.000 m: løbsdagen fremstår 1 sek. langsommere end en **historisk HCP-normaliseret** benchmark pr. 1.000 m. Tidskorrektion for 1.600m er 1,6 sek. i dette eksempel. Dette er en forskningsdefinition og ikke et verificeret going-label.

## Proces og sikkerhed
- En vinder pr. rent løb som reference; kræver verified manual time, officielt HCP registreret før løbet, samt troværdig vægt.
- Ekskludér løb markeret kunstigt/langsomt/uverificerbart og ekstreme tider. Beregn raceafvigelser fra kalibreret reference, tag robust median af flere løb, flag spredning og lav datadækning.
- Vægtjusteringen er **foreløbig den gamle 0,20 sek./kg**, fordi denne fase handler om banekorrektion, ikke om ny vægtmodel. Skal erstattes efter særskilt validering.
- Historisk manuelle offsets er brugt i *kalibreringsårene* 2024–2025, mens 2026 blev holdt udenfor og sammenlignet bagefter. Ingen læk fra 2026-offsets til modeltræning.
- Når et løb endnu ikke er afviklet, kan dets tid ikke bruges som banekorrektion til en før-løbsprognose. Pilotens anslag er derfor **retrospektive**, når flere løbsresultater er kendt.
- Mangler officielt going metadata; beskriv derfor ikke modellen som fast/blød bane som observeret fakta.
- Vores gamle 18.387 manuelle rankings forbliver uændrede. Intet er sat i drift på den aktive model.

## Visning og korrektur
- Åbn `Nordic_Racing_Banekorrektion_Research_v1.html` på GitHub Pages.
- Vælg løbsdag og se modelvurdering, del-løb, historiske offsets og datakvalitet.
- Ret korrektionen i 0,1 sek./1.000 m og skriv evt. kommentar. Gem lokalt, og hvis du er logget ind på Race Studio via samme browser, gemmes det også i Supabase under separate event_key værdier `track-variant|DATE|COURSE|SURFACE`.
- Der er eksport til CSV af dine manuelle valg.
- Kritisk: Der er ikke sket nogen automatisk bruger-godkendelse af modelvurderinger. Dine historiske faktiske rating-tider/offsets er ikke overskrevet.

## Originale maskinlæsbare filer
- `meeting_candidates.csv` — én række per dato/bane/underlag med score og kvalitetsniveau.
- `race_evidence.csv` — race-observationer bag estimeringen, se kildefilter.
- `audit.json` — maskinlæsbar QA, dækningsgrad og målinger.
- `build_going_v1.py` — reproducerbar kode. Kræver eksisterende source SQLite v86/v43 og v85_formula_reference.py i samme mappe; skriver kun til outputmappen.

## Begrænsninger
Dette er v1-forskning for banespecifik tidskorrektion, ikke en ny godkendt handicap-rating, prognose eller mål for banens fysiske fugtighed. Der mangler officiel going-/vejrmetadata, flere distancer og en fuld uafhængig resultattest. Browserens visuelle automatiske test var blokeret af kørselsmiljøet; JavaScript-syntaks og datastruktur er kontrolleret.

## Klampenborg 2026-10-17 — original `index` sheet verification

Directly read Google Sheet `index`: https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit (tabs `Races`, `Klampenborg - Græs`, `Ranking_Standards`). Spreadsheet formula `Races!K32330` is `=ARRAYFORMULA(IF(L32330="","",L32330 - ((M32330 - 59) * 0.2)))`; `Races!R32330` takes time-threshold match from `'Klampenborg - Græs'`, then adds `Races!D32330` as a **full rating-point offset**. This is *not* a seconds field and not four half-steps.

For this meeting 63 total starts across 8 races: 47 with offset `-4`, 11 blank, 2 at `-3.5`, 1 each at `-3`, `-2.5`, `-1.5`. Winners of races 1, 3–8 have offset `-4`; race 2 at 2800m has blank offset and a manually assessed winning score, separate from this calculation.

| Race | Distance | Winner | Manual seconds | K corrected seconds | Standard-table rating before offset | Offset | Original manual rating |
| --- | ---: | --- | ---: | ---: | ---: | ---: | ---: |
| 1 | 1200 | Biot | 76.0 | 75.2 | 5.5 | -4 | 1.5 |
| 3 | 1400 | Centurion Bling | 90.4 | 90.6 | 9.0 | -4 | 5.0 |
| 4 | 1800 | Wolis Hamoriko | 117.8 | 116.4 | 7.5 | -4 | 3.5 |
| 5 | 1800 | Mumbo Jumbo | 114.8 | 115.2 | 6.5 | -4 | 2.5 |
| 6 | 1800 | My Fortune | 114.2 | 114.1 | 6.0 | -4 | 2.0 |
| 7 | 1800 | Bianca | 118.1 | 117.5 | 8.0 | -4 | 4.0 |
| 8 | 1800 | Finn Ind Forever | 116.8 | 117.0 | 7.5 | -4 | 3.5 |

For the old standard-table increments, an offset of `-4` translates to removing roughly:
- 1200m: 8 half-steps × 0.5s = 4.0s = 3.333s/1000m
- 1400m: 8 × 0.6s = 4.8s = 3.429s/1000m
- 1800m: 8 × 0.8s = 6.4s = 3.556s/1000m

The current research algorithm suggested **+3.056s/1000m** based on six eligible winner performances, slightly *less* going slowdown than the historical manual roughly +3.33–3.56. This delta is a methodological audit target, not grounds to overwrite the historical -4. Do **not** call +3.056 the user's historical offset or confuse the sign of seconds/day versus signed legacy rank points.

**Revised model design:** match user's winner-first evaluation: compute per-race winner's verified manual time, old weight-normalized time, and distance-specific table rank; compare against an independently anchored *expected* pre-race performance level to infer the day's slowdown; robustly aggregate across multiple races, exclude races with no suitable benchmark or unreliable pacing; map the common physical slowdown back into race/distance-specific old rank shifts only for comparison. Never use the user's historical D offsets as a feature in holdout inference; they may calibrate training and evaluate errors only. Keep selected individual-horse exceptions and original manual inputs immutable. No live activation.
