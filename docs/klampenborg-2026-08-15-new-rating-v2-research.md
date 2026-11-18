# Nordic Racing – Klampenborg 15. august 2026: Ny rating v2

**Status:** Foreløbig, ikke godkendt. Originale manuelle tider, handicaps, gamle rankings og Race Studio er uændrede.

## Kilder
- Brugerens Google Sheet `index`, fanen `Races`, rækker 30433–30493 (alle 61 starter i 7 løb; bekræftet mod frosset v86-dataudtræk): https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit#gid=0&range=A30433:U30493
- Brugerens `Klampenborg - Græs` banespecifikke standardtidstabel: https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit#gid=1284952366
- `Handicap` klasseintervaller fra samme ark.
- v43 historisk officiel **før-løb handicap** fra løbsprogrammet https://www.epaper.dk/danskhv/klampenborg/klampenborg_15-08-26/ (alle 61 heste har tilknyttet HCP-post; 8 i 2-års maiden har intet tildelt HCP).

**Ingen officielle banemålinger og ingen gamle ranking-offsets bruges som input.** Officielle mål-tider bruges ikke i stedet for manuelt kontrollerede tider. Den nye rating er højere-bedre og vises som heltal, men beregnes først kontinuerligt.

## Modelopstilling (pilot)
1. Forventet nyt performancepoint = MWP-inspireret rating fra *før-løb* HCP minus (registreret analysevægt − 59 kg) × distanceafhængige længder/kg ÷ længder/nyt ratingpoint. Dette er en **foreløbig** prognose for vinderens niveau, ikke sikkerhed.
2. Den rå manuelle vindertid sammenlignes **uden forudgående vægtjustering** mod brugerens faste klassestandardtid for netop Klampenborg, græs og race-distance.
3. Rå rating = MWP-rating svarende til analyseklassens HCP-midtniveau minus (manuel tid − klassestandardtid) / (effektive sekunder pr. ratingpoint).
4. Effektive sekunder pr. point i denne pilot = (antaget mål-længde 2,50 m × manuel tid / distance) × MWP længder pr. point. **Dette er en usikker proxy for sluttempo**; ingen målt længde eller sluttids-registrering.
5. Foreløbig ny-rated korrektion = forventet − rå rating. Plus er en *langsom* præstation/baneforhold ift. forventningen, minus er hurtigere.
6. Længder/kg for 1.100m interpoleret fra MWP 1.010 og 1.200m. 1.800m = **usikker** 0,75 længde/kg; 2.400m = **usikker** 0,85 længde/kg. Sensitivitet beregnet.

## Første resultat: samtlige vindere

| Løb | Vinder | Distance | Analyseklasse | Før-løb HCP | Kg | Manuel tid | Klassetid | Forventet rating | Rå rating | +/− nye point | Kommentar |
|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 1 | Dimitria | 1100 | 4 | 66 | 64,5 | 64,3 | 65,1 | 77 | 91 | **−13** | Frontrunner; sprint 1100 interpoleret |
| 2 | Kohira | 1300 | 2-års maiden | – | 57,5 | 80,4 | – | – | – | **udeladt** | Ingen individuelt HCP eller numerisk standard |
| 3 | Codify | 1400 | 3 | 71 | 60 | 82,8 | 82,9 | 94 | 98 | **−5** | Vinder alene bedre ift. HCP end nr. 2 og 3 |
| 4 | Isaynomore | 1800 | 4 | 57 | 56,5 | 112,4 | 110,8 | 70 | 62 | **+8** | **Original note: '1 Langsom løb'** |
| 5 | Spinwell | 1800 | 2,5 | 75 | 54,5 | 109,1 | 108,4 | 108 | 102 | **+6** | Vinder let |
| 6 | Reine D'allure | 2400 | 3,5 | 73 | 61 | 154,2 | 150,6 | 97 | 62 | **+35** | Stærk tidsafvigelse; 2400m kg-effekt ikke kalibreret |
| 7 | Go Get Happy | 1600 | 5 | 58 | 70 | 99,7 | 98,9 | 57 | 44 | **+13** | Høj vægt; nyttig til vægtkontrol |

