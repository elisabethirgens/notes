---
layout: post
title:  "git diff master"
date:   2017-06-08 20:30:00 +0200
categories: git
---

`git diff` was probably one of the first 10 terminal commands I ever learnt. I use it a lot for quick comparisons of a few lines, but didn’t get a habit of diff-ing more when I need it the most.

Last week I learnt `git diff master` 🙏 and very quickly experienced how helpful this is when messing around with code changes in multiple commits on several branches over time. Puh.

I know that there will always and forever be concepts and commands to learn that I wish I had learnt before. I try to accept that. But this was downright annoying, because gah… it would have been so useful to grasp some of this somewhat earlier.

## What I’ve been confused about
* what is compared when
* the mental model I had of local branches was a bit off
* something about branches and unstaged changes

## What I understand better now
* unstaged changes do not live on any branch (only commits do)
* my editor will show me one version of the code at a time — but I can use the terminal more actively in my workflow to compare lots of different code changes
* and this doesn’t require as advanced commands as I previously thought

---

## `git diff`
* compares unstaged changes **with the last commit** on the current branch

## `git diff master`
* compares both **commits on the current branch** and **unstaged changes**
with master


---

**Note to self** — Writing is awesome because attempting to write this post gets most of the credit for levelling up and actually understanding this properly. 🏆
