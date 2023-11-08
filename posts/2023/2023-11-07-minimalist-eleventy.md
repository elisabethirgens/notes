---
layout: post
title: "Minimalist Eleventy: tiny11ty 🌱"
date: 2023-11-07
---

…continued from yesterday, after [downloading all my photos from Untappd]({{ '/2023/11/free-my-photos/' | url }}). Today I set up the static site generator [Eleventy](https://www.11ty.dev/) on this project. My favourite way of using Eleventy is _using as little of it as possible_. The [starter projects](https://www.11ty.dev/docs/starter/) are all too elaborate for my taste, but…

I have my own: [github.com/elisabethirgens/tiny11ty](https://github.com/elisabethirgens/tiny11ty)

## Prerequisites

[Node.js](https://nodejs.org/) on my laptop — and a repo! I can start with a `README.md` and a `.gitignore` that is prepped to NOT commit these two directories that I will soon generate:

```
# Ignore packages, these will be installed in the build
node_modules

# Ignore the local build of static files from Eleventy
_site
```

## Get the package

```
npm install --save-dev @11ty/eleventy
```

With that I should now have a `package.json` and a `package-lock.json` and `node_modules` (that will not be committed). And in the `package.json` I want to add two scripts:

```json
  "scripts": {
    "start": "npx @11ty/eleventy --serve --watch",
    "build": "rm -rf ./_site && npx @11ty/eleventy"
  },
```

## Hello World

Set up an `index.html` with some minimalist markup:

```html
<!doctype html>
<html>
  <head>
    <title>tiny11ty</title>
  </head>
  <body>
    hello world 👋
  </body>
</html>
```

`npm start` to run Eleventy locally at http://localhost:8080 <br>
Verify that I can now see “hello world 👋” in a browser. Wohooo!

## Nunjucks

> A template is a content file written in a format such as Markdown, HTML, Liquid, Nunjucks, and more, which Eleventy transforms into a page (or pages) when building our site.

When migrating this blog [from Jekyll to Eleventy](https://github.com/elisabethirgens/notes/commit/2e76072093ac8b691895f116d78ce51c1511f76b) some years ago, I picked Nunjucks because opting for a “templating engine for JavaScript built by Mozilla” seemed like a good choice. Today I’m curious how much the Nunjucks project will be maintained in the future, but sticking with a familiar templating language for now. My templates are not complex, so feeling anything but locked-in.

For today’s project, I move my HTML into a main layout and two pages. This is the first time I set up an Eleventy page that was not a post, and whoa: all I had to do was create the photos file on root.

```
_includes
└── main.njk
index.njk
photos.njk
```

In my `tiny11ty` starter example for a blog, there is a separate template for a blog post. And if I were inclined to split up the header and the footer, they’d go in the `_includes` but there’s just not enough HTML in there yet to bother. Proof in the [commit](https://github.com/elisabethirgens/tiny11ty/commit/aa49fee3c28589d20ec6d234b2f5417df64c140c) 💁🏻‍♀️

```
_includes
├── main.njk
└── post.njk
index.njk
```

## eleventy.config.js

Config is optional. It’s also where you can go bananas and the sky is the limit. But say I want dates in a human readable format, I can use this in my template: `{% raw %}{{ post.date | readableDate }}{% endraw %}`

- h/t to Bryan for [How to show your template code in 11ty blog posts](https://bryanlrobinson.com/blog/how-to-show-your-template-code-in-11ty-blog-posts/) 👆
- And what’s with the `|` ? That is a filter: [www.11ty.dev/docs/filters](https://www.11ty.dev/docs/filters/)

Then add something like this to my config:

```js
const { DateTime } = require("luxon");

module.exports = (eleventyConfig) => {
  eleventyConfig.addFilter("readableDate", (dateObj) => {
    return DateTime.fromJSDate(dateObj, { zone: "utc" }).toFormat("d LLL yyyy");
  });
};
```

Also useful to note:

> If we want to copy additional files that are not Eleventy templates, we use a feature called Passthrough File Copy to tell Eleventy to copy things to our output folder for us.

## As little CSS as we can get away with

- I need to add `<link rel="stylesheet" href="{% raw %}{{ '/css/main.css' | url }}{% endraw %}" />`<br> to my `_includes/main.njk`
- and `eleventyConfig.addPassthroughCopy("css");` to my `eleventy.config.js`
- along with the `.css` files I want to have

Another example commit from [tiny11ty](https://github.com/elisabethirgens/tiny11ty/commit/1e371f292718d0d23564f5a01daf8c9794fec8e3) because yes, it’s true — that is all a minimalist Eleventy blog might need. Browsers are packed with built-in styles. Visually kinda plain, but super useful if we manage to not reset them or break their awesome functionality. If you are a developer who is used to spinning up toolkits for layout, you’d be forgiven for not knowing how snazzy browser styles actually are. The web is fluid and content is responsive out of the box. Mobile or desktop or whatever, I don’t need media queries or other CSS for the layout here to adapt to different viewport widths.

✌️
