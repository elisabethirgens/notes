---
layout: post
title:  "Say Hello to Intrinsic Web Design"
date:   2018-06-27 16:00:00 +0200
categories: learning
---

This was [introduced by Jen Simmons](https://twitter.com/jensimmons/status/980980521848127488) – so I know it’s worth paying attention. But what is it? What does it mean for me, and is the concept relevant for the UIs I’m building at work?

### Intrinsic means belonging naturally

This is one definition I found of the word, along with some relevant synonyms: natural, native, built-in, ingrained, deep-rooted, inseparable. (Sounds like my kind of web design!)

### The antonym is extrinsic

Defined as “not part of the essential nature of someone or something; coming or operating from outside”. (Sounds just like pixel perfect sketches handed over from design to development!)

> Everything about web design just changed.

* [Slides](https://speakerdeck.com/jensimmons/everything-about-web-design-just-changed) from Jen Simmons talk at An Event Apart, Seattle 2018
* [Notes](https://adactio.com/journal/13671) from the talk, by Jeremy Keith
* [labs.jensimmons.com](https://labs.jensimmons.com/) has a lot of examples
* [youtube.com/layoutland](https://www.youtube.com/layoutland) 📺🤓👌

| Responsive Web Design | Intrinsic Web Design |
|---|---|
| flexible images | flexible images **or** fixed images (your choice!) |
| fluid columns | fluid columns **and** rows (you can have rows!!) |
| media queries | media queries only if and when needed |
| set of layouts for different screens | design a flexibility model for your content |

### Four stages of squishiness

Jeremy writes about these that they are…
> a powerful set of tools that may take us years to explore.

* fixed
* fr units (fluid)
* minmax()(fluid until fixed)
* auto (a return to flow)

---

I’m not going to pretend that I completely grasp all this yet, I need to work with it a lot more first. But this is what I do know: **we need to design our layouts with code**. Organizations stuck with older workflows are going to be missing out on so much potential for how their UI layouts could work.

I love the editorial layout examples with awesome graphic design on [labs.jensimmons.com](https://labs.jensimmons.com/) – but the potential I’m excited about, is how to leverage the intristic for content rich application UIs. At work, we have dense layouts and users with large screens, but we’re still not using screen real estate efficiently enough – these are problems we can tackle with better ways to contract and expand.

This strengthens my resolve that no matter how well a designer and a developer collaborates, I just don’t buy that you can do this as separated skill sets and separated tasks. My brain can’t envision squishiness if design work happens by drawing containers in a graphic program where the boxes don’t shrink or grow. The thinking of has to happen in code.
