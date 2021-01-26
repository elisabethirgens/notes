---
layout: post
title:  "Go back to the beginning"
date: 2017-10-07
---

When you are stuck, it can be a good idea to go start over. I did that today. 🌱

[MDN web docs](https://developer.mozilla.org) has the learning module [JavaScript first steps](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps) that I’ve been procrastinating on doing. But now I stepped even further back and did the [basic JavaScript intro](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics) under “Getting started with the Web”. It was great, I needed a soft start and the win of feeling smart because they explain so many things I already understand. But I did force myself to type every line of example code, play around with it, read other pages too, and to write up these notes&nbsp;👇 in my own words to be sure I actually understood.

---

## Hello 🌎

``` js
var myHeading = document.querySelector('h1');
myHeading.textContent = 'Hello world!';
```

Yay, that was fun. So what’s happening here?

* Use a function called `querySelector()` to grab the element.
* Store that in a variable and name it `myHeading`.
* Set a value to the variable’s `textContent` property.
* These two features are both part of the DOM API.

✅ Played around in the console. *(And let’s be honest, I haven’t really done that much before now. I guess it’s easier for a website than [a paper book]({{ '/2017/07/javascript/' | url }}) to encourage diving in there.)*

---

## Variables to store values 👜

```js
var myBeverage = 'coffee';
myBeverage = 'ginger daiquiri';
```

* Declare a variable, name it and give it a value.
* Change the value of the variable in the next statement.
* Variables can have different datatypes; string, number, boolean, array, object.

(I enjoyed a very nice ☕️ with 🥐, and then a 🍸, while going through this tutorial.)

---

## Operators to produce a result 🔨

| | |
| --- | --- |
| `+` | Add numbers or concatenate strings. |
| `-` `*` `/` | Subtract, multiply, divide to do basic math with numbers. |
| `=` | Assigns a value to a variable. |
| `===`| Are these two things equal? Yay or nay. |
| `!` | A logical NOT operator that returns the opposite boolean. |
| `!=` | An inequality operator that can test if two values are *not* equal. |

---

## Conditionals to run alternative code ⚠️

This is a code structure that will test if an expression is true. Or else… it will run the alternative. I’m actually quite used to reading and understanding conditionals from code bases in various languages, also way back when working with WordPress templates in php.

---

## Functions to wrap up functionality for reuse 📦

* Some are built into the browser, like `document.querySelector()` and `alert()`.
* I can also declare my own functions \o/.
* They can take arguments in parentheses to do their job.
* A variable defined within a function is local (not global).
* Functions can be either named or anonymous (without a name).

---

## Events to notify what’s happening 📅

```js
document.querySelector('html').onclick = function() {};
```
The click event listens for a mouse click in the browser. Other examples:

* **Resource Events**  —  cached, error, abort, load
* **Focus Events** — focus, blur
* **Form Events** — reset, submit
* **View Events** — resize, scroll
* **Mouse Events** — mouseover, click, select

---

[This](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics) was a very nice hands-on dive-right-in introduction and oveview.

> We have barely scratched the surface of JavaScript. If you have enjoyed playing, and wish to advance even further, head to our JavaScript learning topic.

Yes! Let’s do that!!!!1 ✌️✌️✌️
