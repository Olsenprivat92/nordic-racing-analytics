# Nordic Racing — samlet distancekontrol efter 11 brugerrettelser

**19. november 2026 · Kun forslag og kontrol.** Ingen kildetidstabeller, originale tider, rangeringer, dags-offsets eller Race Studio-data er ændret af denne analyse.

## Bekræftet seneste ændring
Øvrevoll græs, 1.980 m: klasse 2-standard **122,2 → 122,4 s**, klasse 4 **125,4 → 125,6 s** (den seneste ændring er +0,2 s; samlet +0,6 s i forhold til den arkiverede standard). Dermed er **11 manuelle justeringer** registreret på **10 forskellige bane-/distancerækker**. De 10 reviderede rækker er genberegnet ud fra de arkiverede manuelle tider og de oprindelige dags-offsets, ikke skrevet tilbage til kildedata.

## Datagrundlag
- **10.566 manuelt rankede hestestarter**, **1.327 almindelige numeriske handicapløb**, **6.577 top-5-starter** fra 2024–2026, ekskluderer amatør-, 2-års-, 3-års-, vinder- og max-/capped-handicapløb.
- **64 bane × distance**-kombinationer (11 bane-/underlagskombinationer med mindst ét kvalificeret handicap), **318 bane × distance × klasse**-kombinationer.
- Gammel skala: **lavere ranking = bedre**. Manuelle dags-offsets bevares, og der foretages **ingen ny vægtkorrektion**. Ingen officiel banemåling eller MWP-score indgår.
- Top-5-residualer kontrollerer for handicapklasse, placering i feltet, feltstørrelse og kalenderår, men kan ikke fuldt ud isolere tempo, distancepræferencer eller hestekvalitet. Samme-dags sammenligninger og sammenligninger af samme hest på forskellige distancer bruges som supplerende QA. Sidstnævnte omfatter 3.538 **ikke-uafhængige par** fra 535 heste, og må ikke forveksles med en formel effektmåling.
- Kildedata: brugerens [Google Sheet index](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), det frosne v86-arkiv og tidligere revisionspakker. Eksakte underliggende rækker i vedhæftet Excel/CSV.

## De vigtigste resterende afstandssignaler

| Bane × distance | Top-5 / handicapløb | Indenfor-bane top-5-forskel (gamle point) | Samme hest, øvrige distancer | Vurdering |
|---|---:|---:|---:|---|
| **Klampenborg græs 1.100 m** | 15 / 3 | **−0,56** (lettere ranking) | −0,31 over 36 par, 8 heste | **Prioritér manuel QA**; meget lille løbsantal og 2026-løbet er ikke tydeligt for let |
| **Bro Park græs 1.200 m** | 64 / 13 | **+0,22** (sværere ranking) | +0,57 over 61 par, 21 heste | **Forsigtigt forslag: +0,1 s** på grade 1–11 |
| **Aalborg græs 1.800 m** | 130 / 26 | **+0,48** | +0,49 over 66 par, 24 heste | Undersøg 2024 mod 2025–26 og banestyrkemål; **ingen automatisk +s**, da det ville gøre Aalborg stærkere relativt til Bro Park |
| **Øvrevoll græs 1.170 m** | 155 / 31 | +0,31 | +0,04 over 209 par, 43 heste | **Ingen rettelse endnu**: samme-hest-kontrollen og 2026 er ikke enige med samlet mønster |
| **Øvrevoll græs 1.980 m** | 53 / 11 | +0,37 | +0,56 over 89 par, 27 heste | Netop justeret; 2026 residual ~+0,01, så **ingen ny rettelse** nu |
| **Øvrevoll græs 2.400 m** | 115 / 23 | −0,35 | −0,13 over 140 par, 28 heste | Historisk let, men 2026 neutral; **ingen generel ændring** |
| **Aarhus græs 2.000 m** | 154 / 31 | +0,39 | +0,62 over 55 par, 29 heste | Næsten hele årsafvigelsen i 2024; **ingen generel ændring** |
| **Klampenborg græs 2.400 m** | 60 / 13 | +0,22 | +0,36 over 63 par, 23 heste | 2026 driver forskellen; ny standardjustering allerede gennemført; **afvent** |

En positiv afvigelse betyder en for **dårlig** gammel ranking relativt til andre distancer på samme bane efter specificeret klasse-/placering-/årsjustering; negativ betyder en **for god** ranking. Parresultater er fortegnet tilsvarende. Disse residualer er ikke MWP-point.

## Konkrete næste testforslag
**Bro Park græs 1.200 m: +0,1 sekunder** på rankingtrin 1–11, uændret trin 0. **Klasse 2: 69,6 → 69,7 sekunder** og **klasse 4: 71,6 → 71,7 sekunder**. Simuleret top-5-gennemsnit **3,59 → 3,50**, internt justeret residual **+0,22 → +0,12**. I 2024 +0,107→−0,018, 2025 +0,587→+0,482, i 2026 −0,120→−0,170. Derfor ikke anbefale +0,2 på nuværende grundlag; det ville forringe 2026 betydeligt mere. De to mest repræsenterede klasser 2 og 2,5 har begge positive residualer mod samme klasse på andre Bro Park-græsdistancer.

**Klampenborg græs 1.100 m: afvent ændring.** De tre kvalificerede klasse-4 løb er:
- 16. august 2024, Soup Or Sonic: top 5 **3,80** vs andre distancer på samme møde **4,10**.
- 15. august 2025, Soup Or Sonic: **3,70** vs **4,44**.
- 15. august 2026, Dimitria: **4,40** vs **4,36** (ingen lethed dette år).

En *kun simuleret* −0,2s justering flytter intern top-5-afvigelse fra −0,56 til cirka −0,33; −0,4s giver ca. −0,09, men et så stort indgreb er **ikke underbygget af tre løb**, og ville gøre 2026-løbet markant dårligere end sammenligningsløbene. Vent til vi kan analysere race-pace, mere historisk evidence og distancer mere generelt. Hvis brugeren ønsker, kan 1.100m fortsat sættes på særskilt review-listen, uden at ændre tabellen.

## Hvad vi gør efter denne runde
1. Hvis brugeren ønsker det, ret **kun Bro Park græs 1.200 m +0,1 sek.** og genberegn historiske sammenligninger.
2. Afslut **klassevis** kontrol af Aalborg 1.800m og Øvrevoll græs 1.980m; kig på om de forskellige år og hestegrupper forklarer afvigelserne. Nye distancetidstabeller må ikke tvinge alle baner til samme niveau, da brugeren har fastlagt styrkeforskelle.
3. Få særskilt kontrol af Klampenborg 1.100m med flere sammenlignelige data før rettelse.
4. **Først derefter** begynd ny MWP-kalibrering; behold noten om historiske tidsspring per halv gammel rankinggrad (0,5s på 1100–1300m til 1,0s på 2400m) og brugerens hypotese om længder/kg. De er forskellige fysiske størrelser og må ikke sidestilles uden særskilt kalibrering.

**Ingen kildeændringer foretaget i denne runde.**