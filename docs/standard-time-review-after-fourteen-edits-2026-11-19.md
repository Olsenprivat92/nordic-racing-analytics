# Nordic Racing — standardtidskontrol efter 14 godkendte rettelser

**19. november 2026 · Research-only.** Begge nyeste rettelser er verificeret i den tilsluttede `index` Google Sheet; der er **ikke skrevet til brugerens kildeark eller den aktive Race Studio-model**.

## Basis

- Frozen v86 indeholder de originale manuelle tider, gamle rankings, oprindelig vægtbehandling og manuelle dags-offsets. Ingen af disse ændres.
- 10.566 manuelt rankede hestestarter i **1.327 almindelige numeriske handicapløb** fra 2024–2026, 6.577 top-5-starter, 64 bane × distance-kombinationer og 318 bane × distance × klasse-kombinationer. Maiden, vinderløb, 2-/3-årsløb, amatørløb og særskilt max-/capped-HCP er udeladt.
- Gamle rankingtrin genberegnes med de aktuelt godkendte standardtider, oprindelig rankingtid og uændret dags-offset. Den eksisterende vægtformel indeholdt allerede en vægtjustering, men **ingen ny vægtmodel, kg-omregning eller MWP-rating er anvendt i denne kontrol**. Officielle going-målinger er ikke anvendt.
- Statistik for lokale distanceforskelle er justeret for klasse, år, placering og feltstørrelse. Ekstra kontroller samme løbsdag og samme hest på forskellige distancer. **Lavere gammel ranking er bedre.**

## Bekræftet: to nyeste brugerrettelser

| Bane og distance | Standard klasse 2 før → nu | Løb / top 5 | Top 5-ranking før → nu |
|---|---:|---:|---:|
| Aalborg græs 2.000 m | 124,2 → **124,0 sek.** | 11 / 55 | 4,636 → **4,773** |
| Klampenborg græs 1.100 m | 63,1 → **62,9 sek.** | 3 / 15 | 3,967 → **4,200** |

Aalborg 2.000 m har nu klasse-/placeringsjusteret lokal distanceforskel **−0,129**, mod tidligere **−0,263**. Klampenborg 1.100 m har fortsat lokal afvigelse **−0,333**, mod tidligere **−0,561**, men kun 3 løb. Samme-hest-sammenligninger ved 1.100 m er nu tæt på nul og understøtter at **afvente flere rettelser på Klampenborg 1.100 m**.

Der er nu **14 godkendte enkeltrettelser på 13 forskellige bane-/distancerækker** (Øvrevoll græs 1.980 m er rettet i to omgange).

## Næste forslag — behandl Aalborg 1.500 og 1.800 m som ét samlet forsøg

| Aalborg græs | Nuværende klasse 2 | Forslag klasse 2 | Top 5 / løb | Nuværende top 5-ranking | Simuleret top 5-ranking |
|---|---:|---:|---:|---:|---:|
| **1.500 m** | 89,0 | **88,8 sek. (−0,2)** | 49 / 10 | 4,449 | **4,653** |
| **1.800 m** | 109,2 | **109,3 sek. (+0,1)** | 130 / 26 | 5,012 | **4,927** |

Ret **kun de udfyldte rankingtrin** i de to rækker; bevar tomme felter. Tallet i klasse 4 bliver henholdsvis **91,4 → 91,2 sek.** og **112,4 → 112,5 sek.**

### Samlet distancekontrol med begge forslag samtidig

| Aalborgs præstationer | Justeret lokal afvigelse nu | Ved begge forslag |
|---|---:|---:|
| 1.500 m | −0,437 | **−0,176** |
| 1.800 m | +0,418 | **+0,246** |
| 2.000 m | −0,129 | **−0,124** |

Den samme-model klasse-/placerings-/årsjusterede forskel **Aalborg kontra Bro Park græs** flytter sig kun fra **+0,698 → +0,694 gamle point**, hvor brugeren ønsker cirka **+1,0**. Forsøget forbedrer altså især **intern Aalborg-distancekonsistens**, ikke banens absolutte styrke. At rette kun Aalborg 1.800 m ville få Aalborg til at se unødigt stærkere ud (+0,698→+0,653).

### Forbehold og uenigheder

- **1.500 m:** 2025/26 ser for let ud; 2024 peger svagt i modsat retning. Klasse 3,5 er tæt på neutral før ændring og kan blive lidt vanskeligere. Der er kun 10 løb. 20 gensidigt afhængige samme-hest-sammenligninger fra 11 heste støtter retningen, men er ikke uafhængig dokumentation.
- **1.800 m:** 2025/26 ser for vanskelig ud, 2024 svagt modsat. Klasse 2,5 ligger allerede tæt på neutral; størst forbedring i klasse 3–4. 66 samme-hest-sammenligninger fra 24 heste støtter, at et beskedent plustillæg er relevant. +0,1 vælges bevidst i stedet for +0,2/+0,3 for ikke at øge Aalborgs generelle relative styrke for meget.
- **Øvrevoll græs 1.800 m:** 9 løb og forskellige handicapklasser, årskonflikt; afvent.
- **Aarhus græs 2.000 m:** afvigelsen er primært 2024, mens 2025/26 er næsten neutrale; afvent.
- **Klampenborg græs 1.100 m:** den nyligt godkendte −0,2 sek. er nu indregnet; afvent mere datagrundlag.

## Næste trin

Hvis begge Aalborg-ændringer godkendes, verificér live-standarderne og genberegn kontroltabellen; undersøg derefter **klasse- og årsafhængige** mønstre på Aalborg samt øvrige bane-/distancegrupper uden at forsøge at tvinge alle distancer til identisk gennemsnit. Overgangen til MWP og en ny vægtmodel forbliver et separat projekttrin.

**Kilder:** [Brugerens connected `index` Google Sheet](https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit), frozen v86-manual-rank historie, [tidligere kontroller i research branch](https://github.com/Olsenprivat92/nordic-racing-analytics/tree/feature/analysis-phase-2-foundation/docs). Reproducerbare scripts og CSV-tabeller er bevaret i researchpakken fra den aktuelle chat.