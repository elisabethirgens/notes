---
layout: post
title: "Complete the First React Course Assignment"
date: 2019-12-30
---

I’m taking the Udemy course [React - The Complete Guide](https://www.udemy.com/course/react-the-complete-guide-incl-redux/) and today it was time for the assignment after section 3: “Understanding the Base Features & Syntax”.

🏆 Nailed the assignment without peaking, but can’t say I found it easy. Spent a lot of time rewatching the video with instructions over and over to understand what they actually meant, wrote a lot of code that didn’t compile, referred to previous code from the course, rewatched certain lessons. Phew.

Now writing up some notes for me to repeat & reference later:

## Create new components 🌱

- Make new directory with a new file, named like component (but TitleCase here)
- Create a function component (unless I need to manage state, then consider class component)
- Remember naming conventions with camelCase

```javascript
// Enable my JSX to be converted to React elements
import React from 'react';

// Create the component itself as a function
const myComponent = () => { ... }

// Make it possible to access this component from another file
export default myComponent;
```

## Use new component inside `App.js` ⛽️

```javascript
// Make it possible to add the new component in this container
import MyComponent from "./MyComponent/MyComponent.js";
```

```javascript
return (
  // Add my new component as a self-closing tag
  <MyComponent />
);
```

## Set up some props 🎭

```javascript
// Pass a prop (string for now, but something else later)
<MyComponent myDynamicContent="will come here later" />
```

```javascript
// Accept a props argument in the function
const myComponent = (props) => {
  // Output the prop to display it in the browser
  return <div> {props.myDynamicContent} </div>;
};
```

## Manage state in the container ♻️

- Add state inside the `App.js` class component

```javascript
// Add state property to the class with a new username property
state = { developer: "Elisabeth" };
// Add a method to be able to manipulate the state
changeDeveloperHandler = (event) => {
  this.setState({ developer: event.target.value });
};
```

```javascript
// Pass something dynamic from the state to the component
<MyComponent myDynamicContent={this.state.developer} />
```

## Pass event handler and bind it to event 🤹🏼‍♀️

```javascript
<UserInput
  // Pass a reference to the event handler method
  changed={this.changeDeveloperHandler}
  // Enable the two-way binding by passing a reference
  currentDeveloper={this.state.developer}
/>
```

```javascript
const userInput = (props) => {
  return (
    <input
      type="text"
      // Bind my event handler to the change event
      onChange={props.changed}
      // Add two-way binding
      value={props.currentDeveloper}
    />
  );
};
```

While I follow all this technically and made it work in my actual app code, I don’t get how it’s a great idea to pass references back and forth between small files like this. Wouldn’t it then be easier to read if more code was gathered in slightly larger files?!

## Add styles 🎨

```javascript
const mySpecialInputStyle = {
  padding: "0.5rem 1rem",
  border: "3px solid teal",
  fontSize: "1.25rem",
  fontFamily: "Monaco, sans-serif",
  color: "slategray",
  marginBottom: "1rem",
};
```

```
    // Add the style attribute to the element
    <input style={mySpecialInputStyle} />
```

Task was to use both inline and adding separate stylesheets. CSS is my home turf, so this part is easy. And I have to admit, I can already feel my annoyance for the weird syntax slightly waning — all thought I’m still not convinced it’s a good idea.

---

_But yay! Section 3 all done and thoroughly dusted. Only 27 more to go…_
