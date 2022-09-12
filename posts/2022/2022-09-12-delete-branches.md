---
layout: post
title: "Delete All Local Branches"
date: 2022-09-12
---

Most of the time I habitually delete branches after I am done with them, so I don’t need to wonder if there’s any useful work lurking on them. But occasionally they pile up, and then I delete them one by one, while cursing that _yeah there is of course a better way to do this, but not right now…_ Well, one fine day this summer, I finally invested a handful of minutes to find that yay — let’s use this next time:

```shell
# Delete all local branches that are fully merged
git branch | grep --invert-match "main" | xargs git branch -d
```

Deconstructed this command will:

- `git branch` to list existing branches
- `|` is a pipe that takes the result from the command on it’s left and sends that into what ever comes on the right hand side of the pipe
- `grep --invert-match "main-"` to find branch names not matching ‘main’
- another pipe `|` so any and all branches not matching ‘main’ are piped into the next command
- `xargs` to repeat what comes next for each output
- `git branch -d` to ‘delete fully merged branch’

And if I’m absolutely certain I have no local commits I want to keep, I can replace the `-d` with `-D`:

```
-d, --delete          delete fully merged branch
-D                    delete branch (even if not merged)
```
