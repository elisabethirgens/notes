---
layout: post
title:  "Understand React JSX and Components"
date: 2019-12-27
---

More course study notes from moving through [React - The Complete Guide](https://www.udemy.com/course/react-the-complete-guide-incl-redux/) section 3.

---

Why have I seen both filenames `.js` and `.jsx` in React?<br>
Both work fine, but `.js` is convention these days.

### Not technically HTML, it’s JSX


```
return (
  <div className="App">
    <h1>I'm a React app</h1>
  </div>
);
```

That ☝️ get’s compiled to something like this 👇

```
return React.createElement('div', null,
       React.createElement('h1', {className: 'App'}, 'I\'m a React app')
);
```

Cool exercise in the course, rewriting the JSX-ish "HTML" from the first example to the second.

This gave me a lot of context for the concept of [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar):

> syntactic sugar is syntax within a programming language that is designed to make things easier to read or to express. It makes the language "sweeter" for human use: things can be expressed more clearly, more concisely, or in an alternative style that some may prefer.

* JSX is syntactic sugar for JavaScript
* It allows me to write HTML-ish code
* …without having to grapple with nested React.createElement(...) calls

🤯 Soooo… _this_ is in fact why a front-of-the-frontend developer like me has been able to be productive in React applications without actually knowing a lot of neither js or react. I think I’m writing HTML, but React is converting it behind the scenes.

## Restrictions of JSX

Here is some of the stuff that has annoyed me about React in the past, and understanding properly _why_ helps to accept different syntax. It’s not just because library authors “opted to be weird”, there are technical restrictions with reasons that I can now learn.

* `className` because `class` is a reserved name in JS
* one root element, because the JSX expression requires it

## Capitalize name of custom components

* Uncapitalized components are reserved for native HTML elements
* Uppercase first letter in my own components, like `<Person>`
* React will then identify it as a custom component

## Two ways of creating components

**Functional components** are also know as "presentational", "dumb" or "stateless" components. They are created for example by using using ES6 arrow functions.

**Class-based components** are called "containers", "smart" or "stateful" components. I can create them with using a ES6 class to extend React’s component.

_(Currently confused why the instructor calls the first as best practice. If I only need presentational components, why do I need React?! But I’m sure this will become clear as I proceed.)_

## Use props

1. Receive props in the component: `const person = (props) => {...}`
2. Output props dynamically: `<p>I’m {props.name} and {props.age} years old</p>`
3. Pass props as arguments: `<Person name="Alice" age="37" />`

---

## Parentheses for multiple code lines

```
  return <p>whatever on a single line of code</p>
```

```
  return (
      <p>whatever across
          multiple lines as needed
      </p>
  )
```

Related: Adjacent JSX elements need to be wrapped in an enclosing tag. This I am used to from before, and I’ve even bumped into the syntax for [fragments](https://reactjs.org/docs/fragments.html) to group a list of children inside `<React.Fragment>` and new [short syntax](https://reactjs.org/docs/fragments.html#short-syntax) with empty tags `<></>`.

## Give props children

Here is how I can pass content as props directly where my component is being used. Simple text here, but this feature becomes useful when it’s complex html.

```
  return (
      <p>I’m {props.name} and {props.age} years old
        <span> {props.children}</span>
      </p>
  )
```

```
  <Person name="Carmen" age="66">
    and I love cars
  </Person>
```
