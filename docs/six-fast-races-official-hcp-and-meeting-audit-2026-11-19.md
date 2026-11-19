# Nordic Racing — seks hurtige handicapløb: kilde-, klasse- og løbsdagskontrol

**19. november 2026 · Forskningskontrol – ingen ændringer af levende Google Sheets, 18 godkendte standardtidstabeller, manuelle tider, historiske rankings eller offsets.**

## Beslutningsgrundlag

Gennemgangen viderefører den godkendte analyse med **9.833 starter og 1.225 almindelige numeriske handicapløb i 2024–2026**, efter at **102 hele løb** med brugerens "Langsomt løb" eller "Kunstigt løb" er udeladt fra *kalibrering* (men bevaret i original historik). De seks udvalgte hurtige løb er stadig med, fordi hverken en tempoadvarsel eller en konkret tidsfejl er påvist.

**Hovedfund:** Bro Park dirt 1200 m i brugerens interne *raceklasse 4* har afvigelse **−0,580 gamle rankingpoint** mod klasse 4 på banens andre distancer. Hvis de tre på forhånd udpegede ekstremt hurtige løb **kun som en følsomhedstest** holdes ude, bliver afvigelsen **−0,078** på de resterende fire løb (20 top 5). For Øvrevoll dirt 1100 m raceklasse 5 er den tilsvarende ændring fra **−0,674** (14 løb) til **−0,453** (11 løb). Her findes altså et bredere mønster. **Der er ikke belæg for at ekskludere nogen af de seks**, og de historiske scoretal skal stå.

## De seks løb med aktuelle godkendte standardtider

| Bane · dato · løb i ark | Intern klasse | Vinder (manueltid) | Top 5-gns. gammel ranking | Justeret afvigelse mod klassebane | Afvigelse mod andre distancer *samme dag* | Top 5-gns. officielt formtal ved start |
|---|---:|---|---:|---:|---:|---:|
| Bro Park dirt, 20-10-2024, nr. 1 | 4 | Chinese Emperor (74,7 s) | 3,10 | −1,39 | −0,91 | 66,6 |
| Bro Park dirt, 14-09-2025, nr. 4 | 4 | Bang A Boomerang (72,7 s) | 3,30 | −1,33 | −1,58 | 65,2 |
| Bro Park dirt, 16-11-2025, nr. 3 | 4 | Forward Focus (74,1 s) | 3,30 | −1,33 | −1,31 | 64,8 |
| Øvrevoll dirt, 25-04-2024, nr. 7 | 5 | Clapper (69,5 s) | 3,50 | −1,64 | −1,38 | 52,8 |
| Øvrevoll dirt, 06-11-2025, nr. 6 | 5 | Stogas Athena (69,4 s) | 3,90 | −1,17 | −1,30 | 51,2 |
| Øvrevoll dirt, 01-10-2026, nr. 3 | 5 | Emmeline (69,9 s) | 4,10 | −1,10 | −1,51 | 53,2 |

*Negative gamle rankingpoint betyder hurtigere/bedre end den sammenlignede reference. Løbsdagsreference består af andre **almindelige, normaltempo-handicapløb på andre distancer** samme dag og er ikke altid præcis samme handicapklasse. Hestestart- og årskontrol er i den allerede dokumenterede 18-rettelsesmodel.*

## 1. Kontrol af manuelle kilder og konkrete tider

- Alle seks løb findes i **brugerens levende `index/Races`-ark**, og de udvalgte rækker matcher den arkiverede kildedatabase i dato, nummer, distance, klasse, heste, manueltid og historisk offset. Samtlige **47 hestestarter** har et verificeret manuelt tidsfelt og et dokumenteret **officielt handicapformtal før start** i arkivet. Ingen af de seks løb har bemærkningen om ikke-verificerbar tid, langsomt løb eller kunstigt løb.
- Bro Park 2024 har offset **0**, Bro Park 2025-dagene **+0,5** pr. registreret hest, Øvrevoll 2024 og 2025 **0**; de tomme 2026-offsets behandles som **0** i modellen, uden at der skrives i arket.
- Resultatlisterne for Øvrevoll viser vinder 2024-04-25 **69,5 s**, 2025-11-06 **69,3 s**, 2026-10-01 **69,6 s**; brugerens manuelle tider er **69,5 / 69,4 / 69,9 s**. Afvigelser på 0/0,1/0,3 s er **ikke dokumentation for fejl** – brugeren har eksplicit valgt sine manuelle tider frem for de officielt registrerede, der kan være upålidelige. Ingen ændring foretages.
- I det officielle svenske startprogram **16-11-2025** hedder 1200m med Forward Focus og Sharp Eye **"Lopp 4: KLASS 5 HANDICAP"**, mens det hedder **løb 3 med intern raceklasse 4** i brugerens ark. **Hestene og distancen matcher**. Løbsnummerforskydningen hænger sammen med, at det officielle program også indeholder et tidligere SARA/araberløb, som ikke er i det aktuelle ark. **Den interne raceklasse er en brugertilpasset skala, ikke samme tal som den svenske officielle "Klass 5".** Kontrollér mapping ved andre kilder, men omklassificér ikke automatisk.

