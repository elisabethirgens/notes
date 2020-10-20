---
layout: post
title:  "Create React App"
date:   2019-12-23 12:00:00 +0200
---

I’m continuing with section 3 of [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

##  About Build Workflow

* **Why?** Optimize code, use next-gen js, linters +++
* **How?** Manage deps (npm), bundler (webpack), compiler (babel), dev server

This concise explanation of a build workflow was super nice. Would have been useful to see this 3 year ago, feels like I’ve had to learn this the hard backwards way. Anyway…

## Set up the project

The course suggest to install globally with `npm install -g create-react-app` but I’ll go with running using `npx` to run it directly. The course was probably recorded before that was possible, and it’s what [the updated React docs](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app) recommend now. But seems like a good idea to use the exact same version of the scripts as the course I’m following.

```
npx create-react-app cheeseburger --scripts-version 1.1.5
```

Naming! I’ve always had `cheesecake` as my go to `foo` word when testing stuff. When I was learning Python two winters ago, I named my fizz buzz project [cheesecake]({{ site.baseurl }}/2018/01/cheesecake/). Since our course project app will be something burger related — naturally mine should be called a cheeseburger. Let’s go!

```
added 1312 packages from 734 contributors and audited 14828 packages
```

Puh. That’s a lot. And pretty amazing.

### I get a PWA out of the box with

* `public/manifest.json`
* `src/registerServiceWorker.js`

---

## But what about other projects? 🤔

Using the magic [`create-react-app`](https://github.com/facebook/create-react-app) seems like an excellent way to kickstart using a new library. But for _actual_ software development on teams creating web applications, it feels counterintuitive to me. I know people have differing opinions and preferences… I look forward to developing my own!

I understand the benefits of not trying to reinvent wheels. And by using the awesome code others have written, me and my team can focus on solving other problems. That said, I also understand the benefits of not abstracting away so many parts of your applications that you don’t know the setup. Debugging becomes really difficult when everything is magic.

The course instructor says “It’s the officially recommended tool for creating React projects”.

Create React App’s [README](https://github.com/facebook/create-react-app#popular-alternatives) sounds more nuanced, saying it’s useful for:

> Learning React in a comfortable and feature-rich development environment.<br>
> Starting new single-page React applications.<br>
> Creating examples with React for your libraries and components.<br>

…and then listing a lot of cases “where you might want to try something else”.
