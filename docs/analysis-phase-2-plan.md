# Nordic Racing — Analysefase 2 (v31 fundament)

**Status:** teknisk fundament / forsøgsdesign. Ikke en godkendt ny produktionsmodel.

## Datagrundlag og beskyttede regler

- Hidtidige manuelle rankings må ikke omskrives. Den historiske skala 0–11 med 0,5-trin forbliver et rådatagrundlag (`manual_ranking_v1`). Lavere = bedre.
- Kun manuelle rankings 2024–2026 må anvendes som målvariabel, så 2013–2023 ikke får fabrikerede ratingtal. Historiske starter uden verificerede rankings er `missing`, ikke 0.
- Officielle, **før-løbet** handicap skal kunne bruges som selvstændigt signal. `official_zero_as_printed`, `not_yet_assigned` og `not_retrieved` er tre forskellige tilstande.
- Vægt: anvend base-/tildelt analysevægt før lærlingelettelse, og behold båret vægt separat. Når baneprogrammet har to vægte for samme hest, er den højeste det autoritative analysefelt (med kilde/proveniens).
- Startspor er nummereringen for de tilbageværende aktive programheste, dvs. udgåelser rykker følgende heste op.
- Større ændringer skal versionsmærkes, evalueres på fremtidige/holdout-løb og aldrig retroaktivt erstatte gemte før-løbet prognoser.

## Arbejdspakker

### 1. Finere performance-ranking
- V1 = behold 0–11/0,5 urørt; V2 = kontinuerlig latent performance-score, fx 0,1-trin *kun i afledt score*.
- Kombiner flere observerbare input: manuel ranking, konkurrentstyrke, faktisk margin/tid når verificeret, løbsklasse, alder/underlag/distance, race-day forhold og gyldigt før-start HCP. Ikke en simpel konvertering fra HCP til gammel ranking.
- Kalibrér på løb der ikke indgår i træning, med rullende tidsvindue og isolér løbsdage, heste og data-cutoffs. Evaluer out-of-sample tab for topvalg og A-E kalibrering.
- Rå ranking, officiel HCP, afledt performance og endelig modelscore holdes adskilt i datalaget og vises som separate felter.

### 2. Trip – observation frem for gæt
- `trip_review_status`: `not_reviewed`, `reviewed_no_incident`, `reviewed_event`.
- Standard hændelser: `blocked`, `wide_trip`, `poor_start`, `traffic`, `pace_disadvantage`, `ground_loss`, `clear_run`, `other`.
- Registrér fase (start/sving/opløb), alvor (`mild`, `medium`, `severe`), beviskilde (video/kommentar), fritekst og reviewer. Ingen trip-justering uden indberetning/verificering.
- Gem også positive ture og vægtning af modvind/baneposition som separate signaler; undgå dobbeltregning af allerede tids-/marginjusterede tal.

### 3. Vægt × distance
- Behold nuværende konstant `2 længder/kg` som versionsstyret reference, ikke som facit.
- Svensk Galopp angiver omtrent `0,5 længde/kg @ 1.200 m`, `1,0 @ 1.600 m` og `1,5 @ 2.400 m`. Foreløbig interpolation på afstand, særskilt kalibrering for dirt/turf og kurs.
- Brug `lengths_per_kg(distance, surface, course, going)`; kun kalibreret output efter sample-size- og generaliseringstests.
- Sammenlign mindst: gamle regel, officiel referencekurve, empirisk estimeret kurve; forbehold for selektionsbias i handicaps og for at odds/resultat ikke må lække ind i pre-race features.

### 4. A–E prognosearkiv og obligatorisk efteranalyse
- Ét **uændringsbart før-løbet snapshot** for hver gemt prognose, med model- og egen rating, A–E for begge, rank, event/race/runner-key, modelversion, cutoff, startspor og tilgængelig markedsinfo før løbet.
- Når officielle resultater er importeret, evaluer vind/top3/placering og evt. ROI ved konkrete spilvalg (vis ikke en realiseret ROI hvis ingen spilvalg er gemt).
- For heste med **egen A–E-vurdering C, D eller E** før løbet oprettes et `review_required` efter løbet. Efteranalysen kan ikke markeres afsluttet uden årsagstype og begrundelsestekst; fremhæv især fejlbedømte outsidere. Indtil konkret gruppe-metode er aftalt gemmes gruppen som label uden gættede tærskler.
- Resultatimport og reviewdata er to adskilte, kildeangivne lag; manuelle ændringer efter løbsstart må ikke omskrive den låste prognose.
- Retrospektive/historiske replay-tests skal holdes skarpt adskilt fra ægte før-start prognoser.

### 5. Analysevisninger – genbrug tidligere sites arbejdsgange
- **Course Analysis:** bane + turf/dirt, distance, klasse, startspor efter udgåelser, going, antal starter og konfidens.
- **Trainer Analysis:** samlet/nylig, bane+underlag, distancer/klasser, ændringer ved trænerskift og tilstrækkelig stikprøvestørrelse.
- **Jockey Analysis:** samme dimensioner, herunder lærlingefradrag og jockey/hest-forbindelse.
- **Horse Analysis:** trend/årstoppe, historiske manuelle rankings, official pre-race HCP, vægte, hestespecifikke Trip-markeringer og noter.
- **Breeding Analysis:** sire/dam og dokumenteret pedigree, primært 2-årige/3-årige og maiden med usikkerhedsmarkering.
- **Performance Analysis:** historisk model versus egne A–E, vintal/top3-kalibrering, Brier score/log loss når sandsynligheder findes, grupper, år/bane/underlag/distance/klasse, fejlmønstre, reviewkø, modelversioner.

## Implementering og rækkefølge
1. Snapshot- og reviewdatamodel med autentifikation/RLS. Uden ændringer af live model.
2. Afprøv workflow på testløb med syntetisk data og sikre, at låste snapshots ikke kan ændres; samme login på computer/mobil.
3. Indlæs **kildeverificerede** resultater og opret reviewkø for C–E. A–E definition først som policy efter aftale; ikke bagudkonstruere ægte før-start picks.
4. Implementér analysevisninger mod historiske data og faktiske prognoser; vis datadækning og konfidens.
5. Benchmarks for vægt og ranking; vælg ny version kun ved dokumenteret holdout-forbedring.

## Kendte databegrænsninger, observeret i v30
- Demoen Bro Park 15. november 2026: 56 programheste og 824 synlige historiske starter; **alle 824 har `trip: null`**.
- Historisk handicaptal er kun delvist kildeverificeret i demoen; v43 overlay-kandidat indeholder 110.670 start-id'er, men er ikke i sig selv hele starts-/rankingdatabasen.
- Den publicerede Race Studio-visning er en historisk research-demo, ikke en fremtidig live løbsdag. Efterprøvning på faktiske fremtidige prognoser kræver nye løbsdage/resultater.

## Litteratur / reference for vægt
- Svensk Galopp: `https://www.svenskgalopp.se/documents/2967/Bro_250709_uppslag.pdf` (vejledning; 1200/1600/2400 m approx.)
- BHA: `https://www.britishhorseracing.com/regulation/performance-figures/` (lbs/length ændres med distance/going)

**Note:** Teksten er en arbejdsplan; kriterier, præcision, holdout og Trip-skala afklares før modelændring.