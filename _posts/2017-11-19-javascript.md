---
layout: post
title:  "Troubleshoot my JavaScript"
date:   2017-11-19 18:00:00 +0200
categories: learning
---

All right, I’m going through the lovely [JavaScript first steps @ MDN web docs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps) and next up is the guide on [“What went wrong? Troubleshooting JavaScript”](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_went_wrong). Let’s write up some notes:

---

## Check the syntax 🤦‍♀️
**Syntax errors** are spelling mistakes, mixed up lowercase / uppercase, or missing characters causing the script to fail. I will mostly get helpful error messages pointing to the code line.

* `TypeError: "x" is not a function` — typically a misspelled function
* `TypeError: "x" is (not) "y"` — hello undefined and null
* `SyntaxError: missing ; before statement` — check your semicolons
* `SyntaxError: missing ) after argument list` — close your parenthesis
* …and so on. There’s a very long [error reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors)!

---

## Work through the logic 🙃
**Logic errors** are more difficult. I might not get any error messages, but there’s still something wrong so the script doesn’t work as intended. Add patience and go though the logic in the script.

---
 
## Output text to the console 🔎
This is a function I can use for debugging. The parameter can be a message:
```
console.log('testing one two three');
```
…or an object! For example would `console.log(randomNumber);` let me cheat at the numbers guessing game in the tutorial. I can also use these other methods for more categories;


💁 `console.info()` &emsp; ⚠️ `console.warn()` &emsp; 💔 `console.error()`

---

Cool! Feels like I should have learnt this before, but now is better than never.
