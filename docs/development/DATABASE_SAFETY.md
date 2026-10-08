# Databaseveiligheid

Gebruik dit document wanneer het project persistente data gebruikt.

## Canoniek versus afgeleid

Classificeer iedere store/tabel expliciet als één van:
- canonieke gebruikers-/masterdata;
- externe/reference data;
- derived/materialized/cache data;
- scenario/what-if data;
- technische metadata.

Een derived-, cache- of scenariostore mag nooit de enige bron worden van canonieke informatie.

## Migraties

- Elke persistente structuurwijziging krijgt vanaf de eerste ondersteunde baseline een expliciete migratie.
- Alleen het fresh schema aanpassen is onvoldoende wanneer bestaande gebruikersdata ondersteund wordt.
- Bewaar gebruikersdata tenzij een expliciete productbeslissing anders bepaalt.
- Test fresh schema, ieder ondersteund migratiepad, constraints, foreign keys, integriteit en veilig heropenen.
- Oude schema's horen alleen in migratietests of migratiecode thuis, niet als blijvende parallelle runtimewaarheid.
- Een reset/rebuild van canonieke gebruikersdata vereist expliciete eigenaarsbeslissing.
- Leg de actuele migratiebaseline projectspecifiek vast.

## Null, unknown en afwezig

Interpreteer ontbrekende data niet stil als 0, false, leeg of expliciet afwezig.
Maak het verschil tussen onbekend, afwezig en nul expliciet wanneer dat domeinmatig relevant is.

## Derived/cache stores

Een reproduceerbare derived/cache store:
- heeft een eigen schema/lifecycle;
- kan bij corruptie veilig worden gearchiveerd/verwijderd en opnieuw opgebouwd;
- bevat geen canonieke masterdata;
- gebruikt versie/fingerprint/provenance om staleness te detecteren;
- heeft begrensde retentie/GC wanneer groei onnodig is.

## Reference data en seeds

Meegeleverde of externe referentiedata:
- heeft een expliciete datasetversie;
- heeft provenance/effective date;
- wordt vóór activatie op schema en integriteit gecontroleerd;
- wordt atomair vervangen;
- overschrijft een bestaande geldige dataset niet bij mislukte update;
- heeft een expliciet updatepad;
- maakt normale appstart/build niet onverwacht afhankelijk van internet.

## Security en privacy

- Log geen gevoelige gebruikersdata, credentials, tokens of complete providerpayloads.
- Database-/migratiefouten mogen geen secrets of private paden lekken.
- Test herstelpaden zonder productiegegevens te kopiëren naar testfixtures.
