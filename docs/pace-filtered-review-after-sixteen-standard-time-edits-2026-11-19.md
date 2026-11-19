# Nordic Racing — konsekvens af at fjerne langsomme og kunstige løb fra standardtidskontrollen

**Dato:** 19. november 2026  
**Status:** Analysen er genberegnet; ingen originale data eller Google Sheets-tidstabeller er ændret.

## Afgrænsning

Udgangspunktet er 10.566 manuelt rankede hestestarter i 1.327 **almindelige numeriske handicapløb** fra 2024–2026. Ældre-vinderløb, 2-/3-årsløb, maiden, amatør- og særligt max-/capped-handicapløb indgår ikke.

Et løb udelades **i sin helhed** fra standardtidskalibreringen, hvis mindst én tilknyttet løbskommentar eksplicit siger **»Langsomt løb«** (herunder nummererede stavemåder) eller **»Kunstigt løb«**. Hesteindividuelle bemærkninger som »langsom fra start« udelader ikke løbet. Tidskvalitetsanmærkninger er en anden QA-kategori.

- **37** løb med eksplicit langsomt løb, **65** løb med kunstigt løb; **102 unikke** løb (ingen overlap).
- **733 starter og 495 top-5 placeringer** fravælges; **1.225 løb, 9.833 starter og 6.082 top-5** beholdes.
- Årsfordeling af udeladte løb: 2024 **39**, 2025 **25**, 2026 **38**.
- Det tidligere omtalte tal **103** omfattede **ét yderligere løb med anden tempokommentar**; brugerens præcise nye filter udelader kun 102. Dette ekstra løb kan senere flagges separat.
- Top-5-gennemsnittet på de **aktuelle 16 bruger-korrigerede gamle standardtider** ændres fra **3,930 til 3,869** (lavere gammel ranking er bedre).

## Virkning på hidtidige tidstabelændringer

16 separate brugerrettelser berører **15 unikke bane-/distancerækker**, fordi Øvrevoll græs 1.980 m er ændret to gange.

Ved at sammenholde den nuværende og hypotetisk tilbageførte præstation på **det filtrerede datasæt**, med fælles referencejustering for klasse, år, placering og feltstørrelse, reducerer **14 af 15 rækker** afvigelsen fra banens øvrige distancer. Én gør den større. Dette er en *diagnostisk* og retrospektiv kontrol, ikke et kausalt bevis for, at den ændrede standard er korrekt.

| Ændret bane/distance | Løb tilbage | Gammel lokal afvigelse uden ændringen (estimat) | Aktuel lokal afvigelse | Fortolkning |
|---|---:|---:|---:|---|
| Göteborg græs **2.400 m** (samlet +0,4 s) | **9** af 14 | **+0,05** | **−0,19** | **Bør revurderes**: aktuel standard er for lempelig i det filtrerede udsnit |
| Göteborg græs 2.200 m (+0,9 s) | 27 af 32 | +0,36 | −0,14 | Stor forbedring i absolut distancebalance; mindre overkorrektion mulig, men behold indtil videre |
| Øvrevoll græs 1.980 m (samlet +0,6 s) | 9 af 11 | +0,78 | +0,39 | Hjælper tydeligt, men kun få løb; justér ikke mere nu |
| Bro Park dirt 1.200 m (−0,1 s) | 34 af 38 | −0,44 | −0,33 | Hjælper, men stadig lidt for let – klasser 2 og 3 er modstridende |
| Øvrevoll dirt 1.100 m (−0,1 s) | 65 af 70 | −0,35 | −0,25 | Hjælper, men er ikke færdigkalibreret på tværs af klasser |
| Bro Park græs 1.200 m (+0,1 s) | 12 af 13 | +0,08 | −0,00 | Meget god balance efter filter; behold |
| Klampenborg græs 1.100 m (−0,2 s) | 3 af 3 | −0,48 | −0,25 | Hjælper, men 3 løb er for få til yderligere rettelser |

Alle 15 rækker, startantal, top5-forskelle og klasser er dokumenteret i Excel-rapporten.

### Baner hvor filteret ændrer konklusionen mest

Følgende er **klasse-/år-/placeringsjusteret afvigelse i gamle rankingpoint fra den pågældende banes andre distancer**; tal er genberegnet med aktuelle standardtider og separate kontrolmodeller før/efter filtrering:

| Bane/distance | Med alle løb | Uden langsomt/kunstigt løb | Løb fravalgt |
|---|---:|---:|---:|
| Göteborg græs 2.400 m | +0,22 | **−0,19** | 5 af 14 |
| Bro Park dirt 1.200 m | −0,16 | **−0,33** | 4 af 38 |
| Aarhus græs 2.000 m | +0,40 | **+0,22** | 4 af 31 |
| Øvrevoll græs 1.170 m | +0,31 | **+0,40** | 5 af 31 |
| Klampenborg græs 2.400 m | +0,22 | **+0,16** | 3 af 13 |

