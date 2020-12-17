---
layout: post
title:  "Rainy Sunday JavaScript learning notes"
date: 2017-10-15
---

Earlier this month, I went [back to the beginning]({{ '/2017/10/back-to-the-beginning/' | url }}) in my stagnant stab at learning JavaScript. Today I completed these two excellent guides under MDN web docs, JavaScript first steps:

* [What is JavaScript?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript)
* [A first splash into JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/A_first_splash)

---

## APIs! A shitload of functionality on top of core JS ✌️
* These are the building blocks of code for me to use.
* The DOM API helps me manipulate HTML and CSS.
* Other APIs built into the browser: Geolocation, Canvas, WebGL, Audio and Video.
* I can also implement all kinds of third party APIs to do anything and everything.

## Words and concepts 🎓
* Each browser window is a separate **execution environment**.
* The **running order** of JS is generally from top to bottom.
* JavaScript is an **interpreted** language.
* This is different from **compiled** languages like C/C++.
*  **Client-side** code is downloaded, run on my laptop and displayed in a browser.
*  This is different from **server-side** that is first run on a server, before the result is downloaded and displayed in a browser.
*  JavaScript can be both — Node.js is an example server-side.

> JavaScript only needs one friend in the world of HTML — the `<script>` element. 💕

Ah, right. We frown on inline JavaScript handlers inside markup, for the same reasons as inline CSS is not the way to go. Nope, don’t do that. Use pure JavaScript constructs!

---

## Number guessing game 👾

This was [a pretty neat tutorial](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/A_first_splash) that took me step by step through building a game to guess a number between 1 and 100. Max 10 guesses, with hints if your number is too high or too low.

* Turning a general brief into **actionable tasks** is a good idea. ✏️
* **Variables** store my data. 👜
* **Functions** are reusable blocks of code. 📦
* **Operators** let me do math or concatenation (joining strings together). 🔨
    * shortcut operators (augmented assignment operators)
    * comparison operators
* **Conditions** in code blocks can run code selectively. ⚠️
* **Events** are actions that happen in the browser. 📅
* **Event listeners** are constructs that listen for these events.
* **Event handlers** are the blocks of code run as a response.

```js
guessSubmit.addEventListener('click', checkGuess);
```

This is a method that we’ve given two arguments:
* The event we’re listening for — user clicking the `guessSubmit` input.
* Code to run when the event occurs — the function we named `checkGuess()`.

---

## Loops ♻️

Repeat a part of code over and over — until a specific condition is met. (I recognise this concept from my WordPress days, and the different types of loops you could have for posts.)

```js
  for (var i = 1 ; i < 21 ; i++) { console.log(i) }
```

This is a `for` loop with three arguments:

| **A starting value** | `i` is 1 |
| **An exit condition** | when `i` no longer is less than 21 |
| **An incrementor** | keep adding 1 to `i` |


Oh yeah and `i` is a convention, but this name could be anything.

---

## Built-in browser objects

> In JavaScript, everything is an object. An object is a collection of related functionality stored in a single grouping.

I can create my own! But for now we’re learning about the ones that already exist in the browser.

```js
guessField.focus();
```

`guessField` is an `<input>`, so it has access to the `focus()` method and we can use it to focus the user’s text input.

```js
guesses.style.backgroundColor = 'yellow';
guesses.style.padding = '10px';
```

* Elements have a style property that contains an object.
* This object contains inline styles applied to that element.

---

## What I’ve been confused about before 🙃

One of the things that has derailed me when looking at intro JS examples before, is that there are so many words that are readable — **but wtf are they actually in the script!?**

```js
  guessSubmit.disabled = true;
```
*will disable the input like so*
```html
<input value="" class="guessSubmit" disabled="">
```

 When you start learning, it’s impossible to understand what is what. When is something a name the coder has come up with? And when are you referencing something that already exists?! Who knows. Another example from this guide:

```js
  resetButton = document.createElement('button');
  resetButton.textContent = 'Start new game';
  document.body.appendChild(resetButton);
```

These words are readable. 👆 I can understand what happens: create a new button, put text on it, and say where to place it. But still… what is what? Where do the words come from?


## What I understand better now 🤓

* There is a really, really, really long list of web APIs.
* Each of those objects provides access to really long lists of properties and methods.

This is a lot of stuff. All the things. I think I’ve tried to wrap my head around too much too early before. Just getting confused by trying to make sense of words in the code that it would have been okay to hold off on grasping. Maybe… I’ve been a bit too worried about not getting it right.

Examples of words I’ve seen many times before, but first now managed to put into any kind of proper relation to each other.

| Object | Properties | Methods |
| --- | --- | --- |
| [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document) |  | `createElement()` `querySelector()` `getElementById()` |
| [HTMLInputElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement) | disabled, autofocus, required | `focus()` `blur()` `select()` `click()` |
| [Window]() | screenX , screenY | `alert()` `prompt()` |
| [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node) | textContent | `appendChild()` |


Hey `textContent`👋! For some unfathomable reason, I have previously read this as “textContext” which has really *not* been helpful in understanding what it does.

---

Okay, this is it for today. But hm… yay… stuff is actually coming together in my head. ✌️
