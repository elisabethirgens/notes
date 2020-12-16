---
layout: post
title:  "Something (Not Nothing) About JavaScript"
date: 2020-03-16
---

This is post number 100 🍾 since [I started writing these notes]({{ site.baseurl}}/2017/06/hello-world/) to myself almost 3 years ago. To celebrate, I am writing the motivational notes I really need right now. Because I keep telling myself that [“I&nbsp;haven’t learnt JS yet”]({{ site.baseurl }}//2017/07/javascript/) when that is not quite entirely the whole truth anymore. But if I always convince myself that I don’t know _anything_ — I am continuing to sabotage my future progress. So this post is written to convince myself that I actually do know… _something_. 🌱

## I know what JavaScript is

When I come across a language, library, framework or CS topic I know absolutely nothing about, I&nbsp;often find Wikipedia helpful in making the first introductions. For [wikipedia.org/wiki/JavaScript](https://en.wikipedia.org/wiki/JavaScript) there is basically nothing in the introductory paragraphs of 200+ words that is new to me. So by this Wikipedia standard; I know what JavaScript is. (The concept mentioned that I have _least_ familiarity with, is that JS is multi-paradigm. To-do: read more about [programming paradigms](https://en.wikipedia.org/wiki/Programming_paradigm) maybe.)

MDN has a great section on [What is JavaScript?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript) and I know all of this stuff very well. To the point of being able to teach it to newbie web developers. Note to self: this is not _nothing_.

## I know what JavaScript does

Once upon a time, web pages on the internet displayed mostly static text for us to read in a browser. I&nbsp;have worked as a systems developer for over 4 years, I know how complex web applications work. Compared to where I was 5 years ago, this amassed experience is also not _nothing_.

---

## Variables

* `var` was the original old school variable, that I probably don’t need these days
* `let` is the recommended variable declaration in modern web development
* `const` is the one I probably want to use most of the time because it’s constant

## Data types

* number — `123`
* string — `'All kinds of text!'`
* boolean — a statement that resolves to `true` or `false`
* arrays — `['some item', 'another item', 'even more stuff']`
* objects — `{ id: 100, topic: 'learning' }`
* undefined — a variable without an assigned value
* null — points to nothing, often on purpose

## Operators

* Arithmetic: `+` `-` `*` `/` `%`
* Increment `++` and decrement `--`
* Assignment `=` (and I know there are more of ’em)
* Comparison operators like `<` `>` `<=` `>=` and also these are important to fully understand:

| `===` | equal (strict! recommended!) ✅ |
| `!==` | non-equal (strict! recommended!) ❌ |
| `==` | these things are the same, but perhaps not the same datatype 🤷🏻‍ |
| `!=` | nope, not equal 🙅🏻‍ |

Logical operators: AND `&&`, OR `||`, NOT `!`

## Conditionals

* `if...else` is something I’m used to reading in code
* `else if` also
* `condition ? true : false` is a ternary operator that I learnt more recently

## Loops

These all make sense to me: `for` / `while` / `do...while`

## Functions

I know that I can **declare a function** and that I can **call a function**. I know I can give the declaration **parameters** and then when the function is called, I can pass **arguments** to it.

```js
function whateverName() {
  // this comment is wrapped in a declaration for a named function
}
```

```js
const anotherName = () => {
  // this comment is inside an arrow function
}
```

Let’s see… there’s also anonymous functions, return values, local vs global scope.


## Events and more

There’s a whole lot that is still a blur 😜 but I know more than I’ve written up here and what I have written now is… _not nothing_.

---

## I know that fundamentals > frameworks

…and finally, I do know… that when I’m frustrated and struggling, for a variety of reasons, with learning a specific framework — it’s time to buckle down and focus on fundamentals. 😤
