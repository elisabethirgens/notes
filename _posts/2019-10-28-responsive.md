---
layout: post
title:  "Responsify A Logistic System"
date:   2019-10-28 15:00:00 +0200
---


Once upon a time, computer screens had a standard resolution of exactly 1024×768&nbsp;pixels. Designers used a photo editing tool to make pretty pictures of websites that were exactly 960&nbsp;pixels wide. They would divide that up in 12 columns, a time-honoured tradition from the world of graphic design on paper. The pixel perfect designs were then tossed over the fence to developers, who were tasked to implement pixel perfect results in a browser.

## A short history of complicated responsive web design
Then smart phones happened, while laptop screens and external monitors kept getting bigger. The community scrambled to figure out how to make our websites work in different viewports. We had learnt how to make fluid grids by coding pixel perfect columns with percentages. We had a formula! Our style sheets were full of calculation comments for every % with 7 decimals. Brave souls even had a brief spell of using JavaScript to change which CSS classes were added to the HTML.

Thank W3C the `@media` at-rule came along and let us write media queries to conditionally apply CSS rules depending on viewport width. Ethan Marcotte coined the [RWD](https://alistapart.com/article/responsive-web-design/) term, and we all tried to understand what John Allsopp wrote in [A Dao of Web Design](https://alistapart.com/article/dao/) to “accept the ebb and flow of things”.

For a while we coded 4 different versions of any layout. We learnt that device specific media queries was perhaps not the best idea, as the device screen resolutions kept changing, bigger and bigger and then omg they made a watch. 😱 We flipped our media queries to be mobile first, and wrote min-width values in `em` units not based on the latest Apple product. Phew.

## But what even is designing for browsers?!

Smart frontend developers kept up. They built super smart grid systems with Sass. But personally I was never that clever and I was pretty lazy, so I didn't keep up. I did something else instead, I moved the goal post for the projects I worked on.

What if… we decide a different responsive strategy? What if the task at hand isn’t to recreate a designers 12 columns? A graphic designer’s goal for layout can be perfect alignment in a 12/16 column grid. If you’re building an editorial art directed browsing experience, perhaps that goal is nice to have. But as a UI developer building a logistic system, with technical UI debt and different legacy design decisions across various parts of the system, a better goal is: to build responsive UIs with as little code as we can get away with. And what if you can ignore the buzz of mobile first, and sell the idea that no matter how much people use their phones, we shouldn’t get lost in mobile optimization as a way of making things complicated. 98% of users were on desktop, it made more sense to focus on improving the experience on wider screens than on mobile.

The goal defined for this logistics system was: responsive-ish, app by app, over time.

## We skipped the scrambling RWD years

Because the community had done the scrambling already, because we were late thinking about responsive. And because I was lazy, we could skip past the complicated techniques.

The technical UI debt included a header with a complex navigation that had grown and grown. The foundation of the CSS used the font-size 62.5% technique. Dating from 2004, it was a nifty trick so that you could translate a designers 10 px to 1 em and the layout wouldn’t break if uses increased the text in their browser. But all this made it difficult to move forward. I built a duplicate header with navigation, using modern CSS as a foundation and as little of it as possible.

## The minimalist strategy worked 💁🏻‍

After most applications used the new version of the header, it was possible to change the navigation and the 1000 px straitjacket could be lifted. The newer UIs were magically full width over night (because we had focused on creating responsive layouts also within the 1000px limit). The design system I built had [Tachyons](https://tachyons.io/) style utility classes, but even way more simplified. No screen width modifiers for spacing classes, just one additional modifier for the percent widths. It was visually crude, but also efficient in making it easy for newbie coding UXers and backend developers alike to create layouts that were responsive enough.


## What was left behind 🚫
- Kilometres of CSS attempting to brand the UI (styled checkboxes, webfonts +++)
- The 62.5% technique as a base atomic unit or all the other sizes
- Spacing units originating from Photoshop (5px, 10px, 20px)
- Canvas in (start with boxes, then fill them with stuff)
- The idea that design can done, completed and perfect

## What was embraced ✅
- Writing as little CSS as we can get away with (so much cheaper!!)
- Default browser font size 100% as a base atomic unit for all the other sizes
- Spacing units originating from the browser (0.25rem, 0.5rem, 1rem)
- Content out (start with the stuff, then create a layout)
- The idea that design can be continuous incremental improvements

## What we won 🏆

I’m really pleased that I didn’t leave behind a rigid and fragile system of 4 different layouts. I can imagine this working fine enough for other projects, but it would have been a nightmare for these teams working on these applications in this system to have to deal with that. What we have instead is just one single weird value in the media query at `62.5 em` that lives on as legacy from the 1000 px straightjacket. I’m not sure it even counts as technical debt, because it does no harm.

The huge victory of this responsive strategy: **the possibility to work incrementally** across this logistics system of ~25 different applications of varying age that output UI.

Some apps are top notch responsive, others half way there. One of the largest frontends are yet to be modernised and is due for this soon. Now they have a clean slate to approach that, without being weighed down with a responsive strategy of 4 media queries chosen 3 years ago.

## Intrinsic Web Design

Jen Simmons has introduced a new era of design for the web, and I’m starting to think it has less to do with CSS Grid specifically than I’ve thought before. Comparing my previous notes [Say Hello to Intrinsic Web Design]({{ site.baseurl }}/2018/06/intrinsic_web_design/) with the strategy I defined for the logistics system, perhaps the most important aspect is:

* media queries only if and when needed
* design a flexibility model for the content

---

_(This was WIP drafts of separate articles, that are never going to be finished, ended up being dumped into these notes. Probably lacking context, but makes sense for me…)_
