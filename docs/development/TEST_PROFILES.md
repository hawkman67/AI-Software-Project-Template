# Testprofielen

Kies het laagste profiel dat alle geraakte risico's afdekt. Bij twijfel: Development.

| Profiel | Wanneer | Minimale controle |
| --- | --- | --- |
| Docs | Alleen documentatie, templates of workflowbestanden | diffcheck en relevante syntaxcontrole |
| Targeted | Kleine lokale wijziging zonder gedeelde logica of data-impact | format/analyze plus gerichte tests |
| Development | Normale productcode, services of gedeelde logica | volledige analyse en normale tests |
| Database | Schema, SQL, persistentie of migratie | Development plus migratie- en integriteitstests |
| Release | Officiële release of releasekritieke wijziging | Database plus releasecontroles |

Targeted is alleen passend wanneer aantoonbaar is dat de impact lokaal blijft.

Projectspecifieke commando's en scripts moeten in dit document of aanvullende projectdocumentatie worden ingevuld zodra de technische stack is gekozen.
