---
layout: post
title: "Why I Won’t Approve Your PR"
date: 2021-06-22
---

> in-house development has been influenced too much by the GitHub open source PR driven development process. A process driven by zero trust doesn’t fit well in a team with trust.

[Patricia Aas wrote this tweet](https://twitter.com/pati_gallardo/status/1373343835330383878) a while back, and it obviously struck a chord with a whole bunch of people. There’s a great conversation in the thread and replies. Reading this helped put into words what I dislike about required reviews and the concept of **approving** pull requests within a team. 

## I kinda like PRs 💝

A strong culture of always having two sets of eyes on every change is great. I wrote this list a year ago on [What I Love About Pull Requests]({{ '/2020/05/pull-requests/' | url }}) and how the humble PR can be an opportunity to learn, teach, collaborate, share ownership, praise, communicate, know your team mates.

But I also really enjoyed Jessica Joy Kerr’s [Those pesky pull request reviews](https://jessitron.com/2021/03/27/those-pesky-pull-request-reviews/) — an excellent post about _better_ ways to work together. She makes a strong argument for ensemble working, and describes the context switching and queues involved in PR reviews like so:

> This defies everything we know about product development flow. We just increased WIP and slowed our response time by adding a wait into the process.

And her conclusion in this post, that makes so much sense to me:

> Pull requests are an improvement on working alone. But not on working together.

---

## Required reviews makes me sad ☹️

The problems I see with required reviews are that:

- All code changes get the same standard process. A minor style tweak, an urgent bug fix (“someone quick press the button please”), a radical change to tooling, fixing a typo, a large new feature.
- I worry that a standard process gets in the way of building a flexible culture for collaboration.
- Required review lends itself to us feeling less responsibility for our own code changes. Someone else will review and approve if it’s good enough, right?
- Waiting on code review can encourage us to accumulate work instead of [working in small batches](https://cloud.google.com/architecture/devops/devops-process-working-in-small-batches).
- For me personally, I also notice that this repo setting has changed the meaning of reviewing other people’s code. It&nbsp;makes me feel inadequate in the stack, instead of empowered to pitch in and collaborate on whatever kind of code change, like I used to. (Jessica writes in her post about what it actually takes to understand code and to understand a change as an asynchronous task.)

## Gate keeping

I removed myself from two CODEOWNERS files recently, because I decided that I basically reject this role of gate keeper. I can see some scenarios, also in-house, where I might want that role. But for most repos in the type of development organisations that I know? No. Not for me. 🙅🏻‍♀️

## Quality

But what about the quality control? We build quality into our systems by collaborating. Quality is ensured by spreading knowledge more than enforcement. (See also everything in Jessica’s post.)

## Responsibility

Should no-one be responsible? Yes! I am responsible for my code change. I don’t dump that responsibility on you as a reviewer. Taking full responsibility includes assessing my own confidence in the change and enlisting the amount of help from others as necessary. If I am messing about with something I have low confidence in, I will be very explicit in how I ask for help. Preferably at a much earlier stage than in opening a PR. But if I have high confidence in my code change, I would love for you to take a look, but I don’t expect you to spend too much time figuring it all out.

## Collaborating

Removing myself as a code owner doesn’t mean I’m not going to review PRs. I thought a bit about what the ideal flexible reviewing looks like for me as a reviewer:

- Your PR touches HTML, CSS or SVG and since you know I am an expert on that type of code that runs in browsers, you want my feedback and any improvements I can come up with. (Happy to help! Which level of critical eyes do you prefer at this particular time?)
- You finished up a thing we started working on together yesterday, of course I’d love to take a look.
- You refactored something I touched 3 months ago and want to show me. (Thank you!!)
- You’re pretty confident in your PR, but we always strive for two sets of eyes on every code change —&nbsp;because review is an opportunity to spread knowledge. I can read and ask questions. Or you can walk me though your PR while we review together. I learn a lot about our software this way.
- You have built new UI, but it was quick and dirty and wtf is up with the width in that flex shorthand, so you would like me to checkout the branch and iterate over the styling. (Sure!)
- You have done something in React that you are particularly proud of, and since you know I am becoming friends with React, you want me to show me so we can pair review.

---

So I will not approve your PR. But ask me for any of the above, and I will drop <s>everything</s> most things in my hands to collaborate with you on your code change and help get it off to production.

