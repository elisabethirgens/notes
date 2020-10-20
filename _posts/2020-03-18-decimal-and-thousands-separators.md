---
layout: post
title:  "Decimal and Thousands Separators"
date:   2020-03-18 18:00:00 +0200
---

What was correct number formatting again? I’ve read up on this repeatedly the past years to answer the question and get it right in web applications. But as with all interesting problems; “It depends!” _These notes are for future-me, limited to my specific needs for UI internationalization._

## Dot or comma for decimals?

Countries around the world use different decimal separators. [wikipedia.org/wiki/Decimal_separator](https://en.wikipedia.org/wiki/Decimal_separator) has a full list and a world map. Note that the differentiation is countries — not languages.

* Norway, Europe and half the rest of countries use **decimal comma**
* UK, US and the other half of countries use **decimal point**

> The symbol for the decimal marker is either a point or comma on the line. In practice, the decimal point is used in most English-speaking countries and most of Asia, and the comma in most of Latin America and in continental European countries.
<br>—&nbsp;[International System of Units](https://en.wikipedia.org/wiki/International_System_of_Units)

---

## Thousand separator

[Digit grouping](https://en.wikipedia.org/wiki/Decimal_separator#Digit_grouping) is optional, but makes it easier for readers to interpret large numbers quickly. When written as a numeral without thousand separator, it is difficult to tell 3 million from 30 million. Wikipedia is less clear on whether this depends on language or country, the article mentions both.

* Norway, Sweden, and many more use **space**
* Denmark, and many more use **dot**
* UK, US, and many more use **comma**

> Spaces should be used as a thousands separator (1000000) in contrast to commas or periods (1,000,000 or 1.000.000) to reduce confusion resulting from the variation between these forms in different countries. —&nbsp;[International System of Units](https://en.wikipedia.org/wiki/International_System_of_Units)

---

## Internationalization

Can we use `1 234 567,89` in Norway and `1,234,567.89` in the UK and call it a day?

What is the formatting for a Norwegian site in English? What about an application from a Norwegian company offering a service in Norway, in a UI that uses English? And if the users have Norwegian language preferences in their OS or browser? Should you optimize for correct formatting according to language or geography? Or perhaps correct is not the priority, but what users expect?
