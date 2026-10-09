# GitHub Issue- en PR-contract

## Een uitvoerbaar issue

Een implementatie-issue hoort, waar relevant, expliciet te bevatten:
- probleem en gewenste uitkomst;
- scope;
- expliciete non-goals;
- gekozen product-/domeinsemantiek;
- canonieke source-of-truth/eigenaar;
- data-, schema-, migratie- en compatibiliteitsimpact;
- externe dependencies/providers;
- acceptatiecriteria;
- vereiste test-/validatiegebieden;
- dependencies, blockers en opvolgers.

Als een materiële keuze ontbreekt die niet veilig uit bestaande projectregels volgt, wordt die keuze eerst expliciet gemaakt.

## Start

1. Lees issuebody, comments, acceptatiecriteria en dependencies.
2. Vergelijk scope met actuele implementatie en tests.
3. Volg de conditionele routes uit `DEVELOPMENT_GUIDELINES.md`.
4. Voer impactanalyse uit wanneer `AGENTS.md` dit vereist.
5. Bepaal de canonieke eigenaar van ieder gewijzigd domeinfeit.

## Roadmapdiscipline

`docs/ROADMAP.md` is het levende bouwdraaiboek van het project wanneer het project een roadmap gebruikt.

- Bij ieder roadmaprelevant issue: voeg status, volgorde en relevante dependency/testpoort toe.
- Bij afronding: werk in dezelfde issuebranch/PR roadmapstatus en **Actuele positie** bij.
- Wanneer een issue wordt vervangen, opgesplitst of duplicaat blijkt: houd de historische relatie begrijpelijk en wijs naar de opvolger.
- GitHub Issues/PR's blijven de formele bron van waarheid voor uitvoerstatus.
- Een implementatie-PR die de roadmapstatus aantoonbaar verandert is niet compleet zolang de roadmapupdate ontbreekt.

## Commitdiscipline

- Eén afgerond issue is bij voorkeur één commit.
- Combineer alleen technisch onafscheidelijke issues na expliciete toestemming.
- `Pak issue #N op` is toestemming voor commit, push naar een issuebranch en openen/bijwerken van de PR.
- Branchnaam: bij voorkeur `issue/N-korte-omschrijving`.
- Push nooit rechtstreeks naar `main`.
- Herschrijf geen bestaande historie om regels achteraf toe te passen.

## PR- en reviewdiscipline

Na succesvolle issue-implementatie:

1. inspecteer de volledige diff;
2. voer passende lokale validatie uit;
3. commit alleen de issuescope;
4. push de issuebranch;
5. open tijdens actieve ontwikkeling bij voorkeur een draft-PR;
6. maak de PR pas review-ready nadat lokale validatie is geslaagd;
7. verwijs in de PR naar het issue;
8. iedere nieuwe commit op een review-ready PR maakt eerdere review/validatie mogelijk verouderd;
9. laat de PR open voor aparte ChatGPT-code-review;
10. Codex mag `gptapproved` nooit zelf toevoegen;
11. merge niet automatisch zolang verplichte review/user-test ontbreekt.

Bij reviewbevindingen blijft dezelfde branch/PR in gebruik totdat de bevindingen zijn opgelost.

## Oplevering

- Vink alleen aantoonbaar behaalde acceptatiecriteria af.
- Plaats één korte oplevernotitie met wijziging, validatie en open punten.
- Laat een issue open wanneer user-test of expliciete goedkeuring nog nodig is.
- Gebruik `needs-user-test` wanneer het project dat label hanteert.
- Sluit parent-issues pas wanneer alle relevante children gereed zijn.
- Voeg nooit zelf een gebruikersgoedkeurings- of reviewgoedkeuringslabel toe.

## Proportionele voorbereiding en AI-review

**ChatGPT heeft zelf toegang tot de repository.** Bij het opstellen/reviewen van issues inspecteert de reviewer eerst rechtstreeks de relevante actuele code, callers en bestaande tests. Schuif dit niet standaard af op Codex; vraag alleen gericht technisch onderzoek als de code onvoldoende uitsluitsel geeft.

- **Klein/lokaal** (bijvoorbeeld een label, conditie of enkele regels): kort probleem, exacte locatie indien bekend, gewenste uitkomst en passende gerichte controle volstaan. Geen aparte scout, vooronderzoekissue, ADR, uitgebreid implementatiecontract of verplichte brede testmatrix.
- **Middel** (meerdere direct betrokken callers of gekoppeld gedrag): controleer relevante codepaden en tests vooraf, benoem randgevallen en grenzen, en test geraakte consumers.
- **Hoog risico** (data-/schemamigratie, gedeelde rekenregels, security, publieke contracten, onomkeerbaar effect): expliciete afhankelijkheden, aannames, concrete verwachte uitkomsten, rollback en passende regressiegates vóór implementatie.

De classificatie volgt **feitelijke impact, niet het aantal gewijzigde regels**. Een éénregelige wijziging in financiële kernlogica kan hoog risico zijn; een eenvoudige UI-tekstcorrectie blijft licht. Geen automatische tweede analyse-/reviewronde zonder concrete bevinding. Stop uitsluitend bij een materiële onopgeloste keuze; gewone technische details worden binnen het issue opgelost.

Bij review onderscheidt ChatGPT **issuefout, implementatiefout, ontbrekende test en nieuwe productkeuze**; nieuwe wensen zijn niet achteraf als tekortkoming van Codex te presenteren. Recidiverende bevindingen leiden waar zinvol tot een gerichte regressietest of beknopte templateverbetering, niet tot extra proces voor alle issues.
