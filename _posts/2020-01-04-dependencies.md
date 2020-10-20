---
layout: post
title:  "Work with Yarn in a Containerized App"
date:   2020-01-04 13:00:00 +0200
---

Before the holidays, I was fighting with [linters, prettier & pre-commit]({{ site.baseurl }}/2019/12/frontend-tooling/) and declared defeat:

> I basically do not understand how to package.json & node_modules in Docker containers. Thankfully there’s always 2020.

January is now, so… \*rolling up sleeves\* I shall learn more though working with the dependencies.

-------------------------------------

## Vulnerabilities and react-scripts

The version we’ve got is behind one of the critical when I run a `yarn audit` and this seems like the kind of thing we want to keep updated always anyway.

```
17 vulnerabilities found - Packages audited: 939962
Severity: 3 Low | 7 Moderate | 4 High | 3 Critical
```

But how to update? The [release notes](https://github.com/facebook/create-react-app/releases/tag/v3.3.0) suggest:

> Migrating from 3.2.0 to 3.3.0
> Inside any created project that has not been ejected, run:
`yarn add --exact react-scripts@3.3.0`

* How can I find out if this project has ejected or not?
* What if I’m updating from an older version than 3.2.0?
* Is _migrating_ different from _bumping the version_ in package.json?

Read a bit on [Migrate react-scripts v2.x to v3.0.0](https://medium.com/@TechMagic/migrate-react-scripts-v2-x-to-v3-0-0-17134a7ecc66) but also found the official [create-react-app.dev/docs/updating-to-new-releases](https://create-react-app.dev/docs/updating-to-new-releases) stating that:

> In most cases bumping the react-scripts version in package.json and running npm install (or yarn install) in this folder should be enough, but it’s good to consult the changelog for potential breaking changes.

“Most cases”…? “Should be enough”…? 🤔

### It’s kind of a funny story…

When I was working on this yesterday, I misunderstood and thought the release notes mentioned some kind of special migration script. The wording tripped me up, and I didn’t realize then that the command they suggested was basically a standard `yarn add` that would first bump the version number in `package.json`, and next generate a new `yarn.lock`. So what I did to figure out what this “migration script” did, was to copy-paste the command and then compare the result to what happened when I manually bumped the number in `package.json`. I tested on two different git working directories, remembering to remove `node_modules` before trying the next approach. And then ran a `diff` on the separate `yarn.lock` files the approaches generated. Finishing up these notes today, now I understand that there’s no way they could have been different. [yarn add](https://yarnpkg.com/lang/en/docs/cli/add/) did exactly the same as I did manually in two steps. It’s interesting how docs with “just run this smart efficient command” can also obfuscate what _actually_ happens in your codebase.

### Ejecting react-scripts?

I also found this post about [Keeping up with Create React App (after ejecting)](https://www.breathelife.com/keeping-up-with-create-react-app-after-ejecting) that describes how ejecting creates a new `scripts` directory, so that could be an indication to figure out if a project has ejected or not. Learnt a lot and:

✅ Got rid of 1 critical: Arbitrary Code Execution ([npmjs.com/advisories/1118](https://www.npmjs.com/advisories/1118)) in this package: <br>`react-scripts > eslint > eslint-utils`

---

### What about other dependencies of react-scripts? 🤔

All the remaining high severity and a couple of others are still from dependencies of react-scripts after upgrading to the latest. Would be cool to get rid of those too, yeah?!

```
15 vulnerabilities found - Packages audited: 941521
Severity: 3 Low | 6 Moderate | 4 High | 2 Critical
```

[handlebars](https://www.npmjs.com/package/handlebars) has a newer version where the vulnerability is patched, but I can’t see any sign in the repos for WIP to bump versions thought the full path:

`react-scripts > jest > jest-cli > @jest/core > @jest/reporters > istanbul-reports > handlebars`

Did more searching, and read among other things a thread where [Dan Abramov discusses](https://twitter.com/dan_abramov/status/1149795615880011778) 👇

> I know npm vulnerability advisories are meant to help security. But I can’t shake the feeling the way it’s rolled out is creating confusion and FUD. I can’t count how many times I’ve seen build-time tools getting panic in issues because of “prototype pollution” or “regex ddos”.

> I want to make this clear. Those kinds of audit warnings are useless false positives for *build tools*. These false positives are a waste of everyone’s time. Users can’t upgrade, maintainers chase upstream patches — and all for an imaginary problem. I don’t know how to fix this.

> The vulnerabilities assume that your server processes some user generated input. But builds in e.g. Create React App don’t do that. So that doesn’t make real sense.

Interesting! I guess this is the price to pay for using something like `create-react-app`, that tools like `yarn audit` become cluttered — and in return, **I need to learn** how to separate what is important to handle and what is noise.

----------------------------------------------------------------------------------------

## Unmet Peer Dependency?

`yarn list` 😭 (There’s so much. On one hand, that’s awesome. Look at all this code someone else contributed that I can use. On the other hand, omg… this is one long packages list to maintain.)

```
yarn check
info Found 66 warnings.
error Found 110 errors.
```

Hm. Sounds bad. But read up a bit, found for example this post [Acknowledging Yarn Check Errors](https://medium.com/tomincode/acknowledging-yarn-check-errors-10f2ce7da4f6) and also a very helpful comment in a [yarn issue on GitHub](https://github.com/yarnpkg/yarn/issues/5347#issuecomment-463038189) that explains:

> the response here and in other issues against yarn are that this is how yarn works, yarn is not npm, npm is optimistic (if the package is there it's okay, no warning) but yarn is playing it safe.

But also:

> I guess it is just a warning and can be ignored, but some of us are in the "warnings are like broken windows" school of thought.

Where do I sign up?

----------------------------------------------------------------------------------------

## Noooo… wat? The build broke 😭🤨🤔

* Updating react-scripts worked when running locally in Minishift
* I committed the change, thinking all was fine in the world
* But the build broke in the dev environment on OpenShift

Well… I did set out to learn more about dependencies in containers… _something something different versions of node running in the environments… Got more work to do next week then!_
