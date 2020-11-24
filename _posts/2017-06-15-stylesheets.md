---
layout: post
title:  "Be fearless with old stylesheets"
date: 2017-06-15
---

The community talks a lot about writing CSS, and less about dealing with old stylesheets that no-one knows what do anymore. But I’ve had interesting discussions with friends working elsewhere, that have helped me think more about how to approach old CSS.

It’s easy to have too much respect for old CSS. *“Look at all this, that someone put a lot of work into meticulously naming and painstakingly structuring.”* But browsers change, teams change, best practices change, and what might have been spiff back then — is now just rusty and dusty.

There are basically two paths — and being fearless helps in both.

## 💥 Tear it down, then go rebuild

If the old CSS mostly does the job, there are limits to how much effort you want to put into polishing a section of UI or the code behind them. Refurbishing what is already there, can seem like the most efficient approach. I’ve gotten fooled a lot by this recently. When I finally give up and start from scratch, it turns out that rebuilding was by far the simplest way.

## ✂️ Chop first, then fix what you break

But sometimes you do just want to simplify existing code without rewriting too much. When I&nbsp;recently deleted 200 lines, I sort of knew what I was doing and had mostly control over the consequences. But… it was a bit happy-go-lucky. A week later, it seems I just broke one tiny little thing, and it was easily fixed once spotted. No real harm done and our code is improved.

---

**Note to self** — You do actually have some badass CSS skills under your belt, so go be fearless when changing, deleting, writing and rebuilding.
