---
layout: post
title: "Topp typografi uten fontfiler"
date: 2026-07-05
---

Jeg begynte kode på et CSS-kurs i 2006, og den gang brukte ingen webfonter. Regelen `@font-face` eksisterte allerede i spesifikasjonen, men det fantes ikke fontfiler som ble distribuert i et filformat eller med lisenser som gjorde det kurant.

Vi brukte `font-family` og definerte en stabel med verdier som representerte fontfiler man kunne regne med at var installert på brukernes maskiner. Dette ble omtalt som «web safe fonts» eller «system fonts» fordi operativ systemet hadde installert dem — brukernes nettlesere trengte ikke laste dem ned. Seinere gikk folk bananas med webfonter, men det er [en annen historie](https://thehistoryoftheweb.com/web-fonts/).

```css
/* Old school web safe fonts fra 20+ år siden */

font-family: `Arial, Helvetica, sans-serif`;
```

Det er fort gjort å tenke at det der 👆<br>
er omtrent det samme som dette 👇

```css
/* Moderne CSS som refererer til nye system UI fonter */

font-family: system-ui;
```

Forskjellen er resultatet i nettleseren. Arial er en sliten gammel klassiker fra 1982. Siden den gang har det vært noen tiår med modernisering av skriftdesign for skjerm og optimalisering av fontfiler. Den moderne `system-ui` er en CSS-verdi som [vi nå kan bruke](https://caniuse.com/?search=system-ui) med god støtte siden 2021. Verdien gjør at nettleseren bruker den samme fonten som operativsystemet selv benytter for å vise tekst i sitt UI. Vi får ulik font på MacOS, Linux og Windows — men alle får _samme_ font som i sitt eget operativsystem. Det er dritfett!

> The fastest fonts available. No downloading, no layout shifts, no flashes — just instant renders.
> — [github.com/system-fonts/modern-font-stacks](https://github.com/system-fonts/modern-font-stacks#system-ui)

#### Toppmoderne fonter fra dagens operativsystemer

- MacOS — San Francisco: https://developer.apple.com/fonts/
- Windows — Segoe UI: https://en.wikipedia.org/wiki/Segoe#Segoe_UI
- Linux — Ubuntu: https://design.ubuntu.com/font
- Linux med Gnome — Cantarell: https://cantarell.gnome.org/
- Andriod — Roboto: https://en.wikipedia.org/wiki/Roboto

Det ligger mye arbeid i å designe og utvikle en font av høy kvalitet med god lesbarhet i brukergrensesnitt, og det kommer stadig ny teknologi også her.

## En variabel fontfil til å regjere over alle vektene

> Variable fonts are an evolution of the OpenType font specification that enables many different variations of a typeface to be incorporated into a single file, rather than having a separate font file for every width, weight, or style.
> — [mdn web docs: variable fonts guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_fonts/Variable_fonts_guide)

Dette er kjempekult! Og er noe som [vi nå kan bruke](https://caniuse.com/variable-fonts) med god støtte siden 2018. Det er visstnok ganske komplisert å designe en skrift og utvikle en fontfil som er så fleksibel, derfor er det enn så lenge et mindretall av fonter som tar i bruk denne snasne teknologien.

> A new font specification that can significantly reduce font file sizes <br>
> — [web.dev/articles/variable-fonts](https://web.dev/articles/variable-fonts)

---

Partial repost of a text I originally wrote in 2025 for our work blog [Jotter](https://amedia.github.io/jotter/2025/prinsipper-for-fagbloggen/)
