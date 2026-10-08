# AI Software Project Template Guide

Template version: 2.0  
Last updated: 2026-10-08  
Origin: generieke werkwijze afgeleid uit praktijklessen van Grip op Geld en Grip op Energie.

## Doel

Deze repository is een startsjabloon voor softwareprojecten die met GitHub, Codex en aparte ChatGPT-review worden ontwikkeld.

De template levert direct:
- een vaste Codex-router via `AGENTS.md`;
- issue-routing naar light, medium en high agents;
- een read-only scout-agent;
- harde source-of-truth-regels;
- scopebewaking en impactanalyse;
- issue-, branch-, PR- en reviewdiscipline;
- gerichte testprofielen;
- database- en data-eigenaarschapregels;
- templates voor product, architectuur, roadmap, observability en handoff;
- ADR-structuur.

Deze repository is geen gedeelde runtime-afhankelijkheid. Een nieuw project krijgt een zelfstandige kopie en ontwikkelt daarna zelfstandig verder.

## Nieuw project starten

1. Maak een nieuwe repository vanuit deze template.
2. Vul `docs/PRODUCT.md` in: probleem, doelgroep, scope, succescriteria en expliciete non-goals.
3. Vul `docs/ARCHITECTURE.md` in: lagen, boundaries, canonieke data-eigenaren, externe providers en deployment.
4. Vul `docs/PROJECT_CONTEXT.md` compact in met blijvende projectcontext.
5. Vul `docs/ROADMAP.md` in met de eerste bouwvolgorde en beslispoorten.
6. Vul `docs/development/BUILD_AND_RUN.md` in zodra stack en platforms gekozen zijn.
7. Controleer `AGENTS.md` en voeg alleen projectspecifieke regels toe die echt blijvend zijn.
8. Definieer projectlabels, minimaal de Codex-routerlabels en eventueel `needs-user-test` / `gptapproved`.
9. Controleer `.codex/agents/`.
10. Leg grote ontwerpbesluiten vast in `docs/decisions/`.
11. Start daarna pas met feature-issues.

## Kernbestanden

- `AGENTS.md`: hoofdrouter en harde gedrags-/kwaliteitsregels voor Codex.
- `docs/PRODUCT.md`: productdoel, doelgroep, scope en productprincipes.
- `docs/ARCHITECTURE.md`: technische uitgangspunten, boundaries en sources-of-truth.
- `docs/PROJECT_CONTEXT.md`: naslag; niet standaard lezen.
- `docs/ROADMAP.md`: levende bouwvolgorde en actuele positie.
- `docs/CHAT_HANDOFF.md`: compacte overdracht van actuele context tussen chats/sessies.
- `docs/OBSERVABILITY.md`: logging-, privacy- en supportbaseline.
- `docs/development/DEVELOPMENT_GUIDELINES.md`: conditionele documentrouter.
- `docs/development/WORKFLOW.md`: generieke ontwikkel- en bugfixworkflow.
- `docs/development/ISSUE_CONTRACT.md`: issue-, branch-, PR-, roadmap- en reviewcontract.
- `docs/development/TEST_PROFILES.md`: impactgestuurde validatieniveaus.
- `docs/development/DATABASE_SAFETY.md`: migratie-, integriteits- en derived-dataregels.
- `docs/development/BUILD_AND_RUN.md`: project-specifieke build-, run- en releasecommando's.
- `docs/decisions/`: ADR's voor blijvende ontwerpbesluiten.
- `.codex/agents/`: standaard uitvoeragents en scout.

## Belangrijkste geleerde bouwregels

### 1. Eén waarheid per domeinfeit

Leg per domeinfeit één canonieke eigenaar vast. UI-state, caches, materialisaties, scenario's, projections en legacyvelden mogen nooit ongemerkt een tweede waarheid worden.

### 2. Scheid werkelijkheid, scenario en derived state

Current/masterdata, scenario-input en afgeleide resultaten zijn verschillende categorieën. Scenario's mogen de werkelijkheid niet muteren. Reproduceerbare derived data hoort opnieuw opbouwbaar te zijn en een duidelijke invalidatie/fingerprint te hebben.

### 3. Impactanalyse vóór riskante wijzigingen

Analyseer eerst de gevolgen wanneer schema, persistentie, gedeelde logica, bestaande data, security/privacy, providers, compatibiliteit of performance geraakt kunnen worden.

### 4. Test risico's, niet de hele wereld

Gebruik het laagste profiel dat de werkelijke impact afdekt. Volledige suites, releasebuilds en production-volume-harnassen zijn opt-in op aantoonbaar risico.

### 5. Bugs eerst begrijpen

Reproduceer, lokaliseer de root cause en herstel de centrale eigenaar van de regel. Voeg waar praktisch een regressietest toe vóór of samen met de fix.

### 6. Issues zijn uitvoercontracten

Een goed issue bevat probleem, scope/non-goals, gekozen semantiek, acceptatiecriteria, data-/migratie-impact, tests en relevante dependencies. Materiële keuzes horen vóór implementatie expliciet te zijn.

### 7. PR is niet hetzelfde als klaar

Normale flow:
`issue -> issuebranch -> implementatie -> lokale validatie -> draft PR -> review-ready -> aparte ChatGPT-review -> user-test/merge`.

### 8. Externe data is versiegevoelig

Voor seeds, referentiedata en providerdata: versie, provenance, effective date, integriteitscontrole, updatepad en fallbackgedrag expliciet maken. Hardcoded beleids-/tarief-/referentiedata in code vermijden wanneer die los onderhoudbaar hoort te zijn.

### 9. Documentatie heeft verschillende rollen

- Product: waarom/wat.
- Architectuur: blijvende technische grenzen.
- ADR: één blijvende keuze.
- Roadmap: volgorde/status.
- Project context: compact naslagwerk.
- Handoff: alleen actuele overdracht.
- Issue: concrete uitvoerscope.

Maak van geen enkel document een tweede bron van waarheid voor status of gedrag.

## Wanneer een ADR gebruiken

Maak een ADR als een keuze:
- meerdere toekomstige features beïnvloedt;
- moeilijk terug te draaien is;
- architectuurgrenzen of data-eigenaarschap bepaalt;
- technologie of externe afhankelijkheden vastlegt;
- scenario/current-semantiek bepaalt;
- later opnieuw ter discussie kan komen.

Gebruik geen ADR voor gewone bugfixes of tijdelijke implementatiedetails.

## Wat niet blind kopiëren uit een bestaand project

- productdata of domeinspecifieke berekeningen;
- buildhistorie;
- schema- of databaseversies;
- projectspecifieke veiligheidsregels;
- project-ADR's;
- oude padnamen en productnamen;
- historische handofftekst;
- specifieke providercredentials/endpoints;
- testcommando's voor een stack die het nieuwe project niet gebruikt.

## Template onderhouden

Wijzigingen aan deze template gelden niet automatisch voor bestaande projecten.
Neem verbeteringen bewust over en voorkom dat projectspecifieke uitzonderingen teruglekken in de generieke basis.