## 2. Løbsdagsforklaring

- **Bro Park 20-10-2024:** Klasse 4-sprinten ligger −0,91 gamle point mod øvrige distancer på mødet. Der er også klasse 4 på 1600 m (residual −0,59), men 1200 m er markant hurtigere (−1,39). Det er ikke ensbetydende med en generel klassekurvefejl.
- **Bro Park 14-09-2025:** Klasse 4-sprinten (−1,33) er markant hurtigere end gennemsnittet af de øvrige handicapdistancer samme dag (+0,25). Vinderen er noteret "Overlegen", men *en overlegen hest* er ikke et kunstigt løb.
- **Bro Park 16-11-2025:** To 1200m-handicaps er begge meget hurtige i modellen: intern klasse 4, arkets løb 3 (**−1,33**) og klasse 3,5, arkets løb 4 (**−1,45**), mens mødedagens 1600/2100m normale løb ligger omkring **+0,09 / −0,14**. **Det er derfor ikke kun klasse 4, som afviger den dag**. Undersøg en potentiel distance-/start-/løbsdagsfaktor før ændring af klassekurven.
- **Øvrevoll 25-04-2024:** Klasse 5 på 1100 m (−1,64) er specielt hurtig. 1100m klasse 3 samme møde er næsten neutral (−0,04), og 1600m klasse 4 er −0,58. Det taler for både klasse- og løbsspecifik variation.
- **Øvrevoll 06-11-2025:** Klasse 5 på 1100 m er **−1,17**, men **klasse 5 på 2400 m samme dag +0,72**. Kontrasten på cirka **−1,89** gamle point mellem samme interne raceklasse er stor og kan ikke tilskrives en ensartet dagsoffset.
- **Øvrevoll 01-10-2026:** Klasse 5 på 1100 m **−1,10**, mens **klasse 5 på 1750 m samme dag +0,90** (kontrast −2,00). Også 1100m klasse 3,5 er hurtig (−0,73). En forklaring alene med klasse 5 er derfor utilstrækkelig.

## 2b. Sprintbanens særlige løbsdage — sammenlignet med andre møder

For hvert møde i det **filtrerede** datamateriale er de normale 1200/1100-meterløbs gennemsnitlige justerede residual sammenlignet med **andre distancer samme løbsdag**. Her tæller et møde kun én gang, uanset hvor mange sprinterløb det indeholder.

- **Bro Park dirt 1200 m:** 30 sammenlignelige løbsdage, median sprint-minus-øvrige distancer **−0,30** gamle point. **14. september 2025 (−1,58)** er det mest negative møde (**1/30**); **16. november 2025 (−1,37)** det næstmest negative (**2/30**), og der var to hurtige 1200m-løb samme dag. **20. oktober 2024 (−0,40)** ligger derimod midt i fordelingen (14/30). Det taler for **enkelte sprint-specifikke løbsdagsforhold i 2025**, ikke et kronisk problem på enhver 1200m-dag.
- **Øvrevoll dirt 1100 m:** 39 sammenlignelige møder, median **−0,35**. **1. oktober 2026 (−1,33)** er næstmest ekstrem (**2/39**); **6. november 2025 (−0,65)** er omkring 10/39, og **25. april 2024 (−0,58)** er omkring 16/39. Den udvalgte 2026-dag er særskilt usædvanlig, men den generelle 1100m-forskel kan ikke alene forklares af disse tre datoer.

**Fortolkningsgrænse:** Samme-dags-kontrasten kontrollerer ikke fuldt for hestepopulation eller forskel på afviklet tempo i den længere distance. Den siger **ikke**, at banen fysisk var hurtigere i sprintløbene, eller at noget bestemt løb er kunstigt. Den skal bruges som signal om, hvor manuel video-/tidsgennemgang giver mest værdi. Se `10_sprint_vs_other_distances_by_meeting.csv`.

## 3. Hestenes officielle handicapformtal (ingen vægtmodel)

Officielle *før-start-formtal* fra projektets v43-kildedatabase er brugt rent **diagnostisk**, ikke til at genestimere kilo eller ændre gamle rankings. For hver af de seks løb havde top 5-hestene gennemsnitlige formtal som følger:

| Hurtigt løb | Formtal i dette løb | Andre distancer, samme interne raceklasse og år | Forskel |
|---|---:|---:|---:|
| Bro Park 20-10-2024 klasse 4 | 66,6 | 63,1 | **+3,5** |
| Bro Park 14-09-2025 klasse 4 | 65,2 | 64,5 | +0,7 |
| Bro Park 16-11-2025 klasse 4 | 64,8 | 64,5 | +0,3 |
| Øvrevoll 25-04-2024 klasse 5 | 52,8 | 50,4 | **+2,4** |
| Øvrevoll 06-11-2025 klasse 5 | 51,2 | 51,6 | −0,4 |
| Øvrevoll 01-10-2026 klasse 5 | 53,2 | 48,6 | **+4,6** |