Aarhus 2.000 m fremstår markant mindre afvigende. Notér dog, at **2024-05-05 løb 4** ikke er eksplicit tempomarkeret og derfor fortsat indgår; dette løb bør kvalitetstjekkes separat, ikke automatisk udelukkes.

## Mine næste forslag – efter det nye filter

**1. Göteborg græs 2.400 meter: revider den samlede rettelse fra +0,4 til +0,2 sekunder.**
- Aktuel standard **klasse 2 = 145,2 s**, foreslået **145,0 s**: dvs. **−0,2 s fra den nuværende tabel** på alle udfyldte trin 1–11; trin 0 uændret.
- 9 løb / 45 top-5-starter efter filtrering. Lokal afvigelse **−0,185 → −0,085** gamle rankingpoint. Årsafvigelser 2024 **−0,343 → −0,243**, 2025 **−0,022 → +0,045**, 2026 **−0,185 → −0,052**. Tre handicapklasser 2,5/3/3,5 får samlet set en mere rimelig balance; kl. 3,5 går dog fra −0,019 til +0,081, så der er stadig tradeoffs.
- En større tilbagerulning kan forbedre det samlede gennemsnit, men gør enkelte år og klasser mindre sikre. **Foreslå halv tilbagerulning som første forsøg.**

**2. Øvrevoll græs 1.170 meter: test +0,1 sekund.**
- Aktuel standard klasse 2 **68,1 s**, foreslået **68,2 s**; øvrige udfyldte trin 1–11 +0,1s, grad 0 uændret.
- 26 løb / 130 top-5-starter efter filtrering. Lokal afvigelse **+0,401 → +0,301**. De tre års forskelle **2024 +0,661 → +0,550**, **2025 +0,360 → +0,278**, **2026 +0,104 → −0,013**. 128 hestepar-sammenligninger (37 forskellige heste) giver +0,248 old points for 1170m på tværs af distancer: understøtter retningen, men parrene er indbyrdes korrelerede.
- Nogle klasser (2,0 og 3,5) er allerede nær nul og kan blive en smule for gode. **Kun lille +0,1 s indtil mere QA.**

**Afvent Bro Park dirt 1.200 meter.** En ekstra −0,1 s ville forbedre lokal top5-afvigelse **−0,327 → −0,201** og samme-dags-kontrollen, men **klasse 2/3 bliver for dårlige**, især klasse 3 går +0,060→+0,160. Den historiske forskel i samme hests præstationer støtter fortsat, at sprintstandarden kan være for let, men hele klasserækken bør ikke flyttes igen uden en klasseopdelt plan.

**Afvent også Øvrevoll dirt 1.100 meter, Øvrevoll græs 2.400 meter og Aarhus 2.000 meter**; de nuværende års-/klasseforskelle gør én samlet sekundrettelse usikker. Klampenborg 1.100 m er fortsat til senere opfølgning.

## Videre proces

1. Anvend løbs-tempofilteret som **fast standard for standardtidskalibrering**; vis antal tilbageværende løb og top5 i alle fremtidige analyser.
2. Brug aktuelle godkendte 16 rettelser indtil brugeren godkender nye forslag; **gennemfør ikke automatisk tilbageførsel**.
3. Kontrollér særskilt »Tiden kan ikke verificeres« og øvrige ikke-standard-kommentarer. Disse er **ikke automatisk udeladt** med den nuværende regel.
4. Bevar alle originale manuelle tider, dags-offsets og gamle hesterankings i databasen. Udeladelsen gælder **kun kalibreringsudsnittet**, ikke løbshistorikken, og senere også udvalg af løb til at estimere MWP-mødets going-korrektion.
5. Brugerens ønskede forskelle i banestyrke holdes som sidekontrol (Bro Park stærkest på græs, Jægersro på dirt), men må ikke automatisk tvinge standarderne til et på forhånd bestemt gennemsnit.

**Vigtige forbehold:** Dette er en retrospektiv analyse. Ingen blind holdout, 0,5-trinsdiskret rank kan gøre +0,1s forskelle ujævne, og nogle distancer har kun få kvalificerende løb. Ingen officielle banemålinger, ingen separat ny vægtmodel og ingen MWP omregning er brugt her.

### Kilder og arbejdsfiler

- Originalt brugerark: https://docs.google.com/spreadsheets/d/1DuHZC6EjYRX5UHr5hyjejBRY9BKPIyyfhP46jfDp_p8/edit
- Historisk v86-frossen rankingdatabase i brugerens projektfiler samt kommentarer fra tabellen `starts`.
- `01_race_flags_102.csv`, `02_all_vs_filtered_course_distance.csv`, `03_filtered_class_cells.csv`, `06_approved_edits_reassessment_filtered.csv`, `07_candidate_scenarios_filtered.csv`, `08_candidate_class_scenarios.csv`, `09_within_horse_filtered.csv`.
- Reproducerbar beregningskode: `run_analysis.py`, `test_scenarios.py`, `within_horse_check.py`.