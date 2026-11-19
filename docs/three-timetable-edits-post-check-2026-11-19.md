# Kontrol efter tre tidstabelændringer — 19. november 2026

**Status:** Kun read-only forskning; ingen ændringer i historiske starter, manuelle tider, originale rankings, offsets eller produktionsmodellen.

## Datagrundlag
- Brugerens forbundne `index`-ark blev aflæst direkte i fanerne `Jægersro - Dirt` og `Gøteborg - Græs` 19/11/2026.
- Originale v86-arkiverede rankings og rankingtid fra 2024–2026. Kun rene numeriske handicapklasser, ingen amatør-, vinder-, alder- eller maksimum-HCP-løb.
- Formel: `rang = MATCH(ranking_time, banespecifikke tidsgrænser, 1) + gemt dags-offset`. Det oprindelige reference-mønster kan reproduceres præcist for samtlige 535, 189 og 270 relevante starter. Korrigeret simulering beregner kun ændringen fra oprindelig til aktuelt standardmønster og anvender den på den gemte originalranking. Derved bevares original data og offsets.

## Aktuelle standarder kontra *oprindeligt, faktisk arkiveret* beregningsgrundlag
| Bane | Distance | Oprindelig klasse 2-reference | Aktuelt ark | Forskel | Top 5: oprindeligt | Top 5: simulering | Top 5 starter / løb |
|---|---:|---:|---:|---:|---:|---:|---:|
| Jægersro dirt | 1200m | 72,5s | 72,8s | +0,3s | 3,825 | 3,525 | 354 / 72 |
| Jægersro dirt | 1600m | 100,3s | 99,9s | −0,4s | 3,145 | 3,398 | 128 / 26 |
| Göteborg græs | 2200m | 131,4s | 132,3s | +0,9s | 4,728 | 4,231 | 160 / 32 |

**Kilde- og versionsadvarsel:** Ved en **tidligere live-aflæsning** i analysen (før brugerens seneste besked) var Göteborg 2200m allerede på 132,3 sek. ved klasse 2. Fanen er derfor **ikke blevet ændret siden den aflæsning**, men den ligger **+0,9 sek. over den standard på 131,4 sek., som faktisk blev brugt til at producere de arkiverede originale rankings**. Det er umuligt herfra at afgøre præcis hvornår tabellen blev opdateret. Påfør IKKE endnu en +0,9 sek.

## Effekt
- Jægersro: ujusteret distanceforskel blandt top 5 (`1200m minus 1600m`) falder fra **+0,680** til **+0,127** gammel rankingpoint. Det er markant bedre intern sammenhæng, men klasseforskelle skal stadig kontrolleres.
- Göteborg: top 5 på 2200m går fra **4,728** til **4,231**; 1400m ligger på **3,583** (uændret), dvs. den rå tværdistanceforskel falder fra **+1,145** til **+0,648**. En væsentlig del af resten skyldes muligvis klassemix/tempo/hestekvalitet og må ikke uden videre fjernes ved at flytte hele kurven igen.
- Göteborg klasse 4 top-5: 1400m **4,167** (n=15) versus 2200m **4,362** (n=40) efter ændring: differencen kun +0,195. Klasse 2: 2,720 (n=25) vs 3,567 (n=15), diff +0,847. Dette taler for en **klassevis** diagnose i stedet for en anden flad tidsjustering.
- Jægersro klasse 2,5: 1200m går fra **3,381** til **3,054** (n=84); 1600m går fra **2,512** til **2,788** (n=40). Klasse 3,5: 3,744 (n=90) vs 3,650 (n=10) efter ændring.
- For alle hestestarter: Jægersro 1200m 4,539→4,243 (n535); 1600m 3,577→3,836 (n189); Göteborg 2200m 5,126→4,631 (n270).

## Anbefalet næste skridt
1. **Frys disse tre aktuelle standardtabeller som testkandidat** og dokumentér dem særskilt fra de arkiverede originale tidstabeller og rankings. Brugerens live Sheet er ikke ændret af denne analyse.
2. Lav **klasse- og årsopdelt genberegning** for alle baner, præcise distancer og alle regulære handicapløb, sammenlign alle/top5/vindere. Se især tilbageværende Göteborg forskelle fordelt på klasse. Kræv væsentligt datagrundlag for justeringsforslag.
3. Hold forskellige bane-kvalitetsmål separate fra rene standardtidsfejl. Brugerens ønskede styrkeforskelle er priorer/arbejdsmål, ikke naturkonstanter; test gennemsnitsvægt og official pre-start HCP som følsomhed, ikke dobbelttæl fysisk vægt.
4. Revider kun andre kurver ved dokumenteret stabil afvigelse efter ovenstående kontrollag; derefter kalibrér fysisk vægt efter distance og opbyg **ny høj-er-bedre MWP-inspireret rating** inkl. nye ratingpoint til banekorrektion. Ingen direkte overførsel af gamle offsets til nye ratingpoint og ingen officielle going-målinger som modelinput.

Fil: `13_three_updates_impact.csv` i research-workspace; script: `evaluate_three_table_edits.py`.