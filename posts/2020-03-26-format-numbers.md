---
layout: post
title:  "Format Numbers With Intl.NumberFormat"
date: 2020-03-26
---

I’ve been getting to know [Intl.NumberFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat) intimately lately. It is a pretty neat:

* constructor for objects
* to enable language sensitive number formatting
* and this is JS standard built-in stuff, so I can run it in any empty browser console


## The Intl object

> …is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting.
<br>&nbsp;– MDN web docs on [Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

Nice, I see there’s a similar constructor for date and time formatting: [Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat). But for now, I want to format numbers to get control over [decimal and thousands separators]({{ '/2020/03/decimal-and-thousands-separators/' | url }}).


## Locales

When I take it for a spin in the console, these two work as expected. It returns US style thousand separator comma and decimal point, while the Norwegian locale uses space and decimal comma.

```js
Intl.NumberFormat('en-US').format(123456.789)
// returns "123,456.789"
Intl.NumberFormat('nb-NO').format(123456.789)
// returns "123 456,789"
```


## What about default locale?

But I don’t want to hardcode the locale, I want to leave it to the user’s language preferences.

```js
Intl.NumberFormat().format(123456.789)
// returns the number “in the default locale and with default options”
```

But what is the default locale? Not at all straight forward! 🤯 There are so many different language settings. OS? Browser? Html `lang` attribute? MacOS system preferences has **Language & Region**, where I can define English as my preferred language, but Norway as the region. The advanced options under region can be edited, also per application. But default for Norway regarding numbers, is `Grouping: space` and `Decimal: ,` (comma). This is exactly what I want (as a user) for reading numbers the way I’m used to reading them. But as a debugging developer, it’s a different story. Now I finally understand that:

👉 I have been getting `123,456.789` in the application I’m working on, because I have my OS set to English — and **choosing Norwegian in the browser does not override** that as I expected it would. To complicate things further for developers debugging i18n, it depends on the browser…

## Limit the decimals with toFixed()

The code I’m working on has a method for calculating a percent using two values, and to limit the number of digits after the decimal separator, it uses [toFixed()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed). Taking it this for a spin in an empty console to understand what this does:

```js
((100 / 3) * 100).toFixed(2);
// returns "3333.33"
((100 / 2) * 100).toFixed(2);
// returns "5000.00" with the added zeros
```

This does exactly what I need. Most of the percentages have two digits behind the decimal separator. The added zeros, for the occasional instances of a value with only one digit or none, will make sure all numbers align and are scannable down the table column. 👍

## Options argument for decimal

What happens when I format those percentages with my new best friend [Intl.NumberFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat)…?

```js
Intl.NumberFormat().format(5000.00);
// returns "5,000"    without added zeros :-(
```

But ha! I found out there are [options](https://tc39.es/ecma402/#numberformat-objects)! Sounds promising…

```js
Intl.NumberFormat({ minimumFractionDigits: 2 }).format(5000.00);
// returns "5,000"       option is completely ignored

Intl.NumberFormat('en-US',{ minimumFractionDigits: 2 }).format(5000.00);
// returns "5,000.00"    added zeros iz back :-)
```
Butbutbut I want this result _without_ specifying the locale… Tried some versions with a space before the comma separating the options (SyntaxError!) empty strings with single quotes or double quotes (RangeError!). But yay, if I put an empty array in there, then it works:

```js
Intl.NumberFormat([],{ minimumFractionDigits: 2 }).format(5000.00);
// returns "5,000.00"
```

## 🥳
