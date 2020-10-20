---
layout: post
title: "A Map to Navigate the React Ecosystem"
date: 2020-10-05 17:00:00 +0200
---

THIS IS ABSOLUTELY AMAZING but [Sara Vieira](https://twitter.com/NikkitaFTW) has accomplished what no developer, myself included, has ever accomplished before: motivated me to use React for fun.

## 📚 The Opinionated Guide to React, _by&nbsp;Sara&nbsp;Vieira_

This book is ridiculously empowering — for me, where I am in my learning, right now. It’s not a resource to learn React from scratch, nor a deep dive into topics. But it provides a map of the ecosystem and was exactly the overview I was missing. Sara is clear that she is sharing her opinion, and this focus is a lot more helpful for me than having to deal with “here are ALL my options”.

The code examples are super useful. Limited in scope, but every one a complete application on it’s own. Never found that before. I’ve only worked in fully fledged applications with all the bells and whistles — or seen lone snippets of code in tutorials that float around with zero context.

Check out [The Opinionated Guide to React](https://opinionatedreact.com) 🚀 for a full summary of the topics covered in the book. The notes below are a subset, my personal takeaways and thoughts.

---

### Structuring files and folders

```
pages/         our main pages (with sections and modules)
components/    things to be reused multiple places
utils/         stash complicated functions away here
assets/        for images and icons
```

I like the simplicity in starting with these four. For applications in general, regardless of React, it is easy to get lost in “more categories must be better” when one long list of components and a single list of pages is much easier than attempts to maintain levels between the two.

- name files `index.js` and let folder names do the talking
- export named components for easier debugging ([eslint rule](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/display-name.md))
- `eslint-config-react-app` can also be used outside CRA and “saves you from all the common pitfalls without forcing you into a particular style”

### State management

Whoa. I had heard about different libraries with their pros and cons. But I hadn’t seen the library option described in relation to the existing parts of React like Sara explains nicely.

> “context is perfect for many use cases where you need state spread around your application, but that state is never going to grow into a big ball of complicated sadness”

- `useState` can handle simple state locally at component level
- `Context` is also built in, works globally and might be enough
- …and for more complex use cases: you want **a state management library**

> At CodeSandbox, we have been using Overmind for a while, and we were using its predecessor Cerebral before that. It is honestly a breath of fresh air when it comes to state management: it's simpler than most but super powerful and super extensible. You can use Overmind in big applications with minimal boilerplate.

### Project starters

I knew about all these, but hadn’t seen them compared as straight forward as this before — or described as “project starters”, which provides context for my mental model of what and why.

- [Create React App](https://create-react-app.dev/) with `react-scripts` to abstract away a lot of dependencies, great for a quick start, but beware; you have no access to Webpack or a Babel config
- [Next](https://nextjs.org/) is set up for server-side rendered out of the box and you can change the Babel config
- [Gatsby](https://www.gatsbyjs.org/) is a static site generator to export HTML, a lot of options for tools and plugins

It’s great to have these frameworks, but I want to learn setting up an application with my own build toolchain. Possibly famous last words coming up; but “how hard it can be?!”

### Potential problems and suggested packages

- Routing: [React Router](https://reactrouter.com/)
- State management: [Overmind](https://www.overmindjs.org)
- Animation: [Framer Motion](https://www.framer.com/motion/)
- Styling: [styled-components](https://www.styled-components.com/)
- Forms: [Formik](https://jaredpalmer.com/formik/)
- Dates: [date-fns](https://date-fns.org/)
- GraphQL: [React Apollo](https://www.apollographql.com/docs/react/)

The explanations about which problems I might want to solve in my application were really helpful. Sara covers which packages she often uses to solve those problems, and also when you need to look further. (In addition to this list, the book covers UI toolkits, icons and component playground.)

### Hooks

Sara’s examples on hooks are super approachable 🥰 and CodeSandbox helps a lot. Much less like the “how to draw an owl” tutorials on hooks I usually come across. I am looking forward to coding up these examples for myself and playing around with them.

### Deployments

Step by step to deploy all three project starters on Netlify and Vercel. Wohoo!

---

These are my personal notes from reading the book now. But [The Opinionated Guide to React](https://opinionatedreact.com/) itself is going to be updated as the ecosystem keeps evolving and I look foreward to following along when Sara‘s recommendations change!
