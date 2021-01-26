---
layout: post
title: "Adventures in upgrading Yarn"
date: 2017-08-08
---

Monday morning started off with an intent to upgrade Yarn. **I did something I’ve done many times before;** copy/pasted a command that came whizzing by on Slack. It was a chained command with words I had a sense of familiarity about, but no real understanding of what would actually do. I&nbsp;had to ask where to run it, because I wasn’t sure where I was supposed to upgrade Yarn.

It wasn’t immediately obvious if the upgrade was successful or not. There was some output to suggest it wasn’t. **Then I did something I haven’t done before**, at least with problems like these… I&nbsp;decided to throw a lot of effort into learning more _before_ asking for help. Of course, I&nbsp;do figure stuff out on my own all the time, but it tends to be for solving problems in the vicinity of what I already know. This was not. But I convinced myself it was a good opportunity to practice some learning grit, and to feel uncomfortable for not understanding — but trying anyway.

---

`brew update && brew upgrade node yarn` didn’t work because:

- Yarn had originally been installed with npm 🙃
- The command also gave me a git issue with a patch that failed to merge (which upon closer inspection had a commit date correlating to my 2nd week at work two years ago when the machine was brand new and probably when Homebrew was first installed, ahem…)
- And it was really confusing that the HOMEBREW_REPOSITORY migrated to `/usr/local/Homebrew` which was why I couldn’t at first even find the directory that borked.

---

I got some help figuring all that 👆 out. But the really cool thing is that because I spent basically two half workdays reading up on my own first, we could start in a completely different spot when I eventually did ask for help. I now know a serious fuckload more that I did 36 hours ago:

## Homebrew

- a command starting with `brew` refers to [Homebrew](https://docs.brew.sh/) 🍺
- which is a package manager for installing software on my operating system
- stuff like node and git can be installed with brew
- but unlike npm, it’s not used for handling packages in a repo

## npm

- on the other hand, is a package manager [specifically for JavaScript](https://docs.npmjs.com/getting-started/what-is-npm) 📦
- npm is both a client and a registry
- and we use it for two different types of packages:
  - local dependencies in a repo
  - but also those that are globally installed on my machine

## Yarn

- is an alternative npm client [released last year](https://code.facebook.com/posts/1840075619545360) 🌱
- that installs the same packages from the same registry as npm
- and just like npm, we use it for:
  - local packages so everyone working on a project has the same setup
  - but it can also install packages globally on my machine

## package.json

- handles dependencies in Node.js modules for the npm registry
- but it’s also used to do the same in other projects
- a project can use one client (either npm or Yarn) to handle npm packages in that project
- the client is defined in the project, so a developer working on it will not use a different client that the next developer
- but the `package.json` file looks the same regardless of client npm or Yarn

## Managing my package managers and global packages

- While a `package.json` file handles local project modules, I should take more responsibility for knowing what is installed on my machine: both the package managers and the packages that are installed globally. And perhaps even… updating it all once in a while… 🙈
- `brew update` will update the Homebrew package manager itself
- while `brew upgrade` will upgrade the packages I’ve installed with brew
- `brew pin <formula>` can stop something from being changed
- postgresql and mysql are now pinned to current versions on my machine, so I don’t upgrade any databases before there’s a specific need to do so
- which means I can safely update and upgrade now that I know brew is a thing I have on my machine and what it does ✨
- I have now uninstalled Yarn with npm. And I’ve instead used brew as that is now the primary suggested way of [installing Yarn](https://yarnpkg.com/en/docs/install). 👌

Puh.

That adventure was both really uncomfortable and in the end very awesome.
