# Nordic Racing — banestyrke, vægt og tidsstandarder

**Dato:** 19. november 2026  
**Status:** **Kun til review. Intet ændret i Google Sheets, kildedata, manuelle tider, gamle offsets eller den aktive Race Studio-model.**

## 1. Opgave og datagrundlag

Brugeren angav følgende normative ønskede forskelle i **GAMLE rankingpoint** (lavere er bedre):
- **Græs:** Bro Park 0,00; Klampenborg +0,10; Øvrevoll +0,10; Göteborg +0,25; Aarhus +0,60; Odense +0,80; Aalborg +1,00.
- **Dirt:** Jägersro 0,00; Bro Park +0,30; Øvrevoll +0,50.

Vi anvender de eksisterende, godkendte manuelle rankings **efter de gamle manuelle baneoffsets**, på 10.566 starter / 1.327 rene numeriske handicapløb i 2024–2026, 6.577 placeringer som top 5 og 318 bane × distance × klasse-kombinationer. Max-HCP, Ældre Vinder, 2-/3-års særløb, maiden og amatørhandicap er ikke medregnet. Der er yderligere to små baner uden brugerdefineret mål (Gærdet og Strømsholm), og der foreslås ingen ændringer for dem.

Datakilder: brugerens v86 `starts`-arkiv, officiel pre-start HCP fra v43 (`10.557` ud af `10.566` starter matchet), og tidstrin fra den tilkoblede [Google Sheet `index`](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), tabeller for hver bane × underlag.

## 2. Beregning og begrænsninger

Hovedmålet er gennemsnit for **top 5**. Som kontrol vises også alle heste og vindere. En statistisk reference er beregnet efter handicapklasse (numerisk), fire distanceintervaller, afsluttende placering i feltet, feltstørrelse, kalenderår og faktisk analysevægt. Modellen sammenligner de *historiske residualer* med referencebanerne (Bro Park græs og Jägersro dirt).

Den officielle HCP-værdi blev **ikke regressionskontrolleret væk** i hovedbanesammenligningen. Dette er bevidst: Brugeren ønsker at måle forskelle i faktisk niveau for *samme handicapklasse*, og den officielle HCP kan være en del af den reelle forskel. HCP er dog medtaget som selvstændig QA-kolonne i rapporten.

Modellen er ikke en kausal identifikation af baneeffekt; hestebestand, tempo, dagsbane og konkurrenceniveau varierer stadig. Brugerens styrkemål er **valgfrie kalibreringsmål**, ikke fakta som statistikken beviser. Undgå at tilpasse standardtiderne mekanisk til ønskede gennemsnit.

## 3. Banestyrke sammenholdt med målet — TOP 5

| Underlag / bane | Målforskel | Beregnet vægtjusteret forskel | Manglende justering af GAMMEL ranking |
|---|---:|---:|---:|
| Græs, Bro Park | 0,00 | 0,00 | 0,00 |
| Græs, Klampenborg | +0,10 | +0,18 | −0,08 |
| Græs, Øvrevoll | +0,10 | +0,26 | −0,16 |
| Græs, Göteborg | +0,25 | +0,59 | −0,34 |
| Græs, Aarhus | +0,60 | +0,56 | +0,04 |
| Græs, Odense | +0,80 | +0,37 | +0,43 |
| Græs, Aalborg | +1,00 | +0,63 | +0,37 |
| Dirt, Jägersro | 0,00 | 0,00 | 0,00 |
| Dirt, Bro Park | +0,30 | +0,09 | +0,21 |
| Dirt, Øvrevoll | +0,50 | +0,11 | +0,39 |

*Positiv justering af gamle rankingpoint betyder, at en given tid skal have dårligere ranking; negativ betyder bedre ranking. Disse er beregnede fuld-mål-gap, ikke godkendte tabelændringer.*

**Robusthed ved hesteudvalg:** Göteborg har +0,58 for *alle*, +0,59 for *top 5* og +0,61 for *vindere*: ret ens. Klampenborg har derimod +0,30 for alle, +0,18 for top 5 og +0,09 for vindere. Dette taler imod en fælles, blind Klampenborg-ændring. Øvrevoll dirt har +0,19 (alle), +0,11 (top 5) og +0,02 (vindere), hvor brugerens mål er +0,50; det er en væsentlig forskel, men bør valideres gennem klasser og hestekvalitet.

