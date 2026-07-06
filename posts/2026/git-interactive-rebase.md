---
layout: post
title: "A Guide for Git Interactive Rebase"
date: 2026-07-03
---

No prior experience with interactive rebasing — and not sure why you’d ever want to? <br>Excellent! You have come to the right place. I wrote this guide for you.

## The problem 😵‍💫

My branch is a mess of commits. While working on this change, I accidentally deleted the wrong file, added that file back again, tested and iterated, whoops forgot to rename a variable in a test that broke the build, and finally remembered to update the readme. It’s perfectly fine that these five commits were part of my process — but there is absolutely no good reason to preserve this mess.

## The lazy squash-and-merge 🤷🏻

Any reviewer of the PR will just have to ignore the mess, and I will sweep it under the rug with a squash when I merge. Cause that makes the mess go away, right?! Well… if I am not going to clean up the commits on this branch, the absolute least I can do is to make sure that I select [squash and merge]({{ '/2022/03/merge-button/'  | url }}). The next bare minimum is to [not forget the silent step](https://thoughtbot.com/blog/don-t-forget-the-silent-step-when-you-squash-and-merge) (that will otherwise dump the five commit messages into the squash) before hitting **Confirm squash and merge**. Either way, I hope any reviewer will not care, and hopefully nobody will want to investigate the history of this change in the future.

However! I have more Git tricks up my sleeve and can do better than a lazy squash-and-merge. I know how to clean up a messy branch and since I’ve gained some practice, these steps have become a natural part of my workflow. Won’t you join me…?

## Interactive rebase 😎

My strongly recommended prerequisite for this Git operation is to have a Git editor you know how to use. Here’s my guide for how to [Give Yourself A Git Editor To Live With]({{ '/2023/10/git-editor/' | url }}).

```
# Check the log, was it five commits I want to clean up?
git log -5
```

Yes, that looks correct. Okay, lets roll up our sleeves.

```
# Make a list of the 5 commits about to be rebased
git rebase --interactive HEAD~5
```

My Git editor will now show me a list like this:

```
pick 2dcd477 Add awesome feature
pick 2a76135 ops dont delete important.js
pick 69cf371 wip iterations
pick a999fe0 whoops rename variable in test
pick c7f3e47 remember readme update
```

In the editor, I can now use commands like this one:

```
s, squash <commit> = use commit, but meld into previous commit
```

I want to meld the 4 last commits into the first.<br>
I can do that by replacing pick with `s` for squash like this:

```
pick 2dcd477 Add awesome feature
s 2a76135 ops dont delete important.js
s 69cf371 wip iterations
s a999fe0 whoops rename variable in test
s c7f3e47 remember readme update
```

After saving / writing that, the next step is the commit message(s). <br>The list in my editor now looks like this:

```
# This is a combination of 5 commits.
# This is the 1st commit message:

Add awesome feature

# This is the commit message #2:

ops dont delete important.js

# This is the commit message #3:

wip iterations

# This is the commit message #4:

whoops rename variable in test

# This is the commit message #5:

remember readme update
```

Note the instructions:

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
```

So what I will do in this specific case, is add `#` in front of the scraps of commit messages for 2,3,4,5 to comment those lines out. This will leave me with `Add awesome feature` and probably I will now make sure to [write some context to that commit message]({{ '/2024/kontekst-i-commit-melding/' }}) (but that is a topic for a different blog post).

After saving / writing the commit message, I want to verify that my rebase happened as intended.

```
# Check the log, are my 5 commits now cleaned up to be 1
git log -2
```

Looking good! The second commit is now something else on the main branch. 🎉

If this is a branch I have previously pushed to remote, I’m gonna need to use force to update it:

```
# Use the force but safety options
git push --force-with-lease --force-if-includes
```

I have cleaned up the mess, and ready to change the PR status from **draft** to **ready for review**.

---

This was just one example with a basic clean up. Practice a couple of times! That will make this operation something that feels natural, and also easier to start looking into other commands like these:

- `r, reword` will use commit, but edit the commit message
- `f, fixup` like "squash" but keep only the previous log message
- `d, drop` to remove commit

It’s also possible to reorder the commits just by moving them around. Have fun!

---

Repost of a text I originally wrote in 2024 for our work blog [Jotter](https://amedia.github.io/jotter/2024/git-interactive-rebase/)
