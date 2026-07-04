---
layout: post
title: "Bli venn med Dependabot"
date: 2026-07-04
---

Dependabot kan være en nyttig medhjelper i arbeidet med sikkerhet. Men hva _er_ egentlig denne bot-en? Hvordan forholde seg til pull requestene den åpner i repoene? GitHub sin dokumentasjon: [Keeping your supply chain secure with Dependabot](https://docs.github.com/en/code-security/dependabot) er grundig og god, men intenst omfattende og laaang. Kanskje du heller vil lese denne bloggposten?!

## Robotgressklipper eller motorsag?

Jeg har ikke hage, men jeg antar at robotgressklipper er mest nyttig på gressplen. Hvis det jeg ser på strengt tatt ligner mer på villniss, så nytter det ikke leve i håpet om at en robotgressklipper kan fikse vedlikehold for meg. Da trenger jeg motorsag for å hugge vekk kratt — og jeg må lage en plan for jobben det er å preppe en plen. En der det seinere kanskje kan gå an å klippe gress. Eller noe sånt. 😅

## Tre ulike funksjoner

Dependabot gjør flere ting. Det er greit å ha et forhold til at dette er 3 separate funksjoner:

- **Alerts** er varsler om at en sårbarhet er funnet i en _dependency_ som brukes i repoet
- **Security updates** er pull requests med en oppdatering for å håndtere en spesifikk sårbarhet
- **Dependency updates** er generelle oppdateringer (ikke relatert til noen kjent sårbarhet)

Jeg er mest opptatt av den første; varslingen som skjer med **alerts**, og tenker på dette som den viktigste rollen til Dependabot. Sikkerhets&shy;miljøene ute i verden oppdager stadig nye sårbarheter, og Dependabot varsler oss i et repo når en ny sårbarhet er identifisert i en avhengighet vi bruker. De to andre funksjonene er oppdateringer i form av pull requests og de kan lage ganske mye støy. Det er derfor fort gjort å legge mest merke til PRene — og tenke at det er disse oppdateringene som _er_ Dependabot. Men automatisk forslag om å bumpe et versjonsnummer er ikke alltid nyttig (mer om det nedenfor!) og jeg kan fint velge helt andre måter å jobbe aktivt med å holde avhengigheter oppdatert. Sagt på en annen måte:

**Updates** fra Dependabot kan jeg eventuelt ignorere. **Dependabot alerts** er det IKKE greit å ignorere. Som utvikler er det mitt ansvar å forholde meg til åpne varsler om sårbarheter i repoene teamet eier.

## Hull i gjerdet! 🚨

Tilbake til hagen; Dependabot er først og fremst en alarm. Den kan ikke gi beskjed om innbrudd, men den varsler om potensielle sikkerhetshull. Sårbarheter som kan ha høy eller lav risiko — eller som kan være kritiske. Noen varsler kan være irrelevant, noe som ikke er et reelt sikkerhetshull i vår kontekst. Men det vet jeg ikke uten at alerten undersøkes. Etterhvert som kjente sårbarheter har vært kjent lenge, så kan det bidra til å øke risikoen for at en inntrenger kan finne akkurat dét hullet i gjerdet.

## Kan jeg stole på PRene fra Dependabot?

Det korte svaret: nei. Det lengre svaret er… _it depends!_ 😎 Jeg tenker på Dependabot som en naiv liten bot med ivrige forslag og svært begrenset innsikt i konsekvenser. Det er viktig at et menneske gjør en vurdering: Hva er risikoen dersom oppgraderingen feiler? Har appen et bygg og en testdekning jeg stoler på? Er forslaget til oppdatering en liten patch eller er det to-tre jafs major? Dependabot bumper nemlig versjons&shy;nummer helt ukritisk, men den vil som regel klare å vise en **compatibility score**. Den viser også info om hva pakken gjør og hva oppdateringen består av, som jeg gjerne kikker over. Det er mye som påvirker hvor grundig eller ikke-i-det-hele-tatt jeg velger å teste før jeg merger. Eller lukker.

## Vil Dependabot fortelle meg at pakker er utdatert?

Nei, egentlig ikke.

Det er, for eksempel i tilfellet Node, heller `npm outdated` som forteller meg hvilke pakker som er utdatert. Dependabot gjør ikke det, med mindre jeg gjør en iherdig innsats med kontinuerlig vedlikehold og konfigurasjon i en `.github/dependabot.yml`. Dependabot kan _bidra_ med vedlikehold, men det er begrenset hvor smart den er og om strategien den legger opp til er nyttig i mitt repo. Hvis appen er i dårlig stand, så kan forslag til oppdateringer fra Dependabot være ganske villedende. PRene fra Dependabot kan være veldig begrenset, og de kan til og med være pauset helt dersom ingen har interagert med dem i det repoet på en stund. Alerts blir ikke pauset, security updates blir ikke pauset. Men de generelle oppdateringene slutter å komme dersom ingen forholder seg til dem. Det er her jeg ser for meg en robotgressklipper som enten stopper helt opp, eller som surrer rundt i en pitteliten krok av hagen der det er flekk med plen. Den trenger hjelp! Og en faktisk gressplen!

## La oss studere konfigurasjon 🔎

**Alerts** er skrudd på for alle repo i Amedia sin organisasjon på GitHub. Team SRE & Utviklerplattform har hos oss laget en tjeneste som sender Slack-melding til riktig team når Dependabot åpner et nytt varsel. (Dersom du jobber her, så får du varselet via den sikre kanalen `private-channel` fra `whoami.yaml` i repoet. Varslene samles også på dashboard Quadrophenia og i systemkatalog Budibase.)

**Security updates** er også konfigurert på org-nivå. Jeg kan ikke skru av i et repo at Dependabot åpner denne type pull requests, og de kan være et okay hint om en oppdatering som bør skje snarere heller enn seinere. Men en utvikler må vurdere om forslaget fra bot-en er en oppdatering med lav risiko — eller om det er en oppdatering som må sjekkes grundigere før PRen kan merges og prodsettes.

**Dependency updates** er generelle oppdateringer som kan konfigureres i repoet. Ved å lage en `dependabot.yml` kan jeg skru av PRene dersom de kun støyer, eller justere dem sånn at de blir nyttige i ulike repo. Jeg kan altså ikke skru av alerts eller security updates, men disse generelle PRene som åpnes for å bumpe det ene etter det andre, det er det teamet selv som kan og må konfigurere.

## Er PRene fra Dependabot nyttige?

Sikkerhetsoppdateringene kan være nyttige. Spesielt når det blir oppdaget en `critical` vulnerability i den ene lille pakken som alle Node-appene bruker, og Dependabot automatisk genererer ny lockfil i samtlige av de 20+ repo-ene i en fei. Det kan spare et team for noen kjedelige manuelle steg.

De generelle oppdateringene syns jeg ofte lager veldig mye støy, uten at de gir meg noen god indikasjon på tilstand av vedlikehold i et repo. Dependabot åpner maks 5 stk pull requests av gangen, med mindre repoet har definert et annet tall enn default 5 med `open-pull-requests-limit` inne i en `.github/dependabot.yml`. Hvis jeg merger 5 stk, så kan Dependabot finne på å åpne nye 5 stk straks etterpå. Derfor har jeg ofte foretrukket å lage mine egne pull requests som samler sammen mange flere oppdateringer. Men det kommer helt an på hvor oppdatert eller ei avhengighetene i repoet er.

Dependabot tar kun én pakke av gangen, og det kan bli skikkelig klønete hvis det er pakker som henger sammen. F.eks. virker det smart at storybook-relaterte pakker oppdateres i samme PR. Men det klarer ikke Dependabot ut av boksen. Det går an å konfigurere branch for Dependabot, sånn at man kan samlet merge inn på hovedbranch og prodsette. Det virker nyttig! Men krever innsats. Generelt stoler jeg mer på Dependabot om oppdatering av avhengigheter generelt i repoet ikke henger for langt etter. Men dersom `npm outdated` tyder på et stort etterslep over hele fjøla, så er ikke min erfaring at Dependabot sin fremgangsmåte med én av gangen er effektiv. Da er det bedre at jeg drar frem en motorsag og gyver løs på villnisset med min egen strategi for oppdateringer.

---

Repost of a text I originally wrote in 2024 for our work blog [Jotter](https://amedia.github.io/jotter/2024/bli-venn-med-dependabot/)