**Årlig stabilitet** (samme justering, top 5): Göteborg +0,74/+0,68/+0,38 i 2024/25/26; Aalborg +0,79/+0,55/+0,60; Odense +0,40/+0,42/+0,30; Klampenborg +0,36/+0,11/+0,08. Banestyrker er ikke nødvendigvis konstante mellem sæsoner.

## 4. Vægt: Den har betydning, men må ikke forveksles med hestekvalitet

Gennemsnitlig vægt blandt top 5: Bro Park græs 59,07 kg; Klampenborg 60,34; Göteborg 60,28; Aalborg 60,54; Jägersro dirt 59,90; Bro Park dirt 60,34; Øvrevoll dirt 59,84. Ved samme klasse, afstandsgruppe, placering, feltstørrelse og år er én kg højere vægt statistisk forbundet med **0,153 point bedre gammel ranking** (race-klynget standardfejl 0,0027), men **det er ikke en kausal vægteffekt**: den gamle ranking giver selv en vægtbonus, og gode heste får højere handicapvægt.

F.eks. Klampenborg vs Bro Park græs stiger den beregnede top 5-forskel fra **+0,12 uden vægtkontrol til +0,18 med vægtkontrol**, og Göteborg fra +0,53 til +0,59. Vægtfordelingen skjuler derfor lidt af forskellen. Der er ingen grund til at vælge den gamle 0,20 s/kg som ny v2-faktor ud fra denne regression.

**Klassisk eksempel:** Aalborg klasse 4 top 5: 74 starter, gennemsnitlig rank 5,15, vægt 61,14kg, officielt HCP ca.63,0; Bro Park græs klasse 4 top 5: 30 starter, rank 4,02, vægt 61,32kg, officielt HCP ca.62,8. Vægten og HCP er omtrent ens, men rankings er forskellige. Dette understøtter at det er værd at undersøge klassens faktisk realiserede præstationsniveau og/eller standardtider.

## 5. Forskellen varierer med klasse — dette er afgørende før rettelser

**Aalborg vs Bro Park græs:** Klasse 2,5 +0,46 (25 top5 på Aalborg), klasse 3,5 +0,36 (65), klasse 4 +0,90 (74), klasse 4,5 +1,17 (30). Ved generelt mål Aalborg +1,00 ligger klasse 4 allerede tæt på. En blind +0,37-pointjustering for *alle* grader på Aalborg kan ødelægge dette.

**Odense:** Klasse 2,5 +0,18 (35 top5), klasse 3,5 +0,39 (65), klasse 4 +0,66 (95), klasse 4,5 +0,78 (20) vs. målet +0,80. Her bør især de **stærkere handicapklasser** efterprøves.

**Göteborg:** Klasse 2,5 +0,60 (128), klasse 3,5 +0,53 (145), klasse 4 +0,60 (105), klasse 4,5 +0,93 (56), alle mod mål +0,25. Her er svaghedstendensen bredere.

**Øvrevoll dirt:** Klasse 2,5 +0,21 (81), klasse 3,5 −0,03 (129), klasse 4 −0,13 (170), klasse 4,5 −0,20 (135) mod mål +0,50. En fælles ændring kan være utilstrækkelig og samtidig ramme klasserne ulige.

VIGTIGT: Bro Park græs reference i klasse 4 er blot **30 top 5-starter** og klasse 4,5 blot 18. Klassedifferencer er derfor mindre sikre end banens samlede gennemsnit.

## 6. Konkrete tidsstandard-forslag til MANUEL REVIEW

En bane-distance med et positivt `forslag tid ±sek` betyder: *Forøg standardtiderne på den distance* (hesten får bedre/lavere gammel ranking). Et negativt forslag betyder: *Forkort standardtiderne* (hesten får dårligere/højere gammel ranking).

Omregning bruger **hver distances egen originale tidstabel**, og en 0,5-rank-trinsstørrelse i sekunder. Dette er kun **første konservative scenario**, ikke en autoriseret opdatering. Det er ikke en MWP-omregning.

