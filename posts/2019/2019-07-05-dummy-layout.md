---
layout: post
title: "Dig Into The Dummy Layout Diffs"
date: 2019-07-05
---

A recent minor annoyance has been that making changes in one of the app causes git diffs in files I haven’t touched. I’ve previously stashed them and moved along, but today I’m digging into why this happens and figuring out how to improve the setup. 🕵️‍♀️

```
dummy-layout.html
dummyMenuAppDecorator.jsp
```

The uncommited changes that appear are the checksum in linked css and js from a design system. And I know that there are 3 separate applications involved:

- The app X I’m working in and has these files
- The layout application
- The design system in a different repo

The content of the files are copies of source code in the layout application, and I assume the purpose is for running the app X locally with surrounding layout?! It looks like running the app locally causes changes in just the html file. While running the full build will cause changes in both html and jsp.

- How are these files generated?
- Where and how is the checksum set?
- Should these files be ignored by git?

## Checksum

The design system deploys a `main.min.css` of bundled and minified CSS. Individual stylesheets are imported in one `main.css`, we’ve got the PostCSS runner [postcss-cli
](https://github.com/postcss/postcss-cli) that makes [cssnano](https://cssnano.co/) eat up all the whitespace and other optimizations for making the file as small as possible. But the design system does not have any type of versioning or checksums.

Let’s go see what I can find in the layout application. The template files are in [Freemarker](https://freemarker.apache.org/) and there’s a difference in how the internal and the design system css link href’s are set up:

```
<link /// app-internal.css?_t=${header.cssChecksum}"/>
<link /// design-system/main.min.css?cache=${header.cacheId}">
```

Tracking them down both send me into models and controllers java, but I’m not sure why we have different parts of code to do those two. Is there a reason we have separate cache busting techniques? Or is it basically because different people committed these with 2 years in between.

### 1: bash script with md5sum and awk

I think the first uses a bash script with `md5sum` to generate a number and change the file name.

### 2: java time stamp

The second technique looks way simpler with fewer lines of code, just touching one file with a `System.currentTimeMillis()` to generate a unique enough number. Found everything I will ever need to know about [currentTimeMillis](https://currentmillis.com/tutorials/system-currentTimeMillis.html) in a wonderful write up. 🙌

---

## Looping back to the original issue…

Let’s test the theory about ignoring the files in git. No effect at first, but doh… I need to delete the file first and _then_ add the `.gitignore` rule. Thanks [Atlassian git tutorials](https://www.atlassian.com/git/tutorials/saving-changes/gitignore), you’re the best.

Ignoring works. Wohoo! I removed the annoyance. (Reading code and git history is making me wonder if the entire setup that generates these files is old code that can be deleted, but that is something to look into over the weekend.)
