# Codex router

Lees altijd `docs/development/DEVELOPMENT_GUIDELINES.md`. Dit is de korte conditionele router naar de verplichte projectregels.

- GitHub Issue of oplevering: volg het Issuecontract.
- Product- of testcode: volg workflow en testprofielen.
- Persistentie/schema: volg ook databaseveiligheid wanneer aanwezig.
- Officiële build/release: volg ook build- en releasebeleid wanneer aanwezig.
- Domeinspecifiek risicogebied: lees het betreffende safety-/contractdocument.

Lees alleen documenten die de router, het issue of de gebruiker voor de taak aanwijst.

Minimaliseer context, niet correctheid.

## Gedrag

### Eén source-of-truth als bouwregel

Bij iedere feature, bugfix, migratie of refactor moet voor ieder domeinfeit precies één canonieke eigenaar worden aangewezen.

Harde regels:
- bepaal vóór implementatie de canonieke eigenaar van ieder nieuw of gewijzigd domeinfeit;
- sla afgeleide state niet als tweede autoritatieve waarheid op wanneer die deterministisch berekend kan worden;
- caches, projections, snapshots, materialisaties en compatibiliteitsvelden zijn expliciet afgeleid en hebben duidelijke provenance, invalidatie en exit-semantiek;
- introduceer geen bidirectionele synchronisatie tussen twee bronnen als oplossing voor dubbele waarheid;
- scenario-/what-if-state mag nooit current masterdata muteren of current configuratie bepalen;
- legacyvelden mogen voor backward compatibility blijven bestaan, maar niet stil als functionele fallback blijven gelden wanneer een nieuw canoniek model bestaat;
- wanneer twee mogelijke eigenaren voor hetzelfde feit ontstaan: stop en kies eerst de canonieke eigenaar;
- voeg waar relevant regressietests toe die aantonen dat stale, legacy of afgeleide state de canonieke state niet kan overschrijven of maskeren.

### Scope

- Werk strikt binnen scope.
- Onderzoek geen niet-gerelateerde delen van de repository.
- Refactor geen niet-gerelateerde code zonder expliciete noodzaak.
- Voeg geen extra functionaliteit toe buiten het issue.
- Maak geen aannames over materiële product-, architectuur-, data-, security- of compatibiliteitskeuzes.
- Vraag om richting wanneer zo'n keuze noodzakelijk is en niet uit issue/projectregels volgt.
- Push nooit rechtstreeks naar `main` bij issue-uitvoering.

De opdracht `Pak issue #N op` geldt als expliciete toestemming om na succesvolle implementatie en validatie:
1. één issuebranch te gebruiken of maken;
2. de issuewijzigingen te committen;
3. de branch naar GitHub te pushen;
4. een PR naar `main` te openen of bij te werken.

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
- persistentie of bestaande gebruikersdata;
- synchronisatie;
- gedeelde businesslogica of publieke interfaces;
- meerdere architectuurlagen;
- backward compatibility;
- security of privacy;
- externe providers, versiegevoelige referentiedata of seeds;
- performance bij bulkdata;
- release/packaging/native dependencies.

Een expliciet gevraagde impactanalyse is read-only tenzij de gebruiker daarna implementatie vraagt.

## Validatie

Gebruik het passende profiel uit `docs/development/TEST_PROFILES.md`.

- Kies altijd de kleinste validatieset die de daadwerkelijk geraakte risico's afdekt.
- "Voor de zekerheid alles draaien" is geen geldige reden om de scope te verbreden.
- Start met de kleinste relevante testset; breid alleen uit op basis van concrete impact.
- `git diff --check` blijft een goedkope standaard afrondingscontrole.
- Code die potentieel grote aantallen records verwerkt krijgt waar relevant production-achtige volume- en query-countvalidatie; structurele query-/write-counts zijn belangrijker dan fragiele wall-clockgrenzen.

## Bugfixes

Na voldoende diagnose maar vóór de daadwerkelijke fix geeft Codex één compacte tussentijdse terugkoppeling met:
- concrete root cause of best onderbouwde hypothese;
- bewijs/gedrag dat dit ondersteunt;
- geraakte code-/datastroom;
- voorgestelde fix;
- materieel schema-, data-, security- of compatibiliteitsrisico.

Dit is geen stopmoment tenzij een nieuw eigenaarsbesluit nodig is.

## Steer-/follow-upberichten tijdens een lopende taak

Behandel tussentijdse berichten standaard als bijsturing van de lopende taak, niet als opdracht om te stoppen.
Stop of wacht alleen bij een expliciete instructie zoals `stop`, `pauzeer`, `wacht`, `niet verdergaan` of gelijkwaardig.

## GitHub issues en PR's

Bij implementatie van een issue:
- lees issuebody, comments, acceptatiecriteria en dependencies;
- vink alleen aantoonbaar gerealiseerde criteria af;
- voeg na succesvolle implementatie en validatie `needs-user-test` toe wanneer dat label in het project wordt gebruikt;
- sluit het issue niet zonder expliciete gebruikersgoedkeuring;
- voeg nooit zelf een eindgebruikersgoedkeuringslabel toe;
- voeg nooit zelf `gptapproved` toe wanneer het project dat label gebruikt;
- gebruik bij actieve ontwikkeling bij voorkeur een draft-PR;
- maak de PR pas review-ready nadat lokale validatie is geslaagd;
- een nieuwe commit op een review-ready PR vereist opnieuw passende validatie;
- laat de PR open voor aparte ChatGPT-code-review;
- merge niet zelf wanneer die aparte review onderdeel is van de projectworkflow.

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
6. laat die agent het issue volledig uitvoeren en valideren;
7. voer zelf geen parallelle implementatie uit;
8. inspecteer de volledige diff;
9. maak of gebruik `issue/N-korte-omschrijving`;
10. commit alleen de issuescope;
11. push de issuebranch;
12. open of update één PR naar `main`;
13. meld de PR-link en resterende review/user-test.

## Context maintenance

`docs/PROJECT_CONTEXT.md` is naslag en wordt niet standaard gelezen.

- Werk context- of decision-files alleen bij wanneer issue, wijziging of gebruiker dit vereist.
- `docs/ROADMAP.md` is het levende bouwdraaiboek wanneer het project die gebruikt; roadmaprelevante wijzigingen worden in dezelfde issuebranch bijgewerkt.
- Houd `docs/CHAT_HANDOFF.md` compact en alleen voor actuele overdraagbare context, niet als tweede roadmap of changelog.
