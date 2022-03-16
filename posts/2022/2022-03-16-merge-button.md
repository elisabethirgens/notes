---
layout: post
title: "Merge Button Surprise"
date: 2022-03-16
---

It’s not every day I learn something new about a button I have pressed 1001 times. But turns out that the merge button on pull requests in the GitHub user interface behaves a tiny bit different than I thought.

## There is no default

Why does the button default to **squash and merge** in work project A, and default to **Merge pull request** in work project B? I was surprised to find there’s not a default in the way I thought.

- I know the git involved in branching, committing, merging, squashing and rebasing all just fine
- I was aware the merge button on GitHub has an option for me to select between different merge methods. I’ve been making PRs in GitHub since before that feature was there, and the button functionality was expanded in April 2016 to support [squashing](https://github.blog/2016-04-01-squash-your-commits/) and later the same year also [rebase](https://github.blog/2016-09-26-rebase-and-merge-pull-requests/)
- But what I misunderstood: how repo settings affect the behavior of the button

I thought there was a setting for a preferred merge method that someone has defined for this repo. That misunderstanding has influenced my behavior, I thought I was being respectful of a setting in the project, by _not_ making my own intentional choice of merge method when I merge my PRs. Kinda like “oh someone has discussed tabs vs spaces and also squash commit vs merge commit, I don’t need to be the new dev on the team who resurfaces that discussion”.

Now I know I get the button of the merge method I previously used in this project. It's more of a personal default for my user — within the permitted merge methods in the settings.

## GitHub supports 3 different merge methods

- Create a merge commit
- Squash and merge
- Rebase and merge

## How the repo settings actually work

- Settings can check or uncheck which merge methods are allowed
- There is not a setting for a default or preferred method
- The button changes depending on what I have previously selected in the same repo

## I see more squashing in my future

Hm. Could one reason why I didn’t catch this before, be that I used to work with a deploy pipeline that actually required a merge commit?! 🤔 Sometimes I wish it was possible to travel back in time to previous jobs just to poke around the code base and systems to take a look with my current understanding of things. Anyway: there will be way more squash and merge from me moving forward. 💥

And I will even remember the silent step:

> But too often, I find that people who use that button tend to miss the middle step (I might even call it the silent step) between squashing and merging. They usually click “Squash and merge” and then immediately hit “Confirm squash and merge”, In doing so, they forget to write a good cohesive commit message!

— [Don't forget the silent step when you squash and merge ](https://thoughtbot.com/blog/don-t-forget-the-silent-step-when-you-squash-and-merge)
