---
layout: post
title: "Level up with NodeConfEU"
date: 2022-10-07
---

This week I was lucky enough to visit Kilkenny — for 3 days jam packed with all things Node.js —&nbsp;at&nbsp;a&nbsp;lovely venue in the Irish countryside. 🍀 [NodeConfEU](https://www.nodeconf.eu/) gathers an international community of folks developing and using Node.js, for talks and workshops and hallway tracks and social events. I&nbsp;learnt so much! 🙆🏻‍♀️ But even more importantly, I am filled to the brim — much like the foam on a newly poured Kilkenny — with motivation for getting back to improving our Node.js apps at work.

Technically, I have been to a NodeConf before. In 2016, we organized [CSSconf Nordic](https://cssconfno.github.io/2016/#cssconf-nordic-2016), [Web Rebels](https://2016.webrebels.org/) and [NodeConf](https://oslo.nodeconf.com/) in Oslo over 4 days. For the day of NodeConf, I was on organizer hallway duty and didn’t catch any talks. And at the time, I
really didn’t know what Node.js even was, how it actually related to JavaScript the language and npm packages. Fast forward 6 years…

## Fastify my seatbelt for learning

Sunday evening before the event, I was talking with another attendee and [Fastify](https://www.fastify.io/) came up. I&nbsp;had to ask what that was, got a nice explanation and learnt that ‘Okay, Fastify is a web framework for Node.js’ and an equivalent to something I already knew: [Express](https://expressjs.com/). Fun experience, because Fastify is then mentioned again and again and again the following days, only now I know what it is. This is representative for how I have experienced learning in general, since starting a new job a year ago. The&nbsp;complexity of frameworks, libraries and tooling make up a vast amount of trees, so much that it can be difficult to see the forrest. But once I figured out how to see the landscape clearly, new snippets of knowledge fall into place way more easily. As conference attendees, we ask each other “favourite talk so far?” and I do enjoy the discussions that spring out of bringing a specific talk into the conversation. But for me, **my absolutely favourite aspect of the conference** has been the gradual layering of knowledge happening in my brain. I love the feeling of how bits and pieces just fall into place —&nbsp;connected to each other. This is a very different feeling from earlier years of frustration from trying to tame rogue free&#8209;floating parts of knowledge that didn’t quite fit together yet.

## Node.js evolution

[Lizz Parody](https://twitter.com/LizzParody) set us off to a great start Monday morning. I love her slides: [“New and Exciting features in Nodejs”](https://t.co/kpwZegxx2E) and am especially looking forward to try:

```js
// Use new test runner from node.js core (perhaps to replace a test framework?)
import test from "node:test";
```

```shell
# Start app with flag to watch for file changes (no need for dependency nodemon)
node --watch index.js
```

The Fetch API is coming to the back-end! 🎉 We won’t need the dependency [node-fetch](https://www.npmjs.com/package/node-fetch) anymore, and [Ethan Arrowood](https://twitter.com/ArrowoodTech) walked us though the history of the standards and implementations. Found the [Node.js v18 release](https://nodejs.org/en/blog/announcements/v18-release-announce/#fetch-experimental) with this code example:

```js
// node.js made fetch happen outside the browser
const res = await fetch("https://nodejs.org/api/documentation.json");
if (res.ok) {
  const data = await res.json();
  console.log(data);
}
```

Highly interesting to see releaser [Danielle Adams](https://twitter.com/adamzdanielle) present how they manage semver majors, security patches, the stages current / active LTS / maintenance LTS. Slides: [The Life and Times of a Node.js Release](https://slides.com/danielleadams/nodejs-release-nodeconf-eu-2022) (Whoa, the git that allows Node.js to have multiple release lines!) Directly useful for me, is a better understanding of when and why there is a new release. I’ve probably been grappling some hesitation about updating because I haven’t properly understood the consequences. But there is no reason to ignore minor updates or to fear a major update. Now I am inspired to pay way more attention to releases, and to more frequently reap the benefits of upgrading.

## Security, Security, Security

We had many presentations and discussions on vulnerabilities, updating dependencies and writing secure code. I am left with a sense of validation that the work I have been focusing on this year is important. And even more curiosity in playing around with different tools and learning:

- [Snyk](https://docs.snyk.io/snyk-cli/getting-started-with-the-cli) — various tools for security, but especially the CLI
- [learn.snyk.io](https://learn.snyk.io/lessons/?categories=javascript) — lessons on everything from SQL injections to XSS
- [Mend Renovate](https://www.mend.io/free-developer-tools/renovate/) — to automate dependency updates
- [LavaMoat](https://github.com/LavaMoat/LavaMoat) — tools for sandboxing an app’s dependency graphs
- [dotdotpwn](https://github.com/wireghoul/dotdotpwn) — a fuzzer to discover traversal directory vulnerabilities
- [open/source/insights](https://deps.dev/) — an experimental project by Google to understand my dependencies
- [npm-audit-resolver](https://www.npmjs.com/package/npm-audit-resolver) — to build a security practice with a `audit-resolve.json` file for packages that you decide to ignore when something can’t be fixed right away

OpenSSF has recently announced a guide on [npm Best Practices for the Supply-Chain](https://openssf.org/blog/2022/09/01/npm-best-practices-for-the-supply-chain/) with the published document in [github.com/ossf/package-manager-best-practices](https://github.com/ossf/package-manager-best-practices/blob/main/published/npm.md) 👀

All 3 days had workshops after lunch to dive deeper into a topic. Monday I joined [Liran Tal](https://twitter.com/liran_tal/) for [Developer Security Essentials with Snyk](https://www.nodeconf.eu/workshops/developer-security-essentials-with-snyk) where we had fun hacking a chat room app, and gained increased awareness about exploits and application security risks. Not sure it had quite dawned on me before; how containers and vulnerabilities inherited with base images are part of the picture.

## TensorFlow.js 😁😠

[Patty O'Callaghan](https://twitter.com/pattyneta) gave a super fun workshop where we got our hands dirty with using machine learning directly in a browser. I got to set up a webpage with a pre-trained model to recognise objects from my webcam stream. Happy to learn that I am most likely `a person`, and thought it was very funny that my pencil was probably `a baseball bat` 🤪 Next step in the workshop, I created my own model with [Teachable Machine](https://teachablemachine.withgoogle.com) to detect if my face was happy or angry. For about an hour, I was hanging out it the hotel lobby [making faces at my webcam](https://twitter.com/elisabethirg/status/1577349455183069197) to train and test the model.

## Build a Node.js CLI tool

My most awesome win for Wednesday was opting to join the workshop to set up a note taking CLI with features from Node.js core. [Simon Plenderleith](https://twitter.com/simonplend) & [Kevin Cunningham](https://twitter.com/dolearning/) had a great setup to guide us though parsing arguments with `parseArgs` and getting interactive input with:

```js
import * as readline from "node:readline/promises";
import { stdin as input, stdout as output } from "node:process";
import { fileURLToPath } from "node:url";
```

We also used `fetch` to get a response from [api-ninjas.com](https://api-ninjas.com/) to add some data to the notes. I really enjoyed this workshop, and of all the things I picked up from NodeConfEU 2022… maybe just maybe continuing to work on this CLI is the side project I will make a priority.

## More things I want to look into

- [Shell scripting with Node.js](https://exploringjs.com/nodejs-shell-scripting/toc.html) 📖 by Dr. Axel Rauschmayer
- [Fastify](https://www.fastify.io/) — a web framework to spin up Node.js 💁🏻‍♀️ (it would be interesting to learn what it takes to refactor an existing app currently using Express, and also see if I find a diff in speed)
- [Bilt](https://github.com/giltayar/bilt) — a build tool for npm monorepos
- [server.requestTimeout](https://nodejs.org/api/http.html#serverrequesttimeout) — “to protect against potential Denial-of-Service attacks in case the server is deployed without a reverse proxy in front”
- [Glitch](https://glitch.com/) — I knew of Glitch, but hadn’t created an account before the TensorFlow.js workshop. Got interested in finding more use cases for Glitch to teach and demo full-stack web apps ✨
- [Lyra](https://docs.lyrajs.io/) — a search engine I can run on both client and server
- [Replace Dependabot With a Single Dependency Upgrade Pull Request](https://www.oddbird.net/2022/06/01/dependabot-single-pull-request/)
