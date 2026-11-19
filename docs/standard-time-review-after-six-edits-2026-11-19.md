# Nordic Racing – kontrol efter seks godkendte tidstabelændringer

**Status:** Forskningsreview, 19. november 2026. **Ingen Google Sheets-celler, originale manuelle tider, historiske rankings eller offsets er ændret af denne analyse.**

## Datagrundlag
- Frosset v86-datasæt: **10.566** starter i **1.327** almindelige numeriske handicapløb (klasse 1–6), heraf **6.577** top-5-starter, perioden 2024–2026. Alene almindelige handicapløb: ingen vinderløb, 2-/3-årsløb, maiden, amatørhandicap eller handicap med særskilt maksimumsgrænse.
- Bane-, underlags- og distanceopdelte tidsstandarder aflæst live 19. november 2026 fra brugerens [Google Sheet index](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit). Klasse 2-værdier verificeret direkte.
- Gammel ranking genberegnet fra **oprindelig rankingtid**, oprindelig arkiveret klassegradsfunktion og de **seks verificerede aktuelle** standardtidsændringer, mens brugerens historiske løbsdags-offset bevares. Kontrollens 0,5-gradtrappetrin anvendes nøjagtigt, ikke lineær tilnærmelse.
- Residualer kontrollerer for numerisk handicapklasse, år, placering som procentdel af felt og feltstørrelse, **ikke ekstra vægtkontrol**. Samme løbsdags distancer sammenlignes særskilt. **Ingen officielle banemålinger.**

## De seneste tre indtastninger – bekræftet, men Göteborg-deltaer er ombyttet ift. forslagene
| Bane | Distance | Sidste foreslåede skift | Aktuelt skift fra arkivstandard | Top5-starter / løb | Gns. gammel top5 | Gns. nu |
|---|---:|---:|---:|---:|---:|---:|
| Øvrevoll græs | 1980m | +0,4s | **+0,4s** | 53 / 11 | 5,132 | **4,868** |
| Göteborg græs | 2400m | +0,4s | **+0,2s** | 70 / 14 | 4,257 | **4,121** |
| Göteborg græs | 1600m | +0,2s | **+0,4s** | 120 / 24 | 4,338 | **4,025** |

Gamle tre rettelser, som fortsat er aktive: **Jægersro dirt 1200 +0,3s**, **Jægersro dirt 1600 −0,4s**, **Göteborg græs 2200 +0,9s**. Alle seks matches nu med arkiveret rankingformel uden datakorruption.

## Næste to forsigtige ændringsforslag
**1. Göteborg græs 2400m: yderligere +0,2 sekund på standardtiderne for grad 1–11, ikke grad 0.** Den aktuelle klasse-2-standard er **145,0 sek.**, foreslået **145,2 sek.**. Aktuel top5-ranking **4,121**, scenarie **4,021** over 70 top5-starter/14 løb. Klasse-/årsjusteret afvigelse mod Göteborgs øvrige distancer går fra **+0,350 til +0,251** gamle rankingpoint. Samme løbsdagskontrol fra **+0,567 til +0,469**. Klasse 2,5: 3,820→3,700 (25 top5); klasse 3,0: 3,967→3,900 (15); klasse 3,5: 4,450→4,350 (30). Signalet er især i 2025–26, mens 2024 var neutral. En **større yderligere +0,4s** ville give lokal residual +0,13, men skabe overkorrektion i 2024; **ikke** anbefalet.

**2. Klampenborg græs 2400m: +0,2 sekund på grad 1–11, ikke grad 0.** Nuværende klasse-2-standard **147,6 sek.**, foreslået **147,8 sek.**. Top5-ranking **3,608→3,500** over 60 top5-starter/13 løb. Afvigelse mod banens øvrige distancer **+0,317→+0,210** og samme løbsdag **+0,637→+0,524**. Årskontrol viser alle tre år positive før ændringen: 2024 +0,133, 2025 +0,200, 2026 +0,774; scenarie 2024 +0,030, 2025 +0,110, 2026 +0,633. Handicapklasse 2,5 (25 top5) forbedres 3,280→3,180; klasse 3,5 (15) 4,433→4,300; klasse 2 (12) 3,417→3,375. **2026 dominerer afvigelsen**, og kun 13 løb; derfor begræns til +0,2 og kontroller tempo før større skift.