Højere formtal er et signal om stærkere heste, men er ikke årsagsbevis. I en *eksplorativ løbsniveau-regression* for de to klasser går det ubetingede sprint-led fra **−0,58 til −0,49** (Bro Park klasse 4, 25 løb) og fra **−0,67 til −0,57** (Øvrevoll klasse 5, 36 løb), når løbenes gennemsnitlige officielle formtal indgår. Ved yderligere årskontrol er Bro Park-estimatet derimod **−0,74** – et tegn på model-/årsfølsomhed ved små grupper. Der er altså **en vis sammensætningseffekt, men ikke en fuld forklaring**. Tallene er ikke en ny rating eller vægtfaktor.

## 4. Gentagne heste og statistisk uafhængighed

- **Bro Park 14-09-2025 og 16-11-2025:** **Forward Focus, Forward Fun og Sharp Eye** er top 5 i begge hurtige klasse-4-løb. Hændelserne er selvstændige løb, men de repræsenterer delvis **samme hurtige hestekohorte**. Desuden deltager Cara Dune i det hurtige løb 20-10-2024 og igen 16-11-2025.
- **Øvrevoll 06-11-2025 og 01-10-2026:** Emmeline og Heia Pingu er begge top 5 begge dage; Stogas Athena og Price Of Joy går også igen. 2024 og 2025 deler Hope And Glory og Oliver.
- Dette reducerer hvor godt vi kan fortolke løbene som uafhængige stikprøver af *forskellige heste*. Løbsniveau-bootstrap fra den tidligere klassekurvekontrol er stadig en nyttig, men ikke komplet, usikkerhedsmodel.

## 5. Konklusion og næste forskningstrin

1. **Behold alle 18 brugergodkendte standardtidsrettelser.** Ingen af de seks normale løb må udelades alene, fordi de er hurtige.
2. **Ingen generel ændring fra 0,50 s per halve gamle rankingtrin** på Bro Park 1200m eller Øvrevoll 1100m endnu. Det ville påvirke flere raceklasser og forværre visse år.
3. Lav en særskilt **løbsdags-/sprint-distancekontrol** for Bro Park 16-11-2025, hvor to 1200m-løb afviger ens, og Øvrevoll 2025-11-06 / 2026-10-01, hvor 1100m og den længere klasse-5-distance adskiller sig kraftigt. Kontrollér manualtidskilden (ikke automatisk de officielle tider), hestestyrke og race-pace-kommentarer. Hvis der ikke findes flere sikre kommentarer, behold løbene som normale.
4. Ved næste større analyse: test om **raceklasse × distance** har stabile relationer på nye år, **uden at bruge data til både at foreslå og validere samme korrektion**. Vælg evt. senere et særligt klasse-/distanceled i den nye MWP-model i stedet for at gøre de gamle standardtider urealistiske. Ingen særskilt kg-kalibrering i dette trin.
5. Fortsæt det allerede aftalte filter: **102 slow/artificial race exclusions kun fra standardtidsforskning**, aldrig fra original historik. Tider, original-score, vægt og offsets er uændrede.

### Kildeoversigt

- [Brugerens levende Google Sheets-rækker](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), verificeret direkte på de seks aktuelle løb.
- Brugerens arkiverede SQLite v86 manuelle tider og v43 officielle *før-start* HCP-programkilder. Kildeproveniens findes pr. start i `off_hcp_by_start`.
- [Øvrevoll resultater 25. april 2024](https://ovrevoll.no/Spill/Resultater-Ovrevoll/?date=20240425), [6. november 2025](https://ovrevoll.no/Spill/Resultater-Ovrevoll/?date=20251106), [1. oktober 2026](https://www.ovrevoll.no/Spill/Resultater-Ovrevoll/?date=20261001).
- [Svensk Galopps 16. november 2025 officielle løbsoversigt](https://www.svenskgalopp.se/documents/3540/BP_251116_A4.pdf), [14. september 2025 baneprogram](https://www.svenskgalopp.se/documents/3274/Bro_250914_uppslag.pdf). Officiel race-nr. og interne løbsnumre kan afvige.
- Reproducerbar data: `01_all_meeting_ordinary_hcp_races.csv`, `02_six_race_diagnostics.csv`, `03_repeated_horses_across_six_races.csv`, `04_six_races_runner_source.csv`, `05_sensitivity_if_six_omitted_ONLY_FOR_QA.csv`, `06_official_handicap_reference.csv`, `09_hcp_race_level_sensitivity.csv`, samt læse-only analyseprogrammer og tidligere kildepakker.