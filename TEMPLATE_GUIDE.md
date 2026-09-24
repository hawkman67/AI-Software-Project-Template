# AI Software Project Template Guide

Template version: 1.0  
Last updated: 2026-09-24  
Origin: generieke werkwijze afgeleid uit lessen van Grip op Geld.

## Doel

Deze repository is een startsjabloon voor nieuwe softwareprojecten die met GitHub, Codex en AI-ondersteunde ontwikkeling worden uitgevoerd.

De template levert direct:
- een vaste Codex-router via `AGENTS.md`;
- issue-routing naar light, medium en high agents;
- een read-only scout-agent;
- scopebewaking en stille uitvoering;
- impactanalyse voor risicovolle wijzigingen;
- een vaste issue- en reviewworkflow;
- testprofielen;
- basisdocumentatie voor product en architectuur.

Deze repository is geen gedeelde runtime-afhankelijkheid. Een nieuw project krijgt een eigen kopie van de template en ontwikkelt daarna zelfstandig verder.

## Nieuw project starten

1. Maak een nieuwe repository.
2. Kopieer de inhoud van deze template naar de nieuwe repository.
3. Vul `docs/PRODUCT.md` in.
4. Vul `docs/ARCHITECTURE.md` in.
5. Vul `docs/PROJECT_CONTEXT.md` in.
6. Controleer en pas `AGENTS.md` aan voor projectspecifieke regels.
7. Voeg indien nodig domeinspecifieke documenten toe, bijvoorbeeld `DOMAIN_SAFETY.md`.
8. Controleer de agentbestanden in `.codex/agents/`.
9. Leg grote ontwerpbesluiten vast in `docs/decisions/`.
10. Start daarna pas met feature-issues.

## Kernbestanden

- `AGENTS.md`: hoofdrouter en gedragsregels voor Codex.
- `docs/PRODUCT.md`: productdoel, doelgroep, scope en productprincipes.
- `docs/ARCHITECTURE.md`: technische uitgangspunten en architectuurgrenzen.
- `docs/PROJECT_CONTEXT.md`: naslagdocument; niet standaard lezen.
- `docs/development/DEVELOPMENT_GUIDELINES.md`: conditionele documentrouter.
- `docs/development/WORKFLOW.md`: generieke ontwikkelworkflow.
- `docs/development/ISSUE_CONTRACT.md`: regels voor uitvoering en oplevering van issues.
- `docs/development/TEST_PROFILES.md`: validatieniveaus.
- `docs/decisions/`: ADR's voor blijvende ontwerpbesluiten.
- `.codex/agents/`: standaard uitvoeragents en scout.

## Wanneer impactanalyse verplicht is

Voer vóór implementatie een impactanalyse uit bij mogelijke impact op:
- databaseschema of migraties;
- persistentie;
- synchronisatie;
- gedeelde businesslogica;
- meerdere architectuurlagen;
- backward compatibility;
- bestaande gebruikersdata;
- security- of privacygrenzen.

## Wanneer een ADR gebruiken

Maak een ADR als een keuze:
- meerdere toekomstige features beïnvloedt;
- moeilijk terug te draaien is;
- architectuurgrenzen bepaalt;
- technologie of externe afhankelijkheden vastlegt;
- later opnieuw ter discussie kan komen.

Gebruik geen ADR voor gewone bugfixes of tijdelijke implementatiedetails.

## Wat niet blind kopiëren uit een bestaand project

- projectdata;
- buildhistorie;
- schema- of databaseversies;
- domeinspecifieke veiligheidsregels;
- projectspecifieke ADR's;
- oude padnamen en productnamen;
- historische besluiten.

## Template onderhouden

Wijzigingen aan deze template gelden niet automatisch voor bestaande projecten.
Bestaande projecten blijven zelfstandig. Neem verbeteringen alleen bewust over.
