---
layout: post
title:  "Salvage The Sunken Source Maps"
date:   2019-07-25 14:00:00 +0200
---

The annoying bug I’ve been hunting down for 3 days resulted in 2&nbsp;files changed, 3&nbsp;insertions(+), 2&nbsp;deletions(-). It was quite the debugging adventure, and I took plenty of notes along the way to avoid getting lost. Now slightly rewritten into this post, so future-me will remember what I learnt.

While reorganizing a handful of CSS and JS files, I was getting console warnings. First it took me _forever_ to realize it was not my changes, the setup didn’t work on master in production either.

---

Out of the box (mwahaha) [Parcel](https://parceljs.org/) will create source maps by default. But it’s not working in this app. Source maps are helpful for debugging CSS, so I want to get this working.

## Firefox dev tools

The first thing I notice, was a console warning:

> Source map error: request failed with status 404

(Later, I got really tripped up by how the warning wasn’t there initially. I thought I’d fixed it! But then I understood that it only appears _after_ you attempt to interact with the CSS bundle. Which explains we’ve not noticed it before, nobody’s been poking at this CSS in a while.)

The link in the warning to [learn more on MDN](https://developer.mozilla.org/en-US/docs/Tools/Debugger/Source_map_errors) was really helpful, but it took a while to understand how to grok this suggestion:

> The fix here is to make sure the file is being served and is accessible to the browser

## Chrome dev tools

There was no console warning in Chrome, and also the source CSS is completely minified on one line. (Interesting that Firefox will make the stylesheet readable for you, even though the source map is missing.)

## More about source maps

> A source map provides a way of mapping code within a compressed file back to it’s original position in a source file.

* [Treehouse: An Introduction to Source Maps](https://blog.teamtreehouse.com/introduction-source-maps)
* [CSS-Tricks: Should I Use Source Maps in Production? ](https://css-tricks.com/should-i-use-source-maps-in-production/)

## Check the files in a browser

✅ I can see the minified and bundled CSS<br>
`https://www.___.com/fabulous-app/assets/awesome-styles.css`

✅ and that Parcel has added this line at the end:<br>
`/*# sourceMappingURL=/awesome-styles.css.map */`

✅ How does this work? Ok, in a different app with working source maps, I can see how the URL points to a file that the browser asks to download.

🚫 but here, there is no file, just http error 404 on this URL<br>
`https://www.___.com/fabulous-app/assets/awesome-styles.css.map`

## Check the files locally

This is a java web application. And ah… I can see that Parcel does indeed generate the source maps inside a `/target/classes/WEB-INF/assets/awesome-styles.css.map`

Soooo. 🤔 The files exist, but are “not served and accessible to the browser” just like the MDN help page said. I have no clue how the java part of this app works, but grepping words I found in the URL led me to a configuration file. And this code was quite readable. I could see where some assets were excluded from a security something and then added to a resource location. I repeated the lines for the source maps and omg yay it worked 🥳🥳🥳

✅ Running the app locally will now serve up a `awesome-styles.css.map` <br>
✅ I can totally add Java to my resume now, right?!

## But… not so fast!

A gazillion detours and dead ends and debugging the wrong thing at the wrong time is simplified away from this write up. I was debugging the following 👇 for ages, before I understood that ☝️ about how the maps were generated — but not served up by the java configuration.

## Parcel 📦

Ah, Parcel. The “zero configuration web application bundler”. I’m sure that’s great when setting up, but all I’ve wanted the past days is a config file to be able to understand what’s going on.

But I started to get the hang of how [Parcel CLI](https://parceljs.org/cli.html) worked.

* `build` is the main command in `package.json` for Parcel to do it’s thing in this app
* `--log-level 5` is nice for debugging
* `--no-source-maps` works as expected when I tried adding the option

But I want the source maps dammit and Parcel is still adding an extra `/` to the URL, like so:<br>
`/*# sourceMappingURL=/awesome-styles.css.map */`

When I remove the extra slash in Chrome dev tools, the map and source files appear instantly. So now I know what the correct URL is, but how do I get Parcel to generate this:<br>
`/*# sourceMappingURL=awesome-styles.css.map */`

### Read GitHub issues until my eyes bleed

So many. 👀👀👀 But especially these two:

* [parcel-bundler/parcel/issues/2209](https://github.com/parcel-bundler/parcel/issues/2209)
* [parcel-bundler/parcel/issues/1753](https://github.com/parcel-bundler/parcel/issues/1753)

My huge debugging mistake, was that I was trying this fix before I had fixed the serving and before I had understood how/where/what/when Parcel was doing anything at all. So I _thought_ that nothing worked with using the option to [Set the public URL to serve on](https://parceljs.org/cli.html#set-the-public-url-to-serve-on).

But in fact… `--public-url=./` did the trick.

And tada! We now have functioning source maps that provide developers with easier debugging of CSS and Javacript in this application.

---

## What I learnt

* The basics of how Parcel works and how to actually understand the docs
* More about source maps and dev tools 🔨
* Remember to test some explicit changes first to learn what gets generated and built when, so that I’m not trying a bunch of fixes without actually implementing them
* Before searching the internet for fixes, spend time to understand how different parts are glued together, because it makes it so much easier to know if the fixes I find work or not