**Dagmedian, alle seks handicapløb:** +6,87 ≈ **+7 nye ratingpoint**. **Foreløbig kvalitetssortering: udelad løb 4** (konkret tempo-note) **og løb 6** (meget langt og stort afvigende resultat, samt ukalibreret længder/kg): median af løb 1,3,5,7 **+0,74 ≈ +1 nyt ratingpoint**. Hvis kun løb 6 udelades (løb 4 medtages): median **+6**.

Dette er ikke et entydigt dagligt variant-tal; individuelle løbsafvigelser varierer fra −13 til +35, og selv de fire primære kontrolløb spænder −13 til +13. **Brugeren bør ikke godkende et endeligt dags-offset endnu.** Forskelle kan skyldes taktisk tempo, særskilt distanceadfærd, evne/handicap eller fejlagtig tidskonvertering.

## Uafhængig top-3-kontrol

Modellen bruger **stadig kun vinderne til dagsmedianen**. For at forstå om én vinders individuelle HCP skaber afvigelsen har vi også set på top-3 i hvert løb, med deres egne manuelt kontrollerede tider og før-løb HCP. Foreløbig median blandt de tre første:

| Løb | Vinderkorrektion | Top-3 median | Fortolkning |
|---:|---:|---:|---|
| 1 | −13 | −13 | Alle tre hurtigere end handicapforventning (ca. −13, −17, −13) |
| 3 | −5 | +7 | Vinderen relativt hurtig; øvrige top-3 noget langsommere |
| 4 | +8 | +12 | Flere heste langsomme, passer med race-note om lavt tempo |
| 5 | +6 | +10 | Generelt langsommere end klasse-/HCP-forventning |
| 6 | +35 | +30 | Alle top-3 meget langsomme, sandsynligvis pace/distance-/standard-problem |
| 7 | +13 | +13 | De tre første samlet +13–18 |

Bemærk, at top-3 ikke er uafhængige gentagelser af løbets baneforhold. De deler løbstempo og løbstype.

## Følsomhed

Ved effektiv mål-længde mellem **2,35 og 2,70 meter**, 1.800m længder/kg mellem **0,70 og 0,80**, og 2.400m længder/kg mellem **0,70 og 1,00**:
- Median for alle seks handicapløb: **ca. +5,9 til +7,8 nye ratingpoint**.
- Median for de fire udvalgte kontrolløb (1,3,5,7): **ca. +0,4 til +1,1 nye ratingpoint**.

Disse ranges måler kun variation under de opgivne scenarier, ikke fuld statistisk usikkerhed. Antagelser om klassens benchmark, handicapniveau og løbets taktiske fart er stadig ikke valideret. Ingen påstand om kausal blødheds- eller kg-effekt.

## Gennemgang

Testside: https://olsenprivat92.github.io/nordic-racing-analytics/klampenborg-2026-08-15-rating-v2-review.html

Man kan ændre modelantagelser, medtage/udelade løb, gennemgå de tre første heste, skrive en manuel **test**korrektion og eksportere JSON. Ændringer gemmes **kun lokalt i browseren**. **Ingen Supabase-synkronisering, godkendelse eller ændring af live Race Studio.**

## Konsekvens for næste ranking-kalibrering
1. Færdigkalibrér tid pr. nyt ratingpoint efter distance ved at bruge historiske manuelt målte løb og præstationsmargener; vindertiden/gennemsnitshastigheden er ikke mål-fart.
2. Sammenlign et større antal dage med både sprint og mellemdistance og tilstrækkeligt ens historisk klasse, og brug en robust model med løb som enhed.
3. Kontroller ekstremvægt (fx Go Get Happy 70 kg) separat og uden dobbeltkompensation fra HCP.
4. Udvid top-3-analysen med pace-kontrol; hold 2-års maiden uden rating i denne metode, indtil et andet uafhængigt klasseanker findes.
5. Først derefter vis et endeligt nyt dags-ratingforslag til godkendelse.