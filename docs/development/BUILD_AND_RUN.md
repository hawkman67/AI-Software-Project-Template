# Build, run en release

Vul dit document in zodra de technische stack gekozen is.
Houd build-/runcommando's hier centraal zodat issues en chats ze niet telkens opnieuw hoeven uit te vinden.

## Vereisten

- SDK/runtime:
- Toolchain:
- OS/platform:
- Extra native dependencies:

## Dependencies ophalen

```
...
```

## Development run

```
...
```

## Gerichte tests

```
...
```

## Volledige developmentvalidatie

```
...
```

## Releasebuild

```
...
```

## Buildvarianten / environments

- Development:
- Test:
- Production:

## Externe providers

Normale build/test mag niet onverwacht echte bulkrequests of muterende calls naar productieproviders uitvoeren.
Gebruik deterministic fixtures/fakes/seeds tenzij een expliciete maintenance- of integratietest anders vereist.

## Seeds/reference data

- Locatie:
- Versie/manifest:
- Validatie:
- Updateprocedure:
- Offlinegedrag:

## Releasechecklist

- relevante tests groen;
- packaging/build succesvol;
- migrations/seeds gecontroleerd;
- versie/buildnummer bijgewerkt indien van toepassing;
- release notes / bekende beperkingen;
- rollback/recoverypad bekend.
