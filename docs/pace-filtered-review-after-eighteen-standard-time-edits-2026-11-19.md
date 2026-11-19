# Nordic Racing – kontrol efter 18 tidstabelrettelser med tempofilter

**19. november 2026 · Forskning, ikke ændring af historiske data eller Googles originalark**

## Kilder og metode

- Brugerens [aktuelle Google Sheets-standardtider](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit) er læst og verificeret direkte: **Göteborg græs 2.400 m klasse 2 = 145,0 s** (grad1 143,0 s, grad0 139 s); **Øvrevoll græs 1.170 m klasse 2 = 68,2 s** (grad1 67,2 s, grad0 64 s). De seneste ændringer er **−0,2 s** og **+0,1 s** fra forrige aktuelle tabel. Ændringerne gælder grad1–11, ikke grad0.
- Data: den arkiverede bruger-verificerede v86-historik med **10.566 manuelt rankede starter fra 1.327 almindelige numeriske handicapløb i 2024–2026**, hvorfra **102 hele løb markeret »Langsomt løb« eller »Kunstigt løb«** og deres 733 starter/495 top5 er udeladt af *kalibreringen*, ikke historikken.
- **Analyseudsnit = 1.225 løb, 9.833 starter og 6.082 top-5-placeringer**. Race-key-filtrering; hesteindividuelle bemærkninger om langsom start medfører ikke løbsudeladelse. Andre flags om ikke-verificerbar tid er separate QA-signaler.
- Genberegning med de **16 hidtidige** tidstabelændringer som udgangspunkt og derefter brugernes **to nye**. De samme arkiverede manuelle tider og dags-offsets bevares. Diskrete gamle rankingtrin på 0,5 er genskabt direkte fra relevante standardtidsrækker; de nyberegnede standardtider er **analytiske** og ændrer ikke historiske ranks i database eller Race Studio.
- Residualer i **gamle rankingpoint, lavere er bedre**, justeret med regression for handicapklasse, år, relativ placering og feltstørrelse, men **ikke for ny vægt** og uden officielle goingmålinger. En distanceresidual viser mål-disciplinen minus **andre distancer på samme bane**, efter kovariatkontrol. Den viser association, ikke bevist standardtidsfejl. Samme-dags- og klassekontrol udført, men både klasse-/år- og løbsblanding er fortsat vigtige forbehold. Ingen selvstændig valideringsårgang.

## De to seneste gennemførte ændringers effekt

| Bane / distance | Klasse 2 før → nu | Filtrerede løb / top5 | Gns. top5-rank før → nu | Justeret afstandsresidual før → nu | Samme-dags-residual nu |
|---|---:|---:|---:|---:|---:|
| **Göteborg græs 2.400 m** | 145,2 → **145,0 s** | **9 / 45** | 3,60 → **3,70** | −0,185 → **−0,086** | **+0,127** |
| **Øvrevoll græs 1.170 m** | 68,1 → **68,2 s** | **26 / 130** | 3,896 → **3,796** | +0,401 → **+0,303** | **+0,273** |

Begge ændringer reducerer absolut afvigelse. **Göteborgs resultat bygger kun på 9 normaltempoløb**, hvor samme-dags-indikatoren er positiv, selvom den overordnede er svagt negativ; **ingen yderligere Göteborg-rettelse nu**. For **Øvrevoll 1.170 m** er residualerne pr. år nu 2024 **+0,551**, 2025 **+0,280**, 2026 **−0,010**. 2026 er allerede neutral. **Ingen yderligere generel rettelse nu**.

## De største tilbageværende afvigelser