### Afvent – Øvrevoll græs 1980m
Der er stadig afvigelse +0,492 gamle point mod banens øvrige distancer og +0,732 ved sammenligning samme løbsdag. Et yderligere +0,2s ville sænke top5-ranking 4,868→4,745, men der er **kun 11 løb** og distancen er sårbar over for taktiske/tempoafhængige løb. **Jeg anbefaler ingen ny ændring af denne distance i samme runde.**

## Undgå bred standardændring på disse baner
- **Bro Park dirt 1200m:** samlet for gode gamle rankings (lokal residual −0,271), men klasse 2 afviger +0,413, klasse 3,5 −0,541, klasse 4 −0,716; ikke et ensartet distanceproblem.
- **Øvrevoll dirt 1100m:** lokal −0,246, men klasse 4 +0,273 og klasse 5 −0,779. Bred ændring kan skade korrekt kalibrerede klasser.
- **Aarhus græs 2000m:** lokal +0,394, men næsten hele afvigelsen kommer fra 2024 (2024 +1,140; 2025 +0,079; 2026 −0,013). Ingen ændring.
- **Øvrevoll græs 2400m:** 2024 −0,750, 2025 −0,248, 2026 −0,004. Ikke stabilt.
- **Aalborg græs 1500m:** 10 løb og afvigende 2024-retning; undgå korrektion som underminerer ønsket svagere bane.

## Dine banestyrkemål er stadig separat styringsprincip
På top5-modellen uden yderligere vægtvariabel og efter seks faktiske ændringer ligger klasse-/placeringsjusterede baneforskelle i gamle rankingpoint omtrent: Göteborg **+0,302** mod Bro Park græs (mål +0,25); Klampenborg **+0,124** (mål +0,10); Øvrevoll græs **+0,260** (mål +0,10); Aarhus **+0,593** (mål +0,60); Odense **+0,414** (mål +0,80); Aalborg **+0,659** (mål +1,0). På dirt ligger Bro Park **+0,106** mod Jægersro (mål +0,30), Øvrevoll dirt **+0,291** (mål +0,50). Målsætningerne er **priorer**, ikke resultatgarantier. Forskellige heste, niveauer og tempoer kan forklare noget af forskellen.

## Beslutning
Jeg anbefaler **to små ændringer til gennemgang**: Göteborg græs 2400 **+0,2 sek. ekstra**, og Klampenborg græs 2400 **+0,2 sek.** Begge gælder grad 1–11 uden at ændre grad 0. **Behold alle øvrige aktuelt godkendte tider.** Når brugeren har indtastet ændringerne, efterprøves alle/top5/vindere, pr. klasse og år, med samme metode.

### Beregningsfiler
- `18_six_verified_sheet_edits.csv`: seks kontrollerede ændringer og effekter.
- `18_scenario_comparison_after_six.csv`: direkte genberegning før/efter kandidater, inklusive same-day.
- `18_scenarios_by_class.csv`: ændringer for top 5 i hver handicapklasse.
- `17_current_all_318_track_distance_class.csv`, `17_current_distance_review_with_year_meeting.csv`, `17_current_class_specific_distance_checks.csv`: 318 detaljerede kombinationer og distance/klassekontroller.
- `18_next_round_analysis.py`: reproducerbar skriptkode. Kræver desuden brugerens frosne v86 `manual_ranked.pkl`, som ikke ændres.

**Alle kandidatændringer er scenarier. Google Sheet og live Race Studio er ikke ændret af denne analyse.**