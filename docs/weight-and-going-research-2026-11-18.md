# Vægtkorrektion og baneforhold — empirisk research, 18. november 2026

**Forskningsstatus: IKKE godkendt til live rating.** Ingen originale manuelle tider, gamle rankings, bruger-overskrivninger eller aktive Race Studio-beregninger er ændret.

## Motivation og kilder
- Eksisterende v86-historik: 18.387 oprindeligt manuelt rankede starter fra 2024–26, 2.422 løb. Alle rankede starter følger præcist `ranking_time_original = verified_manual_time_seconds + (59 - weight_original_kg)*0.20`. Den gamle formel **belønner tung vægt ens på samtlige distancer**.
- Originale tidsstandarder: brugerens Google Sheet `index`, banespecifikke tabeller, spejlet som `v85_formula_reference.py` i det historiske v86-arkiv.
- Officielle pre-race handicap-kilder er hentet fra v43 `off_hcp_by_start`. Der er 16.350 rankede rækker med officielt pre-race handicap >0.
- Ekstern dokumentation: [British Horseracing Authority – Performance Figures](https://www.britishhorseracing.com/regulation/performance-figures/) forklarer at vægt pr. længde varierer med distance, underlag/going, løbstid og afsluttende fart. Den genindsætter også lærlingelettelse i handicapvurderinger.

## Skeln mellem omregninger
- **HCP -> evneskala:** den bruger-godkendte MWP-inspirerede mapping, cirka 2 ratingpoint pr. officielt HCP-point (ikke strengt lineær i hele tabellen).
- **Vægt -> præstation:** ud fra brugerens MWP-tal (længder/kg)/(længder/ratingpoint) er ca. **1,43 ratingpoint/kg ved 1010m**, **1,375 ved 1200m**, **1,20 ved 1400m**, **1,077 ved 1600m**. Det er *ikke* 2 ratingpoint/kg.
- Med den midlertidige, ikke-validerede omregning 0,20 sekunder/længde bliver MWP-tal til 0,10, 0,11, 0,12 og 0,14 sekunder/kg; historisk system bruger 0,20 sekunder/kg overalt.
- **Vinderens rå manuelle tid skal aldrig vægtkorrigeres, før den sammenlignes med klassens faste banespecifikke standardtid.** Vægt/handicap indgår separat i forventet niveau og senere hestens standardiserede rating.

## Test 1: beskrivende vægtfordeling
2024–26, alle 18.387 rankede starter:

| Vægt | Andel sejre | Gennemsnitlig gammel ranking (lavere er bedre) |
|--|--:|--:|
| <54 kg | 9,1 % | 5,56 |
| 54–<58 kg | 11,9 % | 5,35 |
| 58–<62 kg | 13,6 % | 4,66 |
| 62–<66 kg | 14,2 % | 4,38 |
| >=66 kg | 14,5 % | 4,21 |

Disse er rå associationer; høj vægt kan reflektere højere faktisk evne og er ikke et bevis for vægtbias.

## Test 2: retrospektiv kronologisk fremtidssimulering
- Udgangspunkt: **12.683** manuelt rankede starter med komplet kurs-/underlags-/distance-mapping i de fem indlæste referencebaner. 8 ekstreme tidsobservationer ekskluderes **udelukkende til dette eksperiment** (bl.a. tider over 600 sekunder i kortere distancer); originalerne forbliver uændret.
- Predictor for et kommende løb: op til 3 **tidligere** manuelle præstationer fra samme registrerede hestenavn; generer genberegnet rating ved alternativ kg-koefficient, med samme tidligere baneoffset og standardtabeller. Den aktuelle start og senere tider indgår ikke i predictor.
- Sammenlign (c=0.20) vs (c=0.12) sek./kg; begge beregnes på samme kontinuerte referencegrad. Lavere formranking indikerer bedre chance.

| År | Parvis finish-rækkefølge ved 0,20 | Ved 0,12 | Vindende top-form ved 0,20 | Ved 0,12 | Parrer | Løb med vinderen rangeret |
|---|---:|---:|---:|---:|---:|---:|
| 2024 | 61,02 % | **61,58 %** | 28,73 % | **30,29 %** | 12.271 | 449 |
| 2025 | 60,65 % | **61,15 %** | 27,95 % | **29,27 %** | 14.444 | 533 |
| 2026 | 62,20 % | **62,46 %** | 28,96 % | 28,96 % | 11.815 | 442 |

Fremgang for 0,12 på parvis rækkefølge alle år, men små forskelle og ikke altid forbedret vinderprognose. **Dette er en retrospektiv simulering, ikke en registreret præ-løbsblindtest**: reference-tabellerne forelå ved analyseperiodens slutning, og navnebaseret hesteidentifikation skal QA-kontrolleres.

## Test 3: uafhængig, ikke-kausal kontrol
En udforskende to-vejs model med heste- og løbsindikatorer (12.481 brugbare starter efter ekstremværdi- og identifikationsfilter) giver omtrent 0,058 sek./kg 2024–25 og 0,077 sek./kg 2026. Distancesplit: <=1400m ca. 0,040, 1401–2000m ca. 0,081, >2000m ca. 0,102. Modellen kan **ikke identificere en kausal fysisk kg-effekt**: vægt afspejler ændringer i handicap, evne, form, klasse og rytter/tempo. Værdierne er plausibilitetssignaler, ikke basis for automatisk ny vægtformel.

## Klampenborg 17 oktober — Biot, korrigeret princip
- Officielt pre-start HCP **86** -> **123** på MWP-inspireret HCP-niveauskala.
- Båret/registrerede analysevægt **63 kg** -> på **1200m** foreløbigt (123 - 4*1.375 = 117.5) som vægtspecifik forventning (vis 118).
- **Rå manuel vindertid 76,0 sek.** mod klasse 2-standard **71,5 sek.**. Ingen forudgående vægtjustering.
- Med den eksplicit **usikre** antagelse om 0,20 sek./længde og 0,40 længder pr. ratingpoint bliver rå score (119-(76-71.5)/(0.20*0.40)=62.75) (vis 63).
- Foreløbig forskel (117.5-62.75=+54.75) -> **+55 nye ratingpoint**, **ikke godkendt baneoffset**. Det tidligere +54-resultat byggede på sammenblanding af HCP->rating og vægt->performance.
- **1800m:** der findes endnu ikke et bekræftet MWP-længder/kg-forhold. Løb 4, 5, 7, 8 kan derfor ikke opdateres præcist efter samme reviderede kg-logik uden ekstra kalibrering. Sidste rapports +48 median er ikke en godkendt korrektion.

## Baneforhold er en eksplicit kommende test
På blødere eller fastere baner kan sekunder/længde, længder/ratingpoint og længder/kg ændres. Indsaml først *uafhængige officielle* banebedømmelser og eventuelle numeriske going-målinger pr. løbsdag, og test interaktionerne `course × surface × distance × going` mod historiske manuelle tider. Klampenborg 17/10 var officielt '4,9 – blød', men ét møde kan ikke afsløre forskellen til fast bane.

**Vigtigt:** tidligere `ranking_offset` er brugerens tids-/klassebedømmelse, ikke en pålidelig erstatning for dokumenteret going. Ingen klassifikation af alle negative offsets som 'blød'.

## Beslutning før implementering
1. Fasthold gammel 0,20 sek./kg i publiceret model.
2. Kør isoleret pilot med 0,12 sek./kg og senere afstands-/going-afhængig kg→point, foreløbig uden ændring af gamle ratings.
3. For første godkendte løbsdag: hent officiel going og fuldt program, kræv manuelt godkendte tider, sammenhold handicap-forventning og klassens tidstabel, estimer +/− *ratingpoint* på tværs af løb, flag afvigere, lad bruger godkende før nye historiske ratings beregnes.
4. Bevar historiske 26 manuelle undtagelser og alle kildeposter.

Det reproducerbare skriptsæt og CSV-tabeller findes i research-ZIP lokalt oprettet i ChatGPT-kørslen.