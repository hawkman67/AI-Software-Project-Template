# Ontwikkelrouter

Lees altijd `WORKFLOW.md`. Lees daarna alleen de routes die op de wijziging van toepassing zijn.

| Conditie | Verplicht document |
| --- | --- |
| Iedere taak | `WORKFLOW.md` |
| Productcode, tests of bugfix | `TEST_PROFILES.md` |
| Database, persistentie, schema of migratie | `DATABASE_SAFETY.md` indien aanwezig |
| Werk aan of oplevering van GitHub Issue/PR | `ISSUE_CONTRACT.md` |
| Build, packaging, runtime of release | `BUILD_AND_RUN.md` indien ingevuld |
| Logging, diagnose, telemetry of supportability | `../OBSERVABILITY.md` |
| Roadmaprelevante wijziging | `../ROADMAP.md` |
| Domeinspecifiek risicogebied | projectspecifiek safety-/contractdocument indien aanwezig |

Aanvullende bronnen worden alleen gelezen wanneer het issue, de gebruiker of een routerregel dit vereist.

Bij strijdigheid bepaalt het issue de productscope; veiligheids-, data-, source-of-truth- en opleverregels blijven gelden.
