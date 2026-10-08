# Testprofielen

Kies het **laagste profiel dat de werkelijk geraakte risico's afdekt**. Een hoger profiel wordt alleen gekozen op basis van concrete impact, niet "voor de zekerheid".

| Profiel | Wanneer | Minimale controle |
| --- | --- | --- |
| Docs | Alleen documentatie, templates of workflowbestanden | diffcheck en relevante syntaxcontrole |
| Targeted | Kleine of lokaal begrensde productwijziging | format/analyze voor geraakt gebied plus gerichte regressietests |
| Development | Gedeelde applicatie-/domeinlogica of meerdere direct geraakte consumers | volledige analyse plus tests van geraakte packages/consumers |
| Database | Schema, SQL, persistentie of migratie | Development plus relevante migratie- en integriteitstests |
| Release | Officiële release, packaging/native buildwijziging of milestonevalidatie | relevante regressie plus releasecontroles |

Targeted is de normale keuze voor lokaal begrensde wijzigingen. Development betekent niet automatisch "alles draaien"; ook daar blijft de testset impactgestuurd.

## Zware controles zijn opt-in op impact

De volgende controles zijn niet standaard verplicht per issue:
- volledige workspace-/package-testmatrix;
- alle platformbuilds;
- production-volume-/jaarharnassen;
- installatie-/packagingtests;
- end-to-end suites tegen echte externe providers.

Gebruik ze alleen wanneer de diff het betreffende risico raakt.

Voorbeelden:
- native/buildconfig, packaging/assets, plugin/FFI -> relevante platform/releasebuild;
- bulk-, materialisatie- of querygedrag -> production-achtige volume- en query-counttest;
- breed gedeeld contract -> transitieve consumers/fullere suite;
- providerintegratie -> deterministic fixtures/fakes plus gerichte contracttest; live provider alleen wanneer expliciet veilig en nodig.

## Databasetests

Bij het Database-profiel test je waar relevant:
- fresh schema;
- ondersteund migratiepad;
- constraints en foreign keys;
- behoud van bestaande gebruikersdata;
- heropenen na migratie;
- unknown/null-semantiek;
- herstel van derived/cache stores zonder canonieke data te muteren.

## Regressieregel

Een bugfix krijgt waar praktisch een test die vóór de fix faalt en na de fix slaagt.
De regressietest hoort bij de centrale eigenaar van de regel, niet alleen bij de UI waar het symptoom zichtbaar was.

## Altijd goedkoop

`git diff --check` blijft een standaard afrondingscontrole.

Projectspecifieke commando's en scripts worden ingevuld zodra de technische stack is gekozen, bij voorkeur in dit document en `BUILD_AND_RUN.md`.