| Bane/distance | Filtrerede løb/top5 | Klasse- og årsjusteret distanceresidual | Grund til IKKE at anbefale endnu en hel-række-rettelse |
|---|---:|---:|---|
| **Øvrevoll græs 2.400 m** | **20/100** | **−0,350** | 2024 −0,574 og 2025 −0,470, men 2026 **+0,177**; forskellen skifter fortegn; flere klasser har få løb |
| **Bro Park dirt 1.200 m** | **34/167** | **−0,328** | Kl. 2 ≈ +0,003, kl. 3 ≈ +0,060, men kl. 3,5 −0,371 og kl. 4 −0,580. En hel −0,1s forbedrer totalen til −0,202, men forværrer kl. 3 til +0,160 |
| **Øvrevoll græs 1.170 m** | **26/130** | **+0,303** | Nyopdateret; 2026 er næsten 0; kl. 2 −0,010 og kl. 3,5 −0,070, mens 2,5 +0,399 og 4,5 +0,630 |
| **Øvrevoll dirt 1.100 m** | **65/321** | **−0,248** | Kl. 2 +0,129 og kl. 4 +0,169, men kl. 2,5 −0,631 og kl. 5 −0,674; endnu −0,1s bringer totalen til −0,128 men forværrer kl. 2 til +0,254 |
| **Aalborg græs 1.800 m** | **25/125** | **+0,227** | Årene giver modsatrettede signaler: 2024 −0,396, 2025 +0,565, 2026 +0,091 |
| **Aarhus græs 2.000 m** | **27/134** | **+0,217** | Stadig i høj grad 2024: +0,809, mod +0,158 i 2025 og −0,137 i 2026; flere unormale løb allerede filtreret |
| **Göteborg græs 1.600 m** | **22/110** | **+0,212** | Kl. 2,5 alene +0,708 (5 løb), men kl. 3/3,5/4/4,5 er tættere på 0; yderligere +0,1s kan skade disse |

### Særligt relevante klasseforskelle for næste analyse

**Bro Park dirt 1.200 m, nuværende standard:**

| Klasse | Filtrerede løb/top5 | Afvigelse fra andre Bro Park dirt-distancer i samme klasse |
|---|---:|---:|
| 2,0 | 3 / 13 | +0,003 |
| 2,5 | 6 / 29 | −0,358 |
| 3,0 | 6 / 30 | +0,060 |
| 3,5 | 10 / 50 | −0,371 |
| 4,0 | 7 / 35 | −0,580 |
| 4,5 | 2 / 10 | −0,270 |

**Øvrevoll dirt 1.100 m:** kl. 2 +0,129 (5 løb), kl. 2,5 −0,631 (6), kl. 3 −0,097 (9), kl. 3,5 −0,188 (11), kl. 4 +0,169 (10), kl. 4,5 −0,361 (9), kl. 5 −0,674 (14). Effekterne er ikke jævnt ordnet efter klasse, så **en enkelt konstant sekunder-per-klassetilvækst vil næppe forklare alle forskellene**; undersøg løbsdage, faktisk tidskvalitet og hvilke klasser der løbes over andre distancer, før en klassekurve foreslås.

## Anbefalet næste fase

1. **Behold de nuværende 18 rettelser.** **Ingen yderligere flad sekundrettelse** til alle trin på samme distance anbefales på det nuværende grundlag. Særligt undlad straks at ændre Göteborg 2.400 og Øvrevoll 1.170 igen.
2. Gennemgå først **Bro Park dirt 1.200 m (klasser 2,5/3,5/4)** og **Øvrevoll dirt 1.100 m (klasser 2,5/4/5)** med løbsniveau og år. Test dernæst om det er klassekurvens hældning eller klasse-/år-sammensætningen, der skaber forskellene. Dette er en **diagnose**, ikke allerede en godkendt ændring af tidsintervallerne.
3. Kontrollér særskilt **»Tiden kan ikke verificeres«** som *datakvalitet*, ikke tempoflag. Behold **»Langsomt løb«/»Kunstigt løb«** ekskluderet i alle kommende standardtidskalibreringer. Bevar originaldata.
4. Brugerens notat skal tages op ved næste **MWP/afstand/klassekurve**-fase: Klampenborgs nuværende 0,5/0,6/0,7/0,8/0,9/1,0 sekunder pr. halve rank-trin afhængig af distance og hypotesen om 0,5–1 længde pr. kilo. Sekunder pr. klassetrin kan ikke uden yderligere måling omregnes direkte til længder pr. kilo. **Ingen særskilt vægtmodel nu.**

## Reproducerbarhed

Nye CSV'er i researchpakken: `01_distance_after18_vs16.csv`, `02_class_after18.csv`, `03_same_day_after18.csv`, `04_two_latest_verified.csv`, `05_all_vs_filtered_after18.csv`, `06_candidate_scenarios_after18.csv`, `07_candidate_class_after18.csv`, `review_after_18.py` og denne rapport. Skriptet bygger på den tidligere oprettede v86-historik/16-edits-kontrol og må ikke forveksles med en komplet standalone database.