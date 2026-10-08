# Architectuur

## Status en bron van waarheid

De actuele repository is de technische bron van waarheid voor de bestaande implementatie.
Dit document beschrijft architectuurrichting en blijvende grenzen.

## Technische uitgangspunten

- ...
- Eén canonieke source-of-truth per domeinfeit.
- Afgeleide state is herkenbaar als afgeleid en heeft provenance/invalidation.
- Scenario-/what-if-state is geïsoleerd van current/masterdata.
- Externe integraties zitten achter expliciete adapters/poorten.

## Platforms en deployment

- Doelplatforms:
- Runtime/deploymentmodel:
- Offline/online verwachtingen:
- Packaging/release:

## Logische lagen

### Presentatie

...

### Applicatie

...

### Domein

...

### Data en infrastructuur

...

## Canonieke data-eigenaren

| Domeinfeit | Canonieke eigenaar/store | Afgeleide representaties | Opmerking |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

## Current, scenario en derived state

Beschrijf expliciet:
- wat de actuele werkelijkheid/masterdata is;
- welke data uitsluitend scenario-input is;
- welke resultaten derived/cache/materialized zijn;
- hoe invalidatie/fingerprinting werkt;
- welke state veilig opnieuw opgebouwd kan worden.

## Data en persistentie

- Stores/databases:
- Schema-/migratiebeleid:
- Retentie:
- Backup/recovery:
- Unknown/null-semantiek:

## Externe integraties

Per provider:
- eigenaar/poort;
- authenticatie;
- ondersteunde data/capabilities;
- rate limits;
- timeout/retry/fallback;
- versie/effective-date-semantiek;
- teststrategie.

## Reference data en seeds

- Welke datasets worden meegeleverd/opgehaald?
- Versie/provenance:
- Integriteitscontrole:
- Updatepad:
- Offline/startupgedrag:

## Security en privacy

...

## Synchronisatie en offlinegedrag

...

## Performance en bulkdata

- Verwachte volumes:
- Set-based/batchgrenzen:
- Query-countregels:
- Materialisatiebeleid:

## Testbaarheid

- Unit/integratie/contract/e2e:
- Deterministische fixtures:
- Providerfakes:
- Production-volumeharnassen waar nodig:

## Observeerbaarheid

Zie `docs/OBSERVABILITY.md`.

## Architectuurbesluiten

Zie `docs/decisions/`.
