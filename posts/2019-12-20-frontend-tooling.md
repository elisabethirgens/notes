---
layout: post
title: "Lint and Prettier and pre-commit, oh my!"
date: 2019-12-20
---

The project I’m now working on has been set up with:

- [ESLint](https://eslint.org/) to lint ECMAScript/JavaScript
- [Stylelint](https://stylelint.io/) to lint CSS (or other style syntaxes)
- [Prettier](https://prettier.io/) to format code
- [pre-commit](https://pre-commit.com/) as the framework for git hooks

So far so good, but I’m not at all clear on how these interact or the details. I see that ESLint is not installed on my machine, but what I want to understand properly is why/when/how — and what the best approach is to ensure the next new developer doesn’t commit code that breaks the build.

Because I thought my machine was set up fine, but turns out that everything happily passed on my laptop — but failed the build in one of the environments. How rude. And definitely something I’d like to dig into and understand properly, so I’m not tripped up by future issues around this.

---

## ESlint

- It’s _possible_ to install ESLint globally (but not recommended)
- When installed locally to the project, you can have plugins and shared configs
- [eslint.org/docs/user-guide/getting-started](https://eslint.org/docs/user-guide/getting-started)
- [eslint.org/docs/user-guide/integrations](https://eslint.org/docs/user-guide/integrations) (editors, build tools, CLI, git, testing)

### ESLint in this project 🤖

ESLint isn’t a dependency in our `package.json` because it’s bundled inside the `react-scripts`. The only references I can see are these:

```json
  "eslintConfig": {
    "extends": [
      "react-app",
      "prettier"
    ],
    "settings": {
      "react": {
        "version": "16.8"
      }
    },
    "rules": {
      "no-throw-literal": 0
    }
  },
```

Hm. Should the project have an `.eslintrc` file? Probably not, because apparently an alternative way to set configuration is using a `eslintConfig` key in a `package.json`. Read about that in [thomlom.dev/setup-eslint-prettier-react](https://thomlom.dev/setup-eslint-prettier-react/)

[Create React App – Experimental: Extending the ESLint config](https://create-react-app.dev/docs/setting-up-your-editor/#experimental-extending-the-eslint-config) — I _think_ this might be what we’ve got…? 🤔 Compared to the example, our file doesn’t have a `shared-config`.

Someone made plugin with React specific rules, but don’t think we’ve used [ESLint-plugin-React](https://github.com/yannickcr/eslint-plugin-react).

These also exist in the Prettier project, we only have the config not the plugin.

- [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)
- [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)

### ESLint on my laptop 💻

> Visual Studio Code support debugging out of the box with Create React App

Noted, but if I can lint from the command line, I’m happy with that for now. Or can I set up something in Atom that will not pick a fight with the rest of the setup?

All docs and tutorials explain how to set up ESLint from scratch and they’re really difficult to read and understand in the context of an existing codebase – especially since this runs containers.

---

## Stylelint

I used the [CSS Lint](http://csslint.net/) that Nicole Sullivan and Nicholas C. Zakas made back in the day. But apart from that, I’ve been preoccupied with deleting CSS and writing as little new CSS as possible, not bothering with linting CSS in recent years. But I do enjoy this article [css-tricks.com/stylelint](https://css-tricks.com/stylelint/) and quote:

> You need a mistake-preventing machine 🤗

[stylelint.io/user-guide/configuration](https://stylelint.io/user-guide/configuration) explains that:

> The linter expects a configuration object. <br>You can either craft your own config or extend an existing one.

[github.com/stylelint/stylelint](https://github.com/stylelint/stylelint) says you first need to decide how to use stylelint:

- on the command line
- in your text editor
- in for your build tool (ex: webpack)
- via the Node.js API
- as a PostCSS plugin

### Stylelint in this project 🤖

So… how do I figure out what “we decided” in this project?

- The project has a `frontend/stylelint.config.js` file
- …and multiple devDependencies in the `package.json`:

```json
    "eslint-config-prettier": "^6.0.0",
    "stylelint": "^7.8.0",
    "stylelint-config-css-modules": "^0.1.0",
    "stylelint-config-standard": "^16.0.0",
    "stylelint-order": "^0.2.2",
    "stylelint-processor-styled-components": "^1.6.0",
```

### Stylelint on my laptop 💻

Same as with ESLint, I don’t understand the workflow for using these tools as dependencies in a container world. When I don’t have node_modules on my machine, how can I lint locally while coding?

---

## Prettier

There’s a great section at the top covering [Why Prettier?](https://prettier.io/docs/en/why-prettier.html) More docs should write stuff like this, not just the “getting started” before you know why you might want something. Haha: “My motivations for using Prettier are: appearing that I know how to write JavaScript well.” 😂

Also found the explaination of [how it compares to linters](https://prettier.io/docs/en/comparison.html) helpful:

- **code-quality rules** are for linters (ex: no-unused-vars)
- but **formatting rules** can be set by either (ex: no-mixed-spaces-and-tabs)

So there is overlap — but Prettier can be used to do some types of formatting instead of linters. Why? The way I understand it now, is that Prettier was written to be opinionated and to focus on printing code. It takes input, formats and outputs that again without dealing with syntax. Linters actually read the code, can analyze it and find potential bugs. But Prettier is designed to not have complex configuration options, it just decides most styles for us, so developers can get on with coding.

> The first requirement of Prettier is to output valid code that has the exact same behavior as before formatting. Prettier only prints code. It does not transform it. This is to limit the scope of Prettier. Let's focus on the printing and do it really well! <br>
> – [What Prettier is concerned about (and not)](https://prettier.io/docs/en/rationale.html)

> Prettier gets rid of all original styling and guarantees consistency by parsing JavaScript into an AST and pretty-printing the AST.
> – [James Long announcing the project in 2017](https://jlongster.com/A-Prettier-Formatter)

### Prettier in this project 🤖

`package.json` with dependencies and scripts with misc settings (truncated here)

```
  "devDependencies": {
    "eslint-config-prettier": "^6.0.0",
    "prettier": "^1.18.2",
  },
  "scripts": {
    "prettier": "prettier --write --single-quote --trailing-comma=all",
    "lint": "npm run lint:js && npm run lint:css && npm run lint:prettier",
    "lint:js": "",
    "lint:css": "",
    "lint:prettier": "",
  },
```

And a `.prettierrc` file with our options, so these can be shared between developers’ editors. This was added recently, after I had problems with the pre-commit hook.

The different options for using [Prettier with a pre-commit tool](https://prettier.io/docs/en/precommit.html) are:

1. lint-staged [github.com/okonet/lint-staged](https://github.com/okonet/lint-staged)
2. pretty-quick [github.com/azz/pretty-quick](https://github.com/azz/pretty-quick)
3. pre-commit [github.com/pre-commit](https://github.com/pre-commit/pre-commit)
4. precise-commits (with husky)
5. bash script

Since I can’t see `husky` or `lint-staged` in our `package.json` and I don’t think we’ve bash scripted this, I’m guessing we have option 3. But it’s the option 1 that mentions:

> Use Case: Useful for when you want to use other code quality tools along with Prettier (e.g. ESLint, Stylelint, etc.) or if you need support for partially staged files

I love my [`git add -p`]({{ '/2017/06/git-add-patch/' | url }}) so now I’m curious if I _don’t_ have support for that with the way it’s currently set up. What does “support” mean in this context? Something I can work around?

### Prettier on my laptop 💻

- I’ve added [Prettier for Atom](https://atom.io/packages/prettier-atom)
- But there are so many settings to deal with 🤕
- Using ESLint together with Prettier:
  [prettier-atom#using-eslint](https://github.com/prettier/prettier-atom#using-eslint)
- Same with Stylelint: [prettier-atom#using-stylelint](https://github.com/prettier/prettier-atom#using-stylelint)

There are two ways to use the plugin:

- Automatically format on save
- Run the command Prettier: Format on files in the editor

The first sounds smooth to consider later, but for now I want less magic and more control.

> By default, we use the prettier instance in your project's node_modules directory. We highly recommend adding Prettier to your dependencies so that your team, CI tooling, and any scripts using Prettier all format code exactly the same way.

We have it as a devDependency, but wtf does that mean when I don’t have `node_modules`?!

> If Prettier can't be found in your project's node modules, then we fall back to using the version that comes bundled with the prettier-atom package.

A-ha. That is what’s happening now. I can’t run `prettier` as CLI, but my editor has a separate version. Which may or may not be the same version as the project. 😭

> Prettier will search up the file tree looking for a prettier config to use. If none is found, Prettier will use its default settings.

Sounds good, that’s what `.prettierrc` is for. We do need to make sure the settings are in sync with those in `package.json` but since there’s only 2 of them, that should be ok to keep track of.

Same as with the linters, I’m confused about the workflow in a container world. And I’m feeling skeptical of all the moving parts to maintain here.

---

## pre-commit

> Git hooks are scripts that run automatically every time a particular event occurs in a Git repository. They let you (…) trigger customizable actions at key points in the development life cycle.
> – [atlassian.com/git/tutorials/git-hooks](https://www.atlassian.com/git/tutorials/git-hooks)

- There’s a `.git/hooks` directory
- Built-in scripts are mostly shell and PERL
- …but I can write Python or anything that can be run as an executable
- Local hooks are not copied when I clone a repo, they need to be installed

> pre-commit is a framework for managing and maintaining hooks

[pre-commit.com](https://pre-commit.com/)

> It is a multi-language package manager for pre-commit hooks. You specify a list of hooks you want and pre-commit manages the installation and execution of any hook written in any language before every commit.

### pre-commit in this project 🤖

`.pre-commit-config.yaml` referencing:

- github.com/pre-commit/pre-commit-hooks
- gitlab…/…/…/git-hooks.git (our internal stuff)
- github.com/prettier/prettier
- github.com/pre-commit/mirrors-eslint

### pre-commit on my laptop 💻

I have set it up like so:

- `brew install pre-commit`
- There are alternative ways on [pre-commit.com/#install](https://pre-commit.com/#install)
- `pre-commit --version` to check status and version
- `pre-commit install` in the project to install the git hook scripts in my repo clone

And how to actually use in a workflow:

`pre-commit run --all-files` ❌ Eeep, don’t do that, it will start changing all the backend files…

`pre-commit run` in a dirty directory will first stash unstaged files, skip checks, then restore the stashed changes. So when I want to test the pre-commit hook, I need to stage changes first. 🚧

`pre-commit run` will run hooks on staged files 👍

---

## Timeline around the breaking build

Puh. Okay, here’s what I now sort of understand and suspect happened:

- I committed changes without having installed pre-commit or it’s hooks
- _Uncertain what happened next. The build hadn’t complained (why not?? or did it? I’m not sure because we had some OpenShift issues at the time)_ 🤷🏻‍♀️
- I set up pre-commit and prettier on my machine, but the project’s `pre-commit-config.yaml` and `package.json` had defined overrides that my editor had no way of knowing about, so I created a `.prettierrc` for editors to use
- Then I ran prettier in my editor, and formatted the files I had previously worked on
- And next I ran pre-commit in my terminal to check that it passed
- At the same time, I removed those custom values from `package.json` thinking that the pre-commit would pick up the overrides from the new `.prettierrc` config and that it was best to keep the settings DRY
- The build then broke _because_ that ☝️ last assumption was false
- Next I changed the `package.json` back to **include the custom values in the scripts**
- With this as the source commit, the build was happy again 👏

---

## What I learnt 🥳

- A boatload writing up all these notes. I’ve been editing and reorganizing as my understanding grew. A great reminder that I learn best when writing.
- That new developers absolutely need to set up pre-commit and install local hooks in the repo before they start commiting code.
- The README explains this now that I added it (but is there a way to enforce it?)

### also that `yarn why` is really cool

```
yarn why eslint
🤔  Why do we have the module "eslint"...?

=> Found "eslint@5.16.0"
info Reasons this module exists
   - "react-scripts" depends on it
   - Hoisted from "react-scripts#eslint"
```

---

## What I can figure out in January

I am still unsure of the workflow and how to make sure different machines use the same versions and settings of these tools.

### The script for Post-Commit Hooks in OpenShift:

`NODE_ENV=development yarn && yarn lint`

I can run this locally and it will point out any issues to fix.
But it will also create a bunch of stuff we don’t want:

- `yarn.lock`
- `node_modules` with a `.yarn-integrity`
- `frontend/node_modules` with all the packages

And I suspect the container runs with different version/settings that my machine, because I’m seeing errors that aren’t in sync.

```
npx prettier --check --single-quote --trailing-comma=all 'src/**/*.{md,js,jsx,ts,tsx,css,scss}' 'test/**/*.{md,js,jsx,ts,tsx,css,scss}'
```

When I [npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) run prettier on my laptop, with the same options as the script in package.json, this will complain about files that my editor’s version of prettier is happy with.

### What I’m used to from non-container projects

- package.json defines versions
- node_modules contains packages of the dependencies
- … and tada ✨ different developers and multiple servers are in sync ✨

### What I don’t understand in the context of this project

- Can I use ESLint without installing it globally ?
- How to property set up [atom.io/packages/linter-eslint](https://atom.io/packages/linter-eslint) ?
- Will my editor grab config from `package.json` ?

**This project runs on Openshift — and I basically do not understand how to package.json & node_modules in Docker containers.** Thankfully there’s always 2020. 💥

#### Stuff to continue reading in January

- [BretFisher/node-docker-good-defaults](https://github.com/BretFisher/node-docker-good-defaults#local-development-features)
- [Tactics To Keep Node.js Rockin’ in Docker](https://www.docker.com/blog/keep-nodejs-rockin-in-docker/)
- This OpenShift [issue about ignoring files](https://github.com/openshift/origin/issues/13255)
- OpenShift [release 4.1.3](https://access.redhat.com/errata/RHBA-2019:1589) that now supports `.dockerignore`