| Prioritet | Bane × distance | Top 5 / løb | Muligt forskningsforslag | Begrundelse |
|---|---|---:|---:|---|
| Høj | **Göteborg græs 2.200 m** | 160 / 32 | **+0,9 sek.** | Internt +0,32 gamle point sværere end Göteborgs gennemsnit; ens fortegn 2024–26 og banens totalniveau ligger +0,34 over ønsket styrkeforskel. |
| Høj | **Jägersro dirt 1.200 m** | 354 / 72 | **+0,2 til +0,3 sek.** | Internt +0,26 gamle point sværere end Jägersro generelt; konsistent 2024–26. |
| Høj | **Jägersro dirt 1.600 m** | 128 / 26 | **−0,3 til −0,4 sek.** | Internt −0,24 gamle point lettere end Jägersro generelt; tre år med samme fortegn. Sammen med 1.200m-opretning bliver sprint/mellemdistance mere ensartet. |
| Undersøg | **Øvrevoll græs 1.980 m** | 53 / 11 | **+0,6 sek.** | Lokalt +0,66 point sværere end banen; kun to tilstrækkelige årsudsnit; kan skyldes tempo og løbsudvalg. |
| Undersøg | **Bro Park dirt 1.200 m** | 186 / 38 | **−0,3 sek.** | Banen ser for stærk ud relativt til målet Jägersro+0,3; distanceprofilen peger delvist i samme retning. |
| Undersøg | **Øvrevoll dirt 2.400 m** | 177 / 36 | **−0,8 sek.** | Øvrevoll dirt er betydeligt stærkere i eksisterende top5-ranking end brugerens ønske. Et kursniveau-scenarie, som bør kontrolleres særskilt for hver handicapklasse. |
| Undersøg | **Odense græs 1.800 m** | 85 / 17 | **−0,7 sek.** | Banen samlet set for stærk ift. mål, men klasse 4 og 4,5 er allerede tættere på målet; *ret IKKE hele tidstabellen ens uden klassetest*. |
| Undersøg | **Klampenborg græs 2.400 m** | 60 / 13 | **+0,6 sek.** | Distanceavvigelse +0,27, men banen samlet ligger tæt på målet. Lavere prioritet end de tre første. |

**Hold foreløbig uændret:** Klampenborg samlet, Aarhus samlet, referencebanernes overordnede niveau; også Göteborg 1.400m, hvor lokal rangering allerede er relativt god sammenlignet med 2.200m. Undgå uniform Aalborg/Odense-ændring på tværs af klassekolonner.

De viste +/-sekunder er rundede hypoteser. Ændringer i faktiske *diskrete* rankings efter et tidstabelsskift kræver fuld replay af tiderne og genbedømmelse af dagens offsets, da den gamle 0,5-pointsskala ikke er kontinuerlig.

## 7. Godkendelsesprocedure og efterfølgende MWP-model

1. Review af **bane × distance × klasse**, minimum 25–40 top5-starter over flere år, plus alle-heste og vindersnit. Marker særlige paceproblemer.
2. Separat valg: (a) justering af **standardtidsniveau pr. bane/distance** og (b) evt. **klassetrin/slope** for enkelte baner; de to ting må ikke blandes uden nyt historisk replay.
3. Efter justering af tidstabeller: genberegn de gamle rankings og de **gamle dags-offsets i en research-overlay**, fordi en ændring i standardtiden ellers delvis kan blive neutraliseret eller dobbelttalt via offset. De originale data bevares.
4. Kontrollér forbedring med heste, der løber på flere baner/distancer, og på et år/datasæt der ikke brugtes til forslagene.
5. Først derefter bruges de nye standarder som kilde i den **nye MWP-inspirerede højere-er-bedre skala**. Oversæt ikke −4 gamle points mekanisk til +60 nye points; beregn direkte fra verificerede manuelle tider, HCP-ankre og distancejusteret fysisk vægtmodel. **Officielle going-tal anvendes ikke.**

## 8. Filer

- `Nordic_Racing_Banestyrke_Vaegt_Tidstabel_Forslag_2026.xlsx` med 9 faner: Overblik, Banemål, Vægt pr bane, Klasser og vægt, Klassevis styrke, Forslag pr distance, 318 kombinationer, Årstest, Metode.
- Underliggende tabeller `01_...csv`–`12_...csv` og reproducerbar analyse-/forslagsscript i researchpakken. Ingen databaseskrivning.