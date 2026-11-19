# Nordic Racing — kontrol af klassekurver efter 18 tidstabelrettelser

**Dato: 19. november 2026. Status: forskningsanalyse, ikke ændring af Google Sheets, de historiske manuelle tider/rankings eller MWP.**

## Datagrundlag og metode

- Den bruger-godkendte historik fra 2024–2026 indeholder oprindeligt **1.327 almindelige numeriske handicapløb med 10.566 starter**. De **102 hele løb** med brugerens annotation »Langsomt løb« eller »Kunstigt løb« er udeladt fra *kalibrering*, ikke slettet fra hestehistorik. Tilbage er **1.225 løb, 9.833 starter og 6.082 top-5-starter**.
- Alle **18** brugerforetagne ændringer af banernes gamle rangeringstidstabeller er indregnet. De oprindelige manuelt korrigerede rankingtider og dagsoffsets er uændrede. Ingen ny vægtkorrektion eller MWP-rating er brugt.
- De to aktuelle live-rækker er verificeret direkte i Google Sheets 19. november: **Bro Park dirt 1200 m: grad0 67,0 s, grad1 71,3 s, grad2 72,3 s; Øvrevoll dirt 1100 m: grad0 62,0 s, grad1 66,1 s, grad2 67,1 s**. Begge har aktuelt **0,50 s mellem hvert halve gamle rankingtrin** i grad1–11.
- Klasseforskelle beregnes som top-5-rangering, regressionsjusteret for numerisk handicapklasse, år, placering og feltstørrelse, minus andre distancer på *samme* bane og underlag. **Lavere gammel ranking er bedre; en negativ forskel indikerer lettere ranking.**
- Udover hestestart-vægtede forskelle er hvert løb behandlet som en selvstændig enhed, og der er beregnet **90 % bootstrap-intervaller med løb som resampling-enhed**. Disse intervaller er *eksplorative og ikke korrigeret for mange simultane sammenligninger*; de påviser ikke kausalt forkert standardtid. Kontrol af samme heste på andre distancer (begge starter i top5 inden for 120 dage og højest én klasse fra hinanden) supplerer, men fjerner ikke præference-/udvælgelsesbias.

## 1. Bro Park dirt 1200 m

**34 normaltempoløb, 167 top-5-starter; 118 andre distanceløb på Bro Park dirt i reference.**

| Handicapklasse | Mål-løb | Hestestart-vægtet afvigelse | Løbsvægtet afvigelse | 90 % bootstrap pr. løb |
|---|---:|---:|---:|---:|
| 2,0 | 3 | +0,00 | −0,02 | −0,33 til +0,27 |
| 2,5 | 6 | −0,36 | −0,38 | −0,79 til +0,01 |
| 3,0 | 6 | +0,06 | +0,06 | −0,31 til +0,45 |
| **3,5** | **10** | **−0,37** | **−0,37** | **−0,71 til −0,05** |
| **4,0** | **7** | **−0,58** | **−0,58** | **−1,03 til −0,09** |
| 4,5 | 2 | −0,27 | −0,27 | −1,44 til +0,90 |

**Årskontrol:** Klasse 4 er negativ i alle tre år, men 2024 har kun 1 løb (−1,10), 2025 2 løb (−1,22), 2026 4 løb (−0,39). Klasse 3,5 er tæt på neutral i 2024 (+0,05), men tydelig negativ i 2025 (−0,48; 5 løb) og 2026 (−0,90; 2 løb). Samme-hest-kontrollen for klasse 4: **9 heste**, gennemsnitlig heste-vægtet afvigelse cirka **−1,31 gamle point**, men der er afstands-/feltselektionsbias. Klassen har ingen særskilt anmærkning »tiden kan ikke verificeres« blandt de 7 mål-løb i kildedata (fravær af note betyder ikke, at alle tider er fejlfri).

**Robusthed mod enkeltløb:** Ved at udelade ét af de 7 klasseløb ad gangen ligger den løbsvægtede klasse-4-afvigelse mellem **−0,83 og −0,46**. Det er derfor ikke blot ét ekstremt løb, der skaber forskellen.

## 2. Øvrevoll dirt 1100 m

**65 normaltempoløb, 321 top-5-starter; 124 øvrige dirt-løb på Øvrevoll som reference.**

| Handicapklasse | Mål-løb | Hestestart-vægtet afvigelse | Løbsvægtet afvigelse | 90 % bootstrap pr. løb |
|---|---:|---:|---:|---:|
| 2,0 | 5 | +0,13 | +0,12 | −0,23 til +0,46 |
| **2,5** | **6** | **−0,63** | **−0,68** | **−1,15 til −0,24** |
| 3,0 | 9 | −0,10 | −0,10 | −0,54 til +0,31 |
| 3,5 | 11 | −0,19 | −0,18 | −0,52 til +0,14 |
| 4,0 | 10 | +0,17 | +0,17 | −0,13 til +0,48 |
| 4,5 | 9 | −0,36 | −0,36 | −0,75 til +0,03 |
| **5,0** | **14** | **−0,67** | **−0,67** | **−1,02 til −0,32** |
| 5,5 | 1 | +0,40 | +0,40 | Ikke estimerbart |

**Årskontrol:** Klasse 2,5 er negativ 2024 (1 løb), 2025 (2 løb) og 2026 (3 løb). Klasse 5 er negativ i alle tre år (2024 4 løb, 2025 5, 2026 5), men effekten varierer. Klasse 4 er derimod positiv i både 2025 og 2026. Samme-hest-kontrollen for klasse 5: **9 heste**, gennemsnitlig heste-vægtet afvigelse cirka **−0,59**. Ved udeladelse af ét klasse-5-løb ad gangen bliver resultatet mellem **−0,77 og −0,59**.

**Diagnose:** Klasseafvigelserne skifter fortegn i takt med handicapklassernes variationer. Dette er ikke én monoton fejl, der kan korrigeres med ét nyt interval mellem rankingtrinnene.

## 3. Test af sekunder mellem gamle rankingtrin

Begge aktuelle standardrækker stiger **0,50 sek. pr. halve gamle rankingtrin**. Der er testet 0,40–0,60 sek. i trin på 0,025 sek., **analytisk**. Den test med fast grad-2-tid holder respektive grad2 på **72,3 s / 67,1 s**, så en ændret hældning ikke forveksles med en ren parallelforskydning.

| Bane | Nuværende interval | Laveste *in-sample* klassefejl | Klassefejl nu → test | Risiko |
|---|---:|---:|---:|---|
| Bro Park dirt 1200 | 0,50 s | **0,40 s** på MAE (eller **0,425 s** på RMSE) | 0,318 → 0,156 (MAE ved 0,40 s) | 2026 samlet residual −0,105 → **+0,518**; klasse 3 bliver +0,56, markant dårligere |
| Øvrevoll dirt 1100 | 0,50 s | **0,45 s** | 0,321 → 0,254 (MAE) | 2025 samlet residual −0,004 → **+0,265**; klasse 4 går +0,17 → **+0,47** |

Et alternativ med fast grad-1-tid giver andre optimale intervaller (Bro Park 0,425 s; Øvrevoll 0,475 s). **Resultatet er altså også afhængigt af, hvilket rankingtrin man holder fast.** Det er et tegn på, at in-sample-optimering her ikke kan bruges som tilstrækkeligt grundlag for en tidstabelændring.

**Vigtigt:** Handicapklassen (f.eks. klasse 4) er en *raceklasse*, mens 0,5 sekunders interval er mellem *gamle rankingtrin* i standardtidstabellen. En rettelse af tabellens hældning påvirker heste i flere raceklasser; man kan ikke målrette kun raceklasse 4 ved blot at ændre ét rankingtrin.

## 4. Konkrete løb, der bør kvalitetssikres senere

| Bane og løb | Raceklasse | Gennemsnitligt top-5-residual | Bemærkning |
|---|---:|---:|---|
| Bro Park **20. oktober 2024, løb 1** | 4,0 | −1,39 | Et af de stærkeste klasse-4-løb; ikke tempomarkeret |
| Bro Park **14. september 2025, løb 4** | 4,0 | −1,33 | Hurtigt ift. raceklassens reference |
| Bro Park **16. november 2025, løb 3** | 4,0 | −1,33 | Hurtigt ift. reference; note om let vinder er ikke automatisk tempoflag |
| Øvrevoll **25. april 2024, løb 7** | 5,0 | −1,64 | Kraftigt hurtigt klasseløb; ikke tempomarkeret |
| Øvrevoll **6. november 2025, løb 6** | 5,0 | −1,17 | Hurtigt ift. klasse, men almindelige kommentarer |
| Øvrevoll **1. oktober 2026, løb 3** | 5,0 | −1,10 | Hurtigt ift. klasse; ingen tidskvalitetsnote |

Alle ovenstående races er med i normaltempokontrollen og bevares, medmindre originalkilder senere godtgør et problem. **Man må ikke konkludere, at de er kunstige, blot fordi de er hurtige.**

## 5. Beslutning og næste forskningstrin

**Ingen nye sekundrettelser anbefales til de to distancers hele standardkurver nu.** De klassevis skiftende effekter, især Bro Park klasse 3 og Øvrevoll klasse 4, gør en enkel hældningsrettelse usikker. De stærke signaler skal i stedet følges op ved:
1. At udvælge de konkrete hurtige løb til **tidskvalitets-/løbsdagskontrol** (ikke automatisk udeladelse).
2. At verificere raceklassens faktiske handicapstørrelse og fordeling i de udvalgte løb, uden at genåbne analysen af vægtpr.-kg før standardtidsforskningen er afsluttet.
3. At sammenligne de samme hestes præstationer med flere referencebanedistancer og holde løb som selvstændige observationsenheder.
4. Først derefter overveje et særskilt raceklasse-afhængigt kalibreringsled i den kommende MWP-model i stedet for at forvrænge hele tidstabellen.

Brugerens tidligere hypotese om Klampenborgs stigende *sekunder pr. halve rankingtrin* på længere distancer (0,5/0,6/0,7/0,8/0,9/1,0 s) **er nu eksplicit genbesøgt**: Den kan inspirere et *distanceafhængigt* interval, men der er endnu ingen grund til at antage, at 0,5–1,0 længde pr. kg er identisk med 0,5–1,0 sekunder pr. rankingtrin. Den separate vægt-/MWP-kalibrering er fortsat udskudt.

### Reproducerbarhed og kilder

- [Brugerens live standardtider i Google Sheets](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit).
- Lokal frozen v86-historik `/mnt/data/ranking_bias_research/data.sqlite` og `manual_ranked.pkl`; læst fra tidligere godkendte bygge- og QA-scripts. Den aktuelle analyse læser originaldata, men skriver kun nye forskningsfiler.
- Skripter: `/mnt/data/class_curve_deep_audit.py`, `/mnt/data/class_curve_quality.py`, `/mnt/data/class_curve_within_horse.py`; CSV-kontroltabeller i `/mnt/data/class_curve_audit_after18/`.