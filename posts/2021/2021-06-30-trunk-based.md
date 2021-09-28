---
layout: post
title: "Speed Up With Trunk-Based Development"
date: 2021-06-30
---

Discussing how to do git branching on your team? [DevOps research](https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development) has identified trunk-based as one of the technical capabilites for delivering software with speed and stability. Paul Hammant has collected everything I ever wanted to know about this branching model on [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/)

## Commit Straight To Trunk? 🧐

The original style of trunk-based. Fascinating to read how ~20 years ago [up to 100 committers](https://trunkbaseddevelopment.com/committing-straight-to-the-trunk/) could be sharing the same trunk and how they would deal with check-ins, reverts and broken builds. This was before git and lightweight branching, and fewer opt for this variant to boost productivity today. 

## Short-Lived Feature Branches! 😍

This is the way! I have seen what it looks like to work with a pipeline rigged for trunk-based, and how teams focused on it, will get better and better at [working in small batches](https://cloud.google.com/architecture/devops/devops-process-working-in-small-batches).

> One key rule is the length of life of the branch before it gets merged and deleted. Simply put, the branch should only last a couple of days. Any longer than two days, and there is a risk of the branch becoming a long-lived feature branch (the antithesis of trunk-based development).

> If there is more that one developer (and the developer’s pairing partner) on the same short&#8209;lived feature branch, then that branch is at risk of not being short-lived. It is at risk of being more and more like a release branch under active development, and not short at all. There is a risk too, that a developer may choose to pull changes to their workstation from a short-lived feature branch rather from the trunk.

Check out this [flow chart](https://trunkbaseddevelopment.com/styles/) that explains those two styles, along with a third called Coupled “Patch Review” System — which is described as suitable for up to 40000 committers. Way out of my league, but certainly interesting to know that Google has been practicing trunk-based in a single repo.

## Measure the effectiveness 📈

If developers work on the same feature branch for weeks, require code freezes and fret merging — there is work to do on improving speed. Factors to test and what to measure from the [DevOps research:](https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development)

- Three or fewer active branches
- Frequency of merging
- Time to approve code changes

## Local build is important

> In all variants of Trunk-Based Development teams run the full build locally (compile, unit tests, a range of integration tests) and see that pass, before declaring ‘done’ and committing/pushing the work to the eyes of teammates and bots (code review / pull-request)

## Release from trunk

The page on [alternative branching models](https://trunkbaseddevelopment.com/alternative-branching-models/) describes that the model branded by GitHub is close to trunk-based — but the difference being where the release is made. [GitHub Flow](https://guides.github.com/introduction/flow/) (not to be confused with GitFlow) describes a deploying from a branch for testing in production, before merging to main. Trunk-based argues that:

> One problem with this is the small risk of regression in the following release - that would be if the release goes out, but the branch is never merged back. Another is that it may indeed not have items in it from the trunk that were part of a previous release (causing a regression).

---

This [history lesson](https://trunkbaseddevelopment.com/game-changers/) of trunk-based since the 80s was fun to read, learning where different practices come from in time, is sometimes what makes it easier to understand the complete picture.

I have recently discovered that when having discussions about branching, it helps if there is no mix-up around terms like [GitOps and GitFlow and GitHub Flow]({{ '/2021/06/gitops/' | url }}) — and that we know a word like trunk can mean _different_ things. Wikipedia describes that a trunk can contain "the most unstable version". Who knew?! That's not the trunk I mean when I want to simplify our branching. 😆

