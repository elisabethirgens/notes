---
layout: post
title: "Start That React Course Already"
date: 2019-12-22
---

The very first time I heard about React, was in 2014 when [Arne Martin @ Web Rebels](https://2014.webrebels.org/speakers.html#arne_martin) had a talk about building UI components with this new thing called React. The sketchnotes I made quotes him that: “React is a thing in the world. It’s pretty nice and you should try it.”

Since then I’ve worked in React applications for a couple of years, but only at the very front of the frontend surface. I know how to dig around for markup, styles and content — but I’ve not really dealt much with the actual React part of the UIs. Or ever built a React app from scratch myself.

Current plan is this course: [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

---

## Getting started with section 1

This was a breeze, but it’s nice to warm up. The main point of React is to:

- write JS that runs in the browser, not on a server
- build custom HTML elements
- create components, components, components

When I add React as script tags, I need: [React](https://reactjs.org/docs/react-api.html) + [ReactDOM](https://reactjs.org/docs/react-dom.html)

### JSX

> is a syntax extension to JavaScript. We recommend using it with React to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript. –&nbsp;[reactjs.org/docs: Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)

### Why React

> UI state becomes difficult to handle with vanilla JS

### One or more React render calls?

| Single page application                   | Multi page applications              |
| ----------------------------------------- | ------------------------------------ |
| content is (re)rendered in the client     | content is rendered on the server    |
| typically only 1 `ReactDOM.render()` call | `ReactDOM.render()` calls per widget |

---

## Refresh some JS in section 2

- `var` is the classic variable statement
- `let` is a newer alternative for variable values
- `const` is a newer alternative for **constant** values

Why was the name `let` chosen?! [Stackoverflow explains](https://stackoverflow.com/questions/37916940/why-was-the-name-let-chosen-for-block-scoped-variable-declarations-in-javascri) the maths origin.

### Classic arrow functions

```javascript
function callMe(name) {
  console.log(name);
}
```

Can also be written as

```javascript
const callMe = function (name) {
  console.log(name);
};
```

And apparently this is new and fancy. Yeah… I honestly don’t see how this syntax is so much more amazing. 🤷🏻‍♀️ But fewer issues with scoping `this` sounds like a useful side effect.

```javascript
const callMe = (name) => {
  console.log(name);
};
```

### Exports & Imports

I will want to split code across multiple files, but might still need to access functionality from a different module. This is where exporting and importing helps.

- **default** 👉 `export default ...;`
- **named** 👉 `export const someData = ...;`

- import **default exports** with:<br>
  `import whatNameYouWantToUseHere from './file.js';`
- Or import **names exports** by exact name with braces<br>
  `import { someData } from './file.js';`

> A file can only contain one default and an unlimited amount of named exports. You can also mix the one default with any amount of named exports in one and the same file.

### Classes, Properties and Methods

`class` is a way to define blueprints for objects

> Properties are like “variables attached to classes/objects”

ES7: `myProperty = 'value'`

> Methods are like “functions attached to classes/objects”

ES7: `myMethod = () => {...}`

### Spread & Rest Operators

Tada ✨ `...` ✨

- Spread when used to split up array elements or object properties
- Reset when used to merge a list of function arguments into an array

### Destructuring

> The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.<br>
> –MDN:&nbsp;[destructuring assignment ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### Array functions

Particularly important in this course are 👇

- [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) creates a new array with the results of a function on every element in the calling array
- [`find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) returns the first element in the provided array that satisfies a testing function
- [`findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) returns the index of the first element in the array that satisfies the test
- [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) creates a new array with all elements passing the test implemented by the function
- [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) executes a reducer function on each element, resulting in a single output value
- [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) is used to merge two or more arrays, without changing the existing arrays
- [`slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) returns a shallow copy of a portion of an array into a new array object
- [`splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) changes contents of an array by removing, replacing and/or adding new elements

---

I really wish the instructor could go though this without constantly referring to it as “easy” and “of course” and “simply” and “obvious”. It’s making me want to ditch this course and find another. 😒
