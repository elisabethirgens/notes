---
layout: post
title:  "Rebase! I totally git it now."
date: 2017-06-18
---

Both merge and rebase are commands I’ve used plenty, and read about a lot, without managing to wrap my head around wtf actually happens. But this week all became clear. 💪 It’s kinda ironic how tutorials with diagrams make sense first *after* you already understand something.

I leveled up now after asking someone to talk me through it. We had pen & paper — and a repo with multiple collaborators, but straightforward changes. This exercise helped identify what I was confused about in a way self study can’t. My git experience has mostly revolved around:

* working alone, often with a rather linear progress
* or collaborating, but with our changes on separate sets of files
* occasional merge conflicts, but that are easy to resolve

So I haven’t needed to understand this before: how does git magically handle so much complexity in a pull request, when it chokes on much simpler changes in a push to master?! And how do some people end up with messy merge conflicts that others seem to avoid?

We found out that I had not quite understood how commits relate to history. Now I know that every single commit always has a parent commit. Only the initial commit has no parent. And just like that, reading about fast-forward makes sooo much more sense.

---

## `git merge`
* does not rewrite history
* requires merge commits that point to more than one parent

## `git rebase`
* will rewrite history so use with care 👌
* moves a branch from one parent commit to a different parent commit
* I can use this to clean up local changes

---

**Note to self** — Concept that is hard to grasp? Discuss with people who understand them! Read&nbsp;up first to get a foundation, then ask for help when stuck. 🙏
