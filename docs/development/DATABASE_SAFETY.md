# Databaseveiligheid

Gebruik dit document alleen wanneer het project een persistente database gebruikt.

- Elke persistente structuurwijziging krijgt vanaf de eerste stabiele baseline een expliciete migratie.
- Alleen het fresh schema aanpassen is onvoldoende wanneer bestaande gebruikersdata ondersteund wordt.
- Bewaar gebruikersdata tenzij een expliciete productbeslissing anders bepaalt.
- Test fresh schema, migratiepad, constraints, integriteit en veilig heropenen.
- Definieer oude schema's alleen in migratietests.
- Log geen gevoelige gebruikersdata.
- Een reset of rebuild van gebruikersdata vereist een expliciete eigenaarsbeslissing.
- Leg de actuele migratiebaseline projectspecifiek vast.
