---
layout: post
title:  "Jump Into Rabbit Holes! Upgrade Dependencies!"
date: 2018-07-24
---

Summer weeks at work have been great for venturing down rabbit holes, and I have done so with unprecedented determination to be okay with both getting lost – and ending up in completely different places than originally planned.

My local repositories have been a mess of different projects in the same directory, and I’ve been meaning to reorganize. We have a script to clone all repositories from our GitHub organization, and also a `good-morning` ☕️ script for automatically pulling from master. Wanting to put those to use was a great opportunity to move around project directories, and set up a lot of things from scratch. I&nbsp;used to be hesitant to touch things that work, but now I’m so much more likely to barge at it, just to see what breaks. Quite a change, and it’s really empowering. 💪

---

## The rabbit hole entrance 🐰🕳

* Cloned the design system repo fresh from GitHub
* Oh, right. I need to install the dependencies?!
* `yarn install` failed due to incompatible module (node)
* Ran `yarn upgrade` and got a new `yarn.lock` 🎉
* Hello, `node_modules`! 👋 There you are.
* Building CSS and deploying works again, yay.

Typing this list up, it’s all pretty clear – which is neat to realize, because why nothing worked wasn’t obvious at first to me that day. But I got some warnings in the output. And how to actually upgrade what needed to be upgraded in the project? And understand what I was doing and why?

---

## What I understood already 👌

* Generally [how packages work]({{ '/2018/02/npm/' | url }}) (from just 5 months ago, though!)
* Yup, lock files are intended to be checked in.
* yarn is an alternative npm client and all that

## What I was confused about 🤔

* But where does yarn stop and npm start?! no puns intended
* How should I upgrade dependencies to _latest_ versions?
* And do I change the version numbers in `package.json` manually or wat?

## Yarn handles what exactly in this project? 👀

Brew has installed Yarn on my machine. But what does it actually do in this design system repo? Let’s&nbsp;read some code and old commit comments to find out…

* There is a [Jekyll plugin](https://jekyllrb.com/docs/plugins/) with a hook that will run `yarn install`. When I run `jekyll serve` to work on a local dev server, this will usually take care of installing dependencies locally.
* The same hook also runs `yarn build-css` which is name we’ve given to the [scripts field](https://yarnpkg.com/en/docs/package-json#toc-scripts) defined in `package.json` with a series of automated tasks. Truncated dummy example:

```
{
  "scripts": {
    "build-css": "postcss autoprefixer cssnano"
  }
}
```

* The `Jenkinsfile` installs dependencies on the build server by running `yarn install` there, same as on my machine.
* …and finally a `yarn.lock` makes sure all installs on all machines use the same versions of the dependencies for this project.

## 🤯🎓😀
(I’m pleased and kinda surprised at how easy it was to figure out how those parts work together.)

---

## Check for outdated packages

A-ha! So even though this project uses yarn, I can still use npm tools like [npm-outdated](https://docs.npmjs.com/cli/outdated):

```
Package       Current  Wanted  Latest  Location
autoprefixer    8.6.5   8.6.5   9.0.1  x
cssnano        3.10.0  3.10.0   4.0.3  x
postcss        6.0.23  6.0.23   7.0.1  x
postcss-cli     5.0.1   5.0.1   6.0.0  x
```

## Yes, I can manually edit package.json ⬆️

This was difficult to ask the internet about, I got confused by both yarn and npm docs. But had a discussion over lunch and yes, it’s fine for humans to make changes in this file. (Later I played around with [npm-check-updates
](https://github.com/tjunnone/npm-check-updates) and saw how it can also be done automatically by a tool like this.)

## Semver version ranges 🥕

* `9.8.7` would be the same as using `=` for the exact version
* `<6.6.6` is a less than comparator, there is also greater than `>` and so on
* `2.x` will match major version
* `^1.2.3` is a caret range, up to the first non-zero digit

And there are loads more [ways to define versions](https://yarnpkg.com/lang/en/docs/dependency-versions/).

## Experiment in different clones 😈

Not being afraid of breaking the set up is really quite helpful! It meant that I could clone this project a gazillion times in different places, play around with the install and upgrade commands to see what they do when. And I had to think hard about this part, for a moment or two; but understood that since `node_modules` are not checked in, they are independent of my git branches. Right!

These commands will all look to what is defined in `package.json`:

* `yarn install` will fill up node_modules with all dependencies
* `yarn upgrade` will find new versions within the range

And a co-worker pointed to a different one:

* `yarn upgrade-interactive` seems fancy ✨

I’m still unclear on why install failed, but upgrade was success at the start of all this. But anyway, it’s much easier for me to read the about the [CLI commands](https://yarnpkg.com/en/docs/cli/upgrade) now. And my understanding of the application architecture increased greatly these past days. \o/
