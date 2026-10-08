# Algemene workflow

## Bronnen en scope

- GitHub Issues bepalen wat wordt gebouwd.
- De repository bepaalt wat al bestaat.
- `docs/PRODUCT.md` bepaalt productdoel en productgrenzen.
- `docs/ARCHITECTURE.md` bepaalt blijvende architectuurgrenzen.
- ADR's bepalen expliciet vastgelegde blijvende keuzes.
- `docs/ROADMAP.md` bepaalt volgorde/status, niet de implementatiesemantiek.
- Houd wijzigingen gericht en behoud bestaand gedrag tenzij het issue een wijziging vereist.

## Voor implementatie

1. Lees issue, comments, acceptatiecriteria en dependencies.
2. Lokaliseer de centrale eigenaar van de geraakte regel/data.
3. Controleer of het issue een materiële keuze openlaat.
4. Voer bij relevante risico's eerst de impactanalyse uit.
5. Bepaal het laagste passende testprofiel.
6. Controleer expliciet of de wijziging een tweede source-of-truth zou introduceren.

## Implementatie

- Scheid presentatie, applicatielogica, domeinlogica en infrastructuur waar passend.
- Dupliceer geen bestaande businesslogica wanneer veilige hergebruikpaden bestaan.
- Afgeleide state wordt berekend uit een canonieke bron of heeft expliciete provenance/invalidation.
- Scenario-/what-if-state blijft geïsoleerd van current/masterdata.
- Voeg geen externe afhankelijkheid, cloudservice, telemetrie of accountkoppeling toe zonder expliciete product- of architectuurbeslissing.
- Vermijd N+1-query/writepatronen in bulkflows; gebruik set-based reads en batched/transactionele writes waar passend.
- Houd externe/providerdata achter een duidelijke adapter/poort en leg versie-/fallbacksemantiek vast.

## Bugfix

1. Reproduceer werkelijk versus verwacht gedrag.
2. Breng geraakte code, data, tests en afhankelijke flows in kaart.
3. Bepaal de root cause; repareer niet alleen het zichtbare symptoom.
4. Meld diagnose + voorgestelde oplossing compact vóór implementatie.
5. Voeg waar praktisch een regressietest toe.
6. Herstel de kleinste centrale eigenaar van de regel.
7. Test de directe fout en alleen relevante regressiegebieden.
8. Leg bewust niet-uitgevoerde zware controles expliciet vast.

## Data en schema

Wanneer persistentie geraakt wordt:
- volg `DATABASE_SAFETY.md`;
- onderscheid canonieke gebruikers-/masterdata van derived/cache/reference stores;
- maak migratie-, rollback/recovery- en backward-compatibiliteitsgedrag expliciet;
- interpreteer ontbrekende/unknown data niet stil als nul, false of afwezig zonder productspecificatie.

## Externe referentiedata en seeds

Wanneer de app meegeleverde of opgehaalde referentiedata gebruikt:
- gebruik een expliciete versie;
- leg bron/provenance en effective date vast;
- valideer schema en integriteit vóór activatie;
- vervang bestaande geldige data atomair;
- maak update- en fallbackgedrag deterministisch;
- laat build/runtime niet onverwacht internetafhankelijk worden.

## Afronding

- Inspecteer de volledige diff.
- Voer `git diff --check` uit.
- Gebruik het laagste passende testprofiel.
- Werk roadmap/documentatie bij wanneer de wijziging hun bronrol aantoonbaar raakt.
- Controleer dat acceptatiecriteria aantoonbaar afgedekt zijn.
- Gebruik branch/PR-discipline uit `ISSUE_CONTRACT.md`.
