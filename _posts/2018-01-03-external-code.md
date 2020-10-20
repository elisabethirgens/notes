---
layout: post
title:  "Deal with external code"
date:   2018-01-03 20:00:00 +0200
---

I’ve had to think more about managing external code lately. There’s always been plenty of it in systems I work on, but often just directories I didn’t necessarily do much with. That changed now, and I had some helpful discussions with coworkers along the way. Let’s write up what I learnt!

## What is *our* code…?
A while back, I asked why we split assets into e.g. `js` and `js-external`. I was discovering examples where this type of separation was well intentioned once upon a time — but now a lie. “In&nbsp;which way is this useful? Isn’t it all ‘our code’ the moment we put it in *our codebase*?”

## Separate code we don’t maintain
The answer I got, was a good explanation about the difference in **using vs maintaining code**. We&nbsp;use frameworks, libraries and plugins that we have absolutely no interest in maintaining. A-ha.&nbsp;This is of course a problem that package managers solve. Which I am familiar with from working with our newer apps, but didn’t quite connect with what I was finding in older apps.

## Never change — always update
The benefits of separating clearly also became very evident for me when working on security updates of jQuery and misc related plugins. X, Y and Z were once used to solve a problem. Maybe that’s not how we’d solve it today, but… priorities! Easily identifiable directories and separated code makes it possible to update often and quickly without loosing any “custom tweaks” we’ve previously hacked. (This concept was very familiar when I suddenly remembered how it’s what I did when building WordPress child themes; to enable updating of the parent theme.)

## It’s perfectly okay to override styles
The problem, and probably main motivation behind my original questioning of this, was wanting to restyle something. For example when using a datepicker; we don’t want to maintain any of the JavaScript, but we do want to make some changes to the default CSS.

This is when a cute lil’ `datepicker-override.css` in a different directory makes it clear what we maintain. Now I see how this is actively using specificity for good. It’s not like the specificity wars will start raging again next week, just because I write a handful of two class selectors.

## Challenge my previously learnt best practices
My purist frontend training squirms at overriding styles like this, but it is exactly what to do when working on a large system with (over time) ~100 other developers. I’m understanding more and more that parts of what I’ve learnt before, originates from a different world, one without legacy code. Best practices change when systems and teams get larger, and when we won’t always be well acquainted with all nooks and crannies of the systems we work on.
