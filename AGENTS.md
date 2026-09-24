# Codex router

Lees altijd `docs/development/DEVELOPMENT_GUIDELINES.md`. Dit is de korte conditionele router naar de verplichte projectregels.

- GitHub Issue of oplevering: volg het Issuecontract.
- Product- of testcode: volg workflow en testprofielen.
- Persistentie/schema: volg ook databaseveiligheid wanneer aanwezig.
- Officiële build/release: volg ook releasebeleid wanneer aanwezig.

Lees alleen documenten die de router, het issue of de gebruiker voor de taak aanwijst.

Minimaliseer context, niet correctheid.

## Gedrag

- Werk strikt binnen scope.
- Onderzoek geen niet-gerelateerde delen van de repository.
- Refactor geen niet-gerelateerde code zonder expliciete noodzaak.
- Voeg geen extra functionaliteit toe buiten het issue.
- Maak geen aannames over materiële product-, architectuur-, data- of compatibiliteitskeuzes.
- Vraag om richting als zo'n keuze noodzakelijk is en niet uit het issue volgt.
- Maak zonder expliciete opdracht geen commit of push.

## Repository exploration

Gebruik gerichte zoekacties op symbolen, bestanden en relevante codepaden.
Stop met verkennen zodra de relevante scope voldoende duidelijk is.

Gebruik de read-only subagent `scout` alleen wanneer gerichte discovery anders onnodig veel uitvoercontext kost.

`scout` mag:
- relevante bestanden vinden;
- callers en dependencies identificeren;
- relevante tests vinden;
- database/schema/migratie-impact signaleren;
- bestaande patronen lokaliseren.

`scout` mag niet:
- implementeren;
- requirements interpreteren;
- architectuur- of productbeslissingen nemen;
- builds uitvoeren;
- GitHub-afronding uitvoeren.

## Impactanalyse

Voer vóór implementatie een impactanalyse uit wanneer een wijziging mogelijk materiële gevolgen heeft voor:
- databaseschema of migraties;
- persistentie;
- synchronisatie;
- gedeelde businesslogica;
- meerdere architectuurlagen;
- backward compatibility;
- bestaande gebruikersdata;
- security of privacy.

Een expliciet gevraagde impactanalyse is read-only.

## Validatie

Gebruik het passende profiel uit `docs/development/TEST_PROFILES.md`.

Rapporteer succesvolle validatie compact. Toon volledige logs alleen wanneer fouten dit nodig maken.

## Communicatie

Werk zonder tussentijdse voortgangstekst tenzij een blokkade, onverwacht risico of eigenaarsbesluit nodig is.
Geef geen stap-voor-stap voortgangsbeschrijving.

Eindrapportage blijft kort:
- wijziging;
- validatie;
- open punt.

## GitHub issues

Bij implementatie van een issue:
- lees issuebody, comments, acceptatiecriteria en relevante dependencies;
- vink alleen aantoonbaar gerealiseerde criteria af;
- voeg na succesvolle implementatie en validatie het label `needs-user-test` toe indien dat label in het project wordt gebruikt;
- sluit het issue niet zonder expliciete gebruikersgoedkeuring;
- voeg nooit zelf een eindgebruikersgoedkeuringslabel toe.

## Codex routering op GitHub-label

- `codex:light` -> `issue_light`
- `codex:medium` -> `issue_medium`
- `codex:high` -> `issue_high`
- `codex:niet-uitvoeren` -> stop en wijzig niets

Bij `Pak issue #N op`:
1. lees issue en labels;
2. stop bij `codex:niet-uitvoeren`;
3. stop bij conflicterende uitvoerlabels;
4. stop wanneer geen uitvoerlabel aanwezig is;
5. kies exact één uitvoeragent;
6. laat die agent het issue volledig uitvoeren;
7. voer zelf geen parallelle implementatie uit.

## Context maintenance

`docs/PROJECT_CONTEXT.md` is naslag en wordt niet standaard gelezen.

Werk alleen context- of decision-files bij wanneer het issue of de gebruiker dit expliciet vereist.
