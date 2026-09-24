# Algemene workflow

## Bronnen en scope

- GitHub Issues bepalen wat wordt gebouwd.
- De repository bepaalt wat al bestaat.
- Lees `docs/PRODUCT.md` bij productwerk.
- Lees `docs/ARCHITECTURE.md` bij architectuurwerk.
- Houd wijzigingen gericht en behoud bestaand gedrag tenzij het issue een wijziging vereist.

## Implementatie

- Scheid presentatie, applicatielogica, domeinlogica en infrastructuur waar passend.
- Dupliceer geen bestaande businesslogica wanneer veilige hergebruikpaden bestaan.
- Voeg geen externe afhankelijkheid, cloudservice, telemetrie of accountkoppeling toe zonder expliciete product- of architectuurbeslissing.
- Voer bij materiële impact eerst de impactanalyse uit zoals beschreven in `AGENTS.md`.

## Bugfix

1. Reproduceer werkelijk versus verwacht gedrag.
2. Breng geraakte code, tests en afhankelijke flows in kaart.
3. Voeg waar praktisch eerst een regressietest toe.
4. Herstel de kleinste centrale eigenaar van de regel.
5. Test directe fout en relevante regressiegebieden.
6. Leg niet-uitgevoerde controles expliciet vast.

## Afronding

- Inspecteer de volledige diff.
- Voer `git diff --check` uit.
- Gebruik het passende testprofiel.
- Werk alleen expliciet aangewezen documentatie bij.
- Maak geen commit of push zonder expliciete opdracht.
