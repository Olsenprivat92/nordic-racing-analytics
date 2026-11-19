# Nordic Racing – kontrol efter 10 godkendte tidstabelrettelser

**19. november 2026 · Forskningsanalyse, ingen ændringer foretaget i kildearket**

## 1. Bekræftelse af seneste rettelse

Den levende Google Sheet-fane `Øvrevoll - Dirt` viser klasse-2-standard for 1100 m **67,1 sek.** mod tidligere **67,2 sek.** (−0,1 s, grad 0 uændret). Den gamle metodes manuelle tider og oprindelige dags-offsets er ikke ændret.

Med samtlige **10** aktuelle tidsrettelser genberegnes **10.566 manuelt rankede starter**, **1.327 almindelige numeriske handicapløb** og **6.577 top-5-starter** i 2024–2026. Ekskluderer specialløb (2- og 3-års-løb, ældre vinder, maiden, amatør, capped/max-HCP). Hver original start og rating beholdes i den frosne kilde; konsekvensen beregnes i forskningskopi.

Øvrevoll dirt 1100 m: **345 top-5-starter / 70 løb**, gammel top-5-ranking 4,214 → ny **4,320**; klasse-, placering- og årskorrigeret difference mod banens andre dirt-distancer **−0,245 → −0,140 gamle point**; samme-dag-difference **−0,297 → −0,193**. 2025 er nu lidt positiv (+0,061), og derfor **ingen yderligere rettelse** til denne distance foreløbigt.

## 2. Næste ene konkrete forslag: Øvrevoll græs 1980 m +0,2 sekund

Denne distance har fortsat den største robuste positive gamle rankingafvigelse (for dårlig ranking) efter de 10 rettelser, **men kun 11 løb**, så anvend en lille testjustering.

| Måling | Nuværende | Test med +0,2 sek. |
|---|---:|---:|
| Standard grad 1 (klasse 1) | 120,6 s | **120,8 s** |
| Klasse 2-standard | 122,2 s | **122,4 s** |
| Klasse 4-standard | 125,4 s | **125,6 s** |
| Top 5-start / antal løb | 53 / 11 | 53 / 11 |
| Gennemsnitlig top 5-ranking (gammel skala) | 4,868 | **4,745** |
| Justeret difference mod Øvrevolls andre græsdistancer | +0,490 | **+0,368** |
| Samme-dag difference mod andre distancer | +0,731 | **+0,622** |
| 2024-difference | +0,541 | **+0,462** |
| 2025-difference | +0,715 | **+0,563** |
| 2026-difference | +0,178 | **+0,013** |

**Kun grad 1–11 ændres; grad 0 bevares.** Resultaterne for de dokumenterede klasse 3, 4,5 og 5 forbedres alle lidt, men hver klasse bygger på få løb. Af de **10 løb med en anden distance på samme mødedag** har 9 en positiv afvigelse inden yderligere justering; medianen er +0,542 point, og to løb har afvigelser omkring +2. Derfor bør vi ikke bruge +0,731 som et præcist måltal eller ændre mere end +0,2 sek. ad gangen. Ved +0,3s er 2026-afvigelsen omtrent uændret; yderligere justering bør afvente flere data og en særskilt tempo-/klassekontrol.

## 3. Andre mulige afvigelser – vent med rettelser

| Bane / distance | Top 5 / løb | Aktuel justeret difference | Hvorfor ikke rette nu? |
|---|---:|---:|---|
| Aalborg græs 1800 | 130 / 26 | +0,481 | 2024: −0,100, men 2025: +0,733 og 2026: +0,537; forbedring vil også gøre Aalborg stærkere relativt til Bro Park, mod brugerens banestyrkemål |
| Øvrevoll græs 1170 | 155 / 31 | +0,300 | 2026 er allerede −0,121; +0,2s ville forskyde 2026 til −0,344 |
| Øvrevoll græs 2400 | 115 / 23 | −0,364 | I 2026 er afvigelsen næsten nul: −0,005; −0,2s ville ændre den til +0,127 |
| Aarhus græs 2000 | 154 / 31 | +0,394 | 2024 driver problemet (+1,141), mens 2025 ligger +0,080 og 2026 −0,014 |
| Odense græs 1800 | 85 / 17 | −0,158 | 2026 afviger modsat de to andre år (+0,664) |
| Klampenborg græs 1100 | 15 / 3 | −0,560 | Kun tre numeriske handicapløb. Brugerens observation om for let 1100m bevares til fuld distancekontrol |

## 4. Metode og forbehold

- Kilder: brugerens [Google Sheet `index`](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), de frosne oprindelige 2024–26 manuelle rangeringer (v86) og de gamle tidstabeller; alle 10 ændringer verificeret mod aktuelt Google Sheet ved tidligere kontroller, seneste Øvrevoll dirt 1100m kontrolleret her.
- Beregning: behold hver hests tidligere manuelle tid, den **eksisterende gamle rankingtidsberegning** og oprindelige dags-offset; genberegn alene gammelt halvt-trins score via aktuelle banespecifikke tider. Ingen **ny** vægtkorrektion, ingen MWP, ingen officiel banemåling.
- Sammenligninger: top 5 og alle heste; normalisering for gammel analyseklasse, placering, feltstørrelse og år; særskilt sammenligning af forskellige distancer på **samme mødedag**. Det er observationelle kvalitetskontroller, ikke kausale effekter eller statistisk bevis for forkerte tidstabeller.
- Det er ikke nødvendigvis korrekt, at alle distancer på samme bane skal have identisk gennemsnit: hestekvalitet, pace, underlag, klassefordeling og distancetilpasning varierer. Derfor små godkendte iterativer.
- Fremtidige noter: Klampenborg 1100m kan være for let; gennemgå ALLE distancer pr. bane efter aktuelle ændringsrunde. Brugerens gamle sekunder pr. 0,5 klassetrin: 1100–1300 0,5s, 1400 0,6s, 1600 0,7s, 1800 0,8s, 2200 0,9s, 2400 1,0s. Genbesøg potentiel sammenhæng med længder/kg først under senere MWP/weight calibration.

**Beslutning:** Anbefal kun Øvrevoll græs 1980 m +0,2 sek. på grad 1–11 nu. Efter brugerens eventuelle ændring: verifikation og helbane-distancekontrol, i stedet for automatisk flere ensartede justeringer.