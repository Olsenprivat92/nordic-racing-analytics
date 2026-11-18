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