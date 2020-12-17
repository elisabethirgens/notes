---
layout: post
title:  "Finish The JS First Steps Modules on MDN"
date: 2018-08-14
---

After some months of focusing on Python and what not, let’s get back to JavaScript. It’s been a while since I [was doing these modules]({{ '/2017/11/javascript/' | url }}) from MDN web docs, but will pick up where I left off.

---

## Variables to store values 👜

Module: [Storing the information you need — Variables](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)

```javascript
// declare a variable
var bestColor;

// initialize the variable
bestColor = 'darkcyan';

// declare and initialize at the same time
var prettyColor = 'cadetblue';
```

[var hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting
) is the behaviour that means I can declare variables up front, because JavaScript handles variable before the script is run.

> it is recommended to always declare variables at the top of their scope (the top of global code and the top of function code) so it's clear which variables are function scoped (local) and which are resolved on the scope chain.

### Naming

* Safe variable naming convention: lowerCamelCase
* Numbers and underscore but not first
* Case sensitive
* …and remember no JS reserved words!

### Data types

* Numbers, strings, booleans, arrays, and objects
* JS is a **dynamically typed language** because I don’t need to specify a data type for variables
* `typeof` is an operator I can use to return the data type of the variable I pass into it

---

## Math with numbers and operators 🔢

Module: [Basic math in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Math)

I noticed at the variables section that I should stop crawling, and **try to speed up!** Same here, after Learn Python The Hard Way, I know what integers, floats and number systems are now.

Console practice session gave me a syntax error when decaring and initializing a variable with a float, so I need to remember that even though the decimal separator in Norwegian is a comma `3,14` that will be interpreted as an array missing square brackets. 🤪

(Unlike Python) JavaScript only has one numeric type:

```javascript
var thisNumber = 666;
typeof thisNumber;
// returns "number"

var thatNumber = 3.14;
typeof thatNumber;
// returns "number"
```

This section also covers basic arithmetic operators and operator precedence, how to use parantheses to calculate parts of an expression first and so on. Yup, all good.

### Increment and decrement operators

```javascript
var start = 50;
start++;
// returns 50
start;
// returns 51
```

If I use the incrementer after the variable like that, the browser will first return the current value — then increment. If I use the operator first like `++myVariable;` or `--myVariable;` the browser will return the incremented/decremented value.

Ha, I see the internet is full of people asking why Python doesn’t have a `++` operator. Well, I learnt Python style increment by `+=` first, so I think that makes way more sense.

## 🤯

This is where I reach the part introducing JS assigmenent operators that… work exactly the same way?! Right.

### Comparison operators

Looks all familiar, also noting that they here recommend using strict `===` and `!==` to test both value and datatype.

---

## Strings 🎻

Module: [Handling text — strings in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Strings)

Not much new in this section, but console exercises are good practice for me. These MDN tutorials get you to type a lot in the console. Also stuff that doesn’t work, so when you do get errors later, you’ve seen the syntax errors before.

* Escape notation
* Concatenate is joining together
* String literal

When I want to convert a string to a number, I can pass the string into the [`number` object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) and it will return a string if it can. `Number('666')`

If I need the opposite: [`toString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString). This is a method to the number object. I don’t pass the number into it like the previous example because…?! Not sure, but it will probably become more clear soon.

---

## Built-in methods to do stuff to strings 🎶

Module: [Useful string methods](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Useful_string_methods)

They keep saying that everything in JavaScript is an object. 🤔

```javascript
var chocolateCake = 'That variable will become a string object instance';
```

* How long is that string? Use the `length` attribute.
* Retrieve a specific character? Use square bracket notation `chocolateCake[5]`
* Need to grab a substring? Use this method `chocolateCake.indexOf('become')`
* Want to extract it? Use the `slice()` method with character positions.
* Change words? Sure! Use the `replace()` method 👇

```javascript
chocolateCake = chocolateCake.replace('string object instance', 'cake');
```

✅ Finished the active learning examples. Had to peak just a tiny bit for hints in the solutions for the first two, but flew through the last one. Yay!

---

## Make lists of multiple data items 🌈

Module: [Arrays](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Arrays)

```javascript
var beer = ['stout', 'brown ale', ['ipa', 'neipa', 'black ipa']];
// modify an item with bracket notation
beer[1] = 'porter';
// beer now returns [ "stout", "porter", (3) […] ]
beer[2][0];
// returns "ipa" within the multidimentional array
```

### Find length of an array

```javascript
beer[2].length;
// returns the number of IPAs as 3
beer[2][beer.length-1];
// returns the last item of the IPAs: "black ipa"
```

…and more commonly, [`length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length) is used to tell a loop to keep going through all items of an array.

### Split data in a string to an array

```javascript
var ourRawData = 'Oslo,Bergen,Trondheim,Stavanger,Tromsø';
var ourAwesomeArray = ourRawData.split(',');
ourAwesomeArray;
// returns [ "Oslo", "Bergen", "Trondheim", "Stavanger", "Tromsø" ]
var lastCity = ourAwesomeArray[ourAwesomeArray.length-1];
lastCity; // returns "Tromsø"
```

### Join items in an array to a string

```javascript
var myNewString = ourAwesomeArray.join('/');
myNewString; //returns "Oslo/Bergen/Trondheim/Stavanger/Tromsø"
```

### Add or remove array items

* `push()` and `pop()` at the end of the array
* `unshift()` and `shift()` items at the beginning

> The new length of the array is returned when the method call completes

…which means if I need it, I can store it in a variable. Same with an item removed from the array, I can use a variable to save it. Here I will remove the first city from the list:

```javascript
var currentCity = ourAwesomeArray.shift();
// returns [ "Bergen", "Trondheim", "Stavanger", "Tromsø" ]
currentCity; // returns "Oslo"
```
---

## 🎉
