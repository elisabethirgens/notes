---
layout: post
title: "Numeronyms and Numerical Contractions"
date: 2026-07-02
---

A rite of passage for any new team, is generating a 100+ comment long Slack thread discussing the fundamental cultural decision in the name for a new repository. And so it was I ended up looking up what this 👇 type of naming “tradition” is technically called:

**Numeronyms** are a type of abbreviation using numerals.

Also called **alphanumeric abbreviation**. Which I find easier to pronounce. But since this is a written blog post, I’ll stick with the word used as the main entry for the [Wikipedia article](https://en.wikipedia.org/wiki/Numeronym). That is also where I&nbsp;learnt there are different types of numeronyms. The type we are looking at now, is the one where for example a long word `internationalization` is abbreviated by counting and replacing the 18&nbsp;characters between the **i** and the **n** 👉 `i------------------n` to end up with the shorter term **i18n**.

## Numerical contractions

- **i18n** – internationalization has 18 characters in the middle of the word
- **a11y** – accessibility has 11 characters between **a** and **y**
- **p13n** – personalization has 13 characters between **p** and **n**
- **g11n** – globalization has 11 characters between **g** and **n**
- **K8s** – Kubernetes has 8 characters between **K** and **s**

## Why use a numeronym?

HTTP is shorter than Hypertext Transfer Protocol. An abbreviation we can all appreciate. But wtf 😏 is the point of abbreviations that obfuscate and even make the thing your are trying to say actually consist of more syllables?! In a code base, `i18n` can save us all from needing to spell internasjonalaisasjon. For other uses, it‘s absolutely a valid argument against using a numeronym if the word function best in the original form. But the thing about plain words is that it can be difficult to know when that word actually represents a name or a more specific term.

A numeronym can transform a word into something that means _more_ than the word means alone.

> The word accessibility has different meanings in different contexts. On the internet, the use of the term a11y helps to identify content related specifically to digital accessibility. <br>— [The A11Y Project](https://www.a11yproject.com/about/#what-does-the-term-a11y-mean)

## Can we make more numeronyms?

Absolutely! Like any abbreviation, you can make your own. My laptop has a sticker **t12t** from an [accessibility meetup](https://t12t.se/en/) in Stockholm. This is from the Swedish word `tillgänglighet` 🇸🇪.

We named our repo **a5e** and this is a numerical contraction for the Norwegian word `annonse` 🇳🇴. Definitely not a word needing abbreviating as such, but we did need to create a term that means something other than the word itself. When someone on the team now refers to **a5e**, other people on the team know we are talking about this specific repository and not about something else.

---

Repost of a text I originally wrote in 2024 for our work blog [Jotter](https://amedia.github.io/jotter/2024/numeronym/)
