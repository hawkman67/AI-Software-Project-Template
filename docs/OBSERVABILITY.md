# Observability-baseline

Logs zijn technische diagnose; geen analytics, businessaudit of vervanging voor user-facing status/foutmeldingen.

## Principes

- Gebruik één applicatiebrede loggingabstractie per runtime.
- Log op operationele grenzen, niet per record/interval in hotpaths.
- Gebruik een operation/correlation ID voor één gebruikersactie of achtergrondoperatie.
- Log dezelfde exception niet in iedere laag opnieuw.
- Loggingfouten mogen de hoofdflow niet breken.
- Sinks hebben begrensde retentie.

## Eventcontract

Een event bevat waar passend:
- UTC timestamp;
- level;
- component;
- stabiele eventnaam;
- veilige message;
- operation/correlation ID;
- elapsed tijd;
- compacte structured fields;
- exceptiontype bij fout.

## Privacy

Log nooit:
- credentials, tokens of authorization headers;
- complete providerpayloads;
- ruwe gevoelige gebruikersdata;
- private keys/secrets;
- onnodige lokale paden;
- bulkdatasets of volledige tijdreeksen.

Gebruik hashing/redaction wanneer een stabiele identifier diagnostisch nodig is.

## Levels

- trace: tijdelijke detaildiagnose;
- debug: fase/cache/flowdiagnose;
- info: betekenisvolle lifecycle- en operationele resultaten;
- warning: recoverable afwijking/fallback/incomplete data;
- error: gevraagde actie kon niet correct worden afgerond.

## Performance

Hotpaths loggen alleen samenvattingen zoals ranges, counts, duur, completeness en resultaat/fallback.
Geen info-event per record of database-row.

## Opslag en support

Vul projectspecifiek in:
- loglocatie;
- rotatie;
- retentie;
- support/exportbeleid;
- configuratie van logniveau.
