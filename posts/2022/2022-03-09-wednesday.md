---
layout: post
title: "JavaScript on a Wednesday"
date: 2022-03-09
---

After [Monday]({{ '/2022/03/monday/' | url }}) and [Tuesday]({{ '/2022/03/tuesday/' | url }}), more study notes from [Vanilla JS Academy ](https://vanillajsacademy.com/) class of October 2021.

## Template literals

```js
// Create strings from multiple lines without concatenating
const string1 = `<h1>Introduced in ES6</h1>
                 <p>These backticks are amazing</p>`;

// Create strings that contain variables
const expression = "Wednesday";
const string2 = `Today is ${expression}`;
```

> You can also use conditionals and functions in template literals. You can’t use if statements as-is, but you can use ternary operators or wrap your if statement in an immediately invoked function expression (IIFE) that returns a string.

```js
// Create strings from a condition
const isItFridayYet = false;
const string3 = `${isItFridayYet ? "<p>YES!! 🥳 </p>" : "<p>Not yet</p>"}`;
```

### Tagged templates call a function

> If there is an expression preceding the template literal, this is called a tagged template. In that case, the tag expression (usually a function) gets called with the template literal, which you can then manipulate before outputting.

The MDN examples with [Template_literals#tagged_templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates) make sense! I think?

## Call multiple endpoints

> The Promise.all() method accepts an array of promises. It doesn’t resolve itself until all of the promises in the array resolve. If one of them fails, it rejects.

```js
// Call multiple endpoints with Promise.all()
function getNews() {
  Promise.all([
    fetch("https://vanillajsacademy.com/api/dragons.json"),
    fetch("https://vanillajsacademy.com/api/dragons-authors.json"),
  ])
    .then(function (response) {
      // Get a JSON object from each of the responses
      return Promise.all(
        response.map(function (response) {
          return response.json();
        })
      );
    })
    .then(function (data) {
      // Do stuff with the data here
    })
    .catch(function (error) {
      // Handle errors here
    });
}
```

> This method can be useful for aggregating the results of multiple promises. It is typically used when there are multiple related asynchronous tasks that the overall code relies on to work successfully — all of whom we want to fulfill before the code execution continues.

## Cross-site scripting (XSS)

Sanitize and encode to protect from cross-site scripting attacks:

- Replace `Element.innerHTML` with `Node.textContent` or `Element.innerText`
- or use a library like [cleanHTML.js](https://vanillajstoolkit.com/helpers/cleanhtml/) or [DOMPurify](https://github.com/cure53/DOMPurify) to handle markup
- Read more on MDN describing [types of security attacks](https://developer.mozilla.org/en-US/docs/Web/Security/Types_of_attacks)

## Shuffle arrays

> languages like PHP and Ruby have built in methods for shuffling arrays, JavaScript does not.

This is a really cool [D3.js visualisation of the Fisher–Yates Shuffle](https://bost.ocks.org/mike/shuffle/) that we use in the course for project **Find the Monsters** game.

## Find closest matching parent element

> You can use the Element.closest() method to get the closest parent up the DOM tree that matches against a selector.

```js
// Check if click happened inside [data-btn]
document.addEventListener("click", function (event) {
  if (event.target.closest("[data-btn]")) {
    console.log("click! on either button or on the img inside the button");
  }
});
```
