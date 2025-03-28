---
layout: post
title: "The worlds tiniest rewrite from CJS to ESM"
date: 2025-03-28
---

My favourite way of using Eleventy is _using as little of it as possible_. The [starter projects](https://www.11ty.dev/docs/starter/) are all too elaborate for my taste. I have my own: [github.com/elisabethirgens/tiny11ty](https://github.com/elisabethirgens/tiny11ty) and it was set up two years ago, when `@11ty/eleventy` used Common JS.

> Historically, Eleventy (prior to version 3) has worked with the Node.js default flavor of JavaScript modules: CommonJS.
> However, ESM (ECMAScript Modules) are a newer JavaScript standard that will work in more JavaScript environments and runtimes.

—&nbsp;[www.11ty.dev/docs/cjs-esm/](https://www.11ty.dev/docs/cjs-esm/)

I haven’t done any rewrites to ESM before, so I was hesitant. How much would I need to change? Well, it seems that I have now done the tiniest rewrite from CJS to ESM in the history of rewrites.<br>
The entire thing in this [commit](https://github.com/elisabethirgens/tiny11ty/commit/306643b84a725efb186b636c6d3258943c6950f3) has `+3
-2 lines changed` 😂

```js
// First lines of eleventy.config.js before
const { DateTime } = require("luxon");

module.exports = (eleventyConfig) => {
    // ...
```

```js
// First lines of eleventy.config.js after
import { DateTime } from "luxon";

export default (eleventyConfig) => {
    // ...
```

VS Code fixed that for me 👆 and in addition I needed to add `"type": "module"` to my `package.json` which I had forgotten but was reminded of when `npm install` failed. And that was that! I have rewritten my first project from CJS to ESM.

### Maintenance of tiny11ty

I remember it taking some work to figure out how to remove a lot of stuff from my set up of Eleventy, but it really turned out quite minimal. Now it is fun to see what a managable amount of work is needed to be done to keep this project updated. The build broke on a different project with the same set up, and that was due to outdated versions of actions in the GitHub workflow. So the first change was necessary, but the other three were more optional.

- Update GitHub workflow actions [commit](https://github.com/elisabethirgens/tiny11ty/commit/079f39b3d3e235774f29e38de547803b3c2dd196)
- Update @11ty/eleventy to v3 [commit](https://github.com/elisabethirgens/tiny11ty/commit/7f9b300fc0818f2575a28e3b2a0d97cba852e072)
- Tiny rewrite from CommonJS to ESM [commit](https://github.com/elisabethirgens/tiny11ty/commit/306643b84a725efb186b636c6d3258943c6950f3)
- Refactor from Nunjucks templating to use Liquid [commit](https://github.com/elisabethirgens/tiny11ty/commit/c4797bb83d04ced6a1d15e55737a275704ff6f40)

Nunjucks is the templating I choose originally, but I get the impression that Mozilla is no longer maintaining that project? It still works just fine, but I wanted to try using Liquid. It will be fun to follow how much or little maintenance this project will need in upcoming years!
