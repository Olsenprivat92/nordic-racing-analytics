# Nordic Racing – distancekontrol efter 12 tidstabelrettelser

**19. november 2026 · RESEARCH · ingen ændringer i brugerens ark eller live-model**

## Bekræftet rettelse
Brugerens live Google Sheet `index`, fanen `Bro Park - Græs`: **1200 m, klasse 2: 69,6 → 69,7 s**. Grade1 68,6 → 68,7 s; grade0 uændret 64 s. Dette er nu den 12. godkendte tidsjustering på 11 forskellige bane-/distancerækker.

## Data og tilgang
- Frosne manuelle løbstider og historiske gamle rankinger fra v86, bevarede manuelle dags-offsets; aktuel standard fra Google Sheet.
- **10.566 hestestarter / 1.327 almindelige numeriske handicapløb / 6.577 top-5-starter**, 2024–2026, **64 bane×distance** og **318 bane×distance×klasse**.
- Ekskluderer maiden-, vinder-, 2-års-, 3-års-, amatør- og max/capped handicapløb.
- Genberegn eksisterende gamle, diskrete rankingtrin ud fra den arkiverede rankingtid. For de 12 ændringer er der matematisk lighed mellem arkiveret grundranking og de oprindelige standardtidstabeller.
- Analyser forskelle inden for samme bane efter justering for numerisk handicapklasse, placering i feltet, feltstørrelse og kalenderår. Suppler med samme løbsdag og samme-hest-distancesammenligninger.
- **Der foretages ingen ny vægtjustering, ingen konvertering til MWP og ingen brug af officiel going-måling.** Den oprindelige gamle rankingtid bevares, herunder dens historiske vægtformel.

## Bro Park græs 1200 m – efter den 12. ændring
- **85 starter / 13 løb / 64 top-5-starter**.
- Top-5-gennemsnit **3,594 → 3,500**.
- Justeret forskel mod andre Bro Park-græsdistancer **+0,22 → +0,12 gamle rankingpoint**.
- 2025 har fortsat positiv afvigelse, 2026 er allerede negativ: **ingen yderligere justering nu**.

## Ny primær anbefaling: Aalborg græs 2000 m, −0,2 sekunder
Gælder alle udfyldte standardtidstrin i 2000m-rækken, og bevarer tomme felter og eventuelle ikke-relaterede kolonner.
- **Klasse 2: 124,2 → 124,0 sekunder**. **Klasse 4: 127,8 → 127,6 sekunder.**
- **72 starter / 11 løb / 55 top-5-starter**.
- Top-5-gennemsnit **4,636 → 4,773**, fordi en hurtigere standard gør samme løbstid lidt sværere at ranke godt på.
- Klasse-/placering-/år-justeret lokal afstand **−0,263 → −0,127 gamle point**.
- Inden for samme løbsdag **−0,111 → +0,026 gamle point**.
- 2025: **−0,164 → −0,093**. 2026: **−0,318 → −0,068**. Ingen kvalificerede 2024-løb på 2000m i datasættet, altså kun to års kontrol.
- Klasse 3: **−0,219 → −0,053**; klasse 3,5: **−0,057 → +0,068** (små overkorrektionssignal); klasse 4: **−0,327 → −0,202**.
- **53 ikke-uafhængige sammenligninger fra 17 samme heste** med andet distanceløb inden for 120 dage og højst én klasseforskel: gennemsnitlig forskel **−0,454 → −0,265**. Par er gentagne og ikke individuelle uafhængige observationer.
- Aalborgs top-5-normaliserede gennemsnit ligger i dag ca. **+0,671 gamle point** svagere end Bro Park græs, mens brugeren ønsker ca. +1,0. Denne ændring løfter Aalborgs relative afstand med ca. +0,031 til **+0,70**, i den ønskede retning. Mål er et *ønsket kalibreringsanker*, ikke uafhængig verificeret sand løbskvalitet.
- **Undlad større indgreb nu**; −0,3/−0,4 kan overkorrigere 2025 og klasse 3,5.

## Særskilt kontrol: Klampenborg græs 1100 m
**24 starter / 3 klasse-4 handicapløb / 15 top-5-starter**, 2024–26.

| Løbsdato | Top-5-rank | Andre distancer samme møde |
|---|---:|---:|
| 2024-08-16 | 3,80 | 4,10 |
| 2025-08-15 | 3,70 | 4,44 |
| 2026-08-15 | 4,40 | 4,36 |

- Samlet top-5 residual **−0,561** mod andre Klampenborgdistancer, samme-møde residual **−0,805**.
- Simuleret **−0,2s**: top-5 gennemsnit **3,967 → 4,200**, lokal residual **−0,561 → −0,328**, samme-møde residual **−0,805 → −0,572**.
- Supplerende **36 ikke-uafhængige indenfor-hest par fra blot 8 heste** ændrer gennemsnitlig forskel fra **−0,314 til −0,023** ved −0,2s.
- Risiko: 2026-løbet ligger allerede omtrent som møde-øvrige distancer, og −0,2s ville ændre top-5 4,40 → 4,60 mod 4,36 på de andre distancer. Derfor **ikke godkendt som næste standardændring** på kun tre løb. Brugerens mistanke om let 1100m består som særskilt QA-note.

## Øvrige observationer
- Aalborg 1800m er relativt vanskelig at få en god gammel ranking på, men en plus-sekund justering ville gøre Aalborg stærkere relativt til Bro Park og 2024 går modsat 2025–26. **Hold den uændret nu**.
- Aalborg 1500m er relativt let, men 2024 er allerede sværere end de andre distancer; **ikke generel ændring nu**.
- Øvrevoll turf 1170m og 1730m har klasse-/årskonflikter. Øvrevoll turf 1980m netop ændret. **Ingen nye rettelser her nu**.

## Fremtidig MWP-note
Brugeren har noteret sekunder pr. gammel halvklasse i Klampenborg (1100–1300m 0,5; 1400m 0,6; 1600m 0,7; 1800m 0,8; 2200m 0,9; 2400m 1,0) og en mulig distanceafhængig sammenhæng til længder/kg. Dette er et fremtidigt forskningsspor, ikke en gyldig automatisk oversættelse mellem sekunder, længder og kg.

**Kilde:** [brugerens tilsluttede index-sheet](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), frosset v86-arkiv og de vedlagte reproducerbare scripts/CSV-filer. Ingen kildeark, historiske originaler, offsets eller live Race Studio ændret ved denne gennemgang.