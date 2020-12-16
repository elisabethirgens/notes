---
layout: post
title:  "Play Twister with Dependencies"
date: 2020-01-06
---

Last week I was figuring out more on how to [work with Yarn]({{ site.baseurl }}/2020/01/dependencies/) and dependencies in my new project. Main differences from the apps I knew from previous gig, is that there are a whole lot more dependencies here — and this application runs on [containers in OpenShift]({{ site.baseurl }}/2019/12/containers/).

* `yarn audit` shows a good handful of vulnerabilities, but apart from the problem with noise, I don’t need to worry too much about the ones related to devDependencies
* `yarn check` is not happy at all with 66 warnings and 110 errors, and here I’m not sure if I should be worried or not
* `yarn outdated` shows that a couple of months have passed since a frontender worked on this application and time moves fast in the world of javascript packages…

> Let me just do a quick basic version bump of react-scripts

Those became my Famous Last Words™️ last Friday, because the build broke. And this is where my confusion starts about environments and what runs where in which containers. How can this change build just fine locally, but then break in the OpenShift project? First I wanted to verify that it was the recent commit to upgrade react-scripts, and not something else. But sure enough:

✅ The build is green with `"react-scripts": "3.0.1"` — lots of warnings, but yarn install runs fine in OpenShift and sets up all the packages it needs.

```
warning "react-scripts > @typescript-eslint/eslint-plugin > @typescript-eslint/typescript-estree@1.6.0" has unmet peer dependency "typescript@*".
warning "react-scripts > @typescript-eslint/eslint-plugin > tsutils@3.17.0" has unmet peer dependency "typescript@>=2.8.0 || >= 3.2.0-dev || >= 3.3.0-dev || >= 3.4.0-dev || >= 3.5.0-dev || >= 3.6.0-dev || >= 3.6.0-beta || >= 3.7.0-dev || >= 3.7.0-beta".
[5/5] Building fresh packages...
```

❌ Assemble script failed with `"react-scripts": "3.3.0"` and output approx this:

```
error @typescript-eslint/eslint-plugin@2.14.0:
The engine "node" is incompatible with this module.
Expected version "^8.10.0 || ^10.13.0 || >=11.10.1". Got "10.12.0"
error Found incompatible module
error: build error: non-zero (13) exit code from docker-registry […]
```

## Debugging hint: node versions

My laptop is running 13.5 but I don’t think that is in play here.

```
node -v
v13.5.0
```

* When I run OKD locally with Minishift, I find `v12.10.0`
* but then there’s `v10.12.0` in the actual OpenShift project

In addition to that default project getting built from the `develop` branch, I have a personal version of the project in the same environment, and there I see that it’s `v12.10.0`.

## How did we end up with different node versions?

| Environment | node -v | |
|--|--|--|
| Locally via Minishift | `12.10.0` because that is currently the :latest of Nodeshift’s nodejs image | `DEV_MODE=true` `NODE_ENV=development` |
| My project on OKD | `12.10.0` because that is currently the :latest of Nodeshift’s nodejs image |  `DEV_MODE=true` `NODE_ENV=development` |
| Default project on OKD | `10.12.0` is a version included in our current cluster image stream and selected in an openshift template | `DEV_MODE=false` `NODE_ENV=production` |

## Can I upgrade to 12 everywhere?

Haha. Nope. Well, not right off the bat anyway. So end of the story today, is that [the dependencies beat me at this game of Twister](https://twitter.com/elisabethirg/status/1214271328666161154) and I need to downgrade `react-scripts` again for now.

---

But I’ve learnt a lot! I’ve pieced together some important parts today in understanding wtf images actually are and how build strategies work in OpenShift.
