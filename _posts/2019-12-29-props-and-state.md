---
layout: post
title:  "Introduce Props and State in React"
date:   2019-12-29 18:00:00 +0200
categories: learning
---

Continuing [React - The Complete Guide](https://www.udemy.com/course/react-the-complete-guide-incl-redux/) course today, but also reading the first couple main concepts in [reactjs.org/docs](https://reactjs.org/docs/hello-world.html) and taking some notes from there.

## More about JSX

Wrap multiple lines of JSX in parentheses, because there is a thing that sounds like it trips up people often: [automatic semicolon insertion (ASI)](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi).

* Use quotes for string values as attributes
* Use curly braces for expressions in an in an attribute

### “JSX Represents Objects”

> These objects are called “React elements”. You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date. –&nbsp;[reactjs.org/docs/introducing-jsx](https://reactjs.org/docs/introducing-jsx.html)

---

## More about components

The instructor does a great job of explaining the difference between function and class components, and also that the course will focus mostly on components extended from class. Reading the official [Function and Class Components](https://reactjs.org/docs/components-and-props.html#function-and-class-components) was a nice supplement:

* Function components are JavaScript functions
* Class components use [ES6 class](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) "special functions"

> if a part of your UI is used several times (Button, Panel, Avatar), or is complex enough on its own (App, FeedStory, Comment), it is a good candidate to be a reusable component.

### Props 🧩

> When React sees an element representing a user-defined component, it passes JSX attributes to this component as a single object. We call this object “props”.

> We recommend naming props from the component’s own point of view rather than the context in which it is being used.

### One strict rule ✋

> All React components must act like pure functions with respect to their props.

---

## State

I’ve worked plenty in different web applications for this concept to be familiar. UI in complex apps has different states, but varying technologies have not always been so smooth in dealing with that. Old apps have needed buttons for updating, while newer apps based on React could render UI changes _without_ users having to visit new pages or press refresh buttons. But… that’s just the very beginning for understanding the technical concept of state in React, but starting with a problem to solve is a good way for me to learn.

> State is similar to props, but it is private and fully controlled by the component.

The example with [Converting a Function to a Class ](https://reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class) explains that:

> The render method will be called each time an update happens…
> This lets us use additional features such as local state and lifecycle methods.

* Use `setState()` instead of modifying state directly
* React may batch `setState()` calls so updates could be asynchronous
* Calling `setState()` will merge the object into current state

### Free up resources with lifecycle methods

Common ones include: `render()` `constructor()` `componentDidMount()` `componentDidUpdate()` `componentWillUnmount() `

### this

[A function's `this` keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) is a primary expression in JS, and MDN says that “the value is determined by how a function is called (runtime binding)”.

* `this.props` is set up by React
* `this.state` has special meaning
* But I can also add additional fields to store something else

---

### Reusable and encapsulated?! 🤔

The `<Clock />` example on [reactjs.org/docs/state-and-lifecycle](https://reactjs.org/docs/state-and-lifecycle.html) looks good, but I get lost on the way. I can follow parts here and there, but as a whole it’s just not clicking at the moment.

🎗**Go back and study it again later!** 🎗
