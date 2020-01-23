---
layout: post
title:  "Shift Down the Downshift"
date:   2020-01-23 20:00:00 +0200
categories: learning
---

I’m diving head first into React at work, and naturally it’s not the simple straight forward components in this app that want my attention. That would be too optimal. Nope, it’s one of the most complex components that is broken and needs work. I started updating dependencies to fix another bug, and those updates were not compatible with the dependencies of _this_ component and hello worse bug.

The project is currently using two different packages related to the functionality:

* [use-downshift](https://www.npmjs.com/package/use-downshift) — [github.com/elsangedy/use-downshift](https://github.com/elsangedy/use-downshift)
* [downshift-hooks](https://www.npmjs.com/package/downshift-hooks) — [github.com/silviuavram/downshift-hooks](https://github.com/silviuavram/downshift-hooks)

They are both very small projects with 1 contributor and <&nbsp;100 weekly downloads, but I found there was a different project with a whole community of 158 contributors and ¼ million weekly downloads in steady increase. Awesome! Not sure why our application didn’t implement this popular version, but it might have been related to early experimenting with hooks before those landed here:

* 🏎 [downshift](https://www.npmjs.com/package/downshift) — [github.com/downshift-js/downshift](https://github.com/downshift-js/downshift)

Now that our app has a bug related to those other packages, we should refactor to use the project that is maintained. Which is also what one of the first maintainers recommends in their readme. But… \*&nbsp;rolling up sleeves&nbsp;\* …wtf even is downshift anyway?! 🧐 Here’s where finding the actual downshift was useful, because it comes with articles and documentation and examples.

This one is very helpful: [Introducing downshift 🏎 for React ⚛️](https://kentcdodds.com/blog/introducing-downshift-for-react) — now I’m starting to understand what we are talking about. But I haven’t learnt enough React basics yet to follow everything, so I’ll try to pick apart and make some notes to study:

But first: haha, I enjoyed stumbling across this [naming discussion](https://github.com/downshift-js/downshift/issues/10) from 2 years back. Including how dropdown, select, and autocomplete are used pretty interchangeably as names for components.

* Alternative solutions will handle the rendering for you: `React.createElement()`
* Downshift doesn’t, it has **render prop** and **controlled props** instead
* It doesn't need to expose as many props because there's no rendering to configure

### render callback

* You only pass `onChange` and `render` props to `<Downshift />`

> The render prop is a function which is invoked with some helper methods and state for us to build our component. **downshift** is responsible for managing user interaction, state, and most of accessibility, and we're responsible for rendering things based on that state.

### prop getters

* `getInputProps` and `getItemProps` are prop getters
* “and they are the key to allowing you to render whatever you like”

> So long as you forward all the props to the appropriate element you're rendering (if you're rendering it at all), then downshift will do all the work of wiring things together.

### controlled props

> The most common of these is the `<input />` component which allows you to specify a value prop if you want to control what the input value is. If you specify that prop, then you're responsible for keeping it up to date (often this requires an `onChange` handler to keep things in sync with when the user updates things).

---

Not going to pretend I understand all of this yet, but way more that yesterday!
