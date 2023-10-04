---
layout: post
title: "Give Yourself A Git Editor To Live With"
date: 2023-10-02
---

A common hurdle to learning Git operations like interactive rebase, or writing great commit messages with documentation, is a small setting that chooses an editor for Git. I used basic `git` from the terminal for years without ever doing anything that required Git to open an editor. But the day you aim to level up with running certain types of Git commands — it’s super helpful to first make sure you understand which editor you have told Git use.

Preferably an editor that you, the human at the keyboard, also want to use. Let’s sort this out:

## Have I configured my Git editor?

```sh
# List all variables set in my config file
git config --list
```

- If there IS a `core.editor` in the output, it’s value shows what I have configured
- If there IS NOT a `core.editor` in that list, it means I have not explicitly configured this and the bad news is that the default will be the shell editor (most likely `vim` 😭) but the good news is that I can change this to an editor I actually know how to use 👇

## Open my .gitconfig file

This `git config` command takes many options, and most guides on configuring Git will suggest using those commands. What I don’t like about running these, is how it obfuscates what they’re actually meddling with on my computer. I prefer to understand that I have a `.gitconfig` file, where it is (probably my home directory, unless I have saved it somewhere else) and how to open it, and frequently take a proper look so I can intentionally edit everything in there.

```
# A typical .gitconfig might contain something like this

[user]
    name = Elisabeth
    email = ########

[core]
    editor = code --wait
```

That last line will configure Git to use `code` aka [VS&nbsp;Code](https://en.wikipedia.org/wiki/Visual_Studio_Code) when it needs to open an editor.

If you are a person who already uses Visual Studio Code all day long, and don’t want to fumble around with a different editor, this setting can be great. The `--wait` makes sure Git knows to wait until any file editing is done and you have closed the file. Note that if you are using iTerm2 or another separate terminal, a prerequisite for using `code` is that you can run `code --version` and get a version. If you get `command not found` you need to look up instructions for how to [add VS&nbsp;Code to path](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).

## Take my Git editor for a spin

```sh
# Trigger git to open an editor to modify my previous commit
git commit --amend
```

## Try different Git editors

After you know how to configure your Git editor, try out different editors and see which one best fits your workflow. I use iTerm2 and found I prefer my Git editor to also be inside the same shell:

```
[core]
    editor = nano --wait
```

I don‘t know all of [nano's shortcuts](https://www.nano-editor.org/dist/latest/cheatsheet.html) but I do need this little dance to write my commit message:<br>
<kbd>Ctrl+O</kbd> to WriteOut, followed by <kbd>Enter</kbd>, and then exit with <kbd>Ctrl+X</kbd>

GitHub Docs has more suggestions in [Associating text editors with Git](https://docs.github.com/en/get-started/getting-started-with-git/associating-text-editors-with-git)

## More commands to try out

```sh
# Show variabel for editor (if it exists)
git config --get core.editor
```

Yes, I could have started off with this command, but then we wouldn’t have gotten a peek at the full list of Git configurations — and more importantly, this direct one line check is seriously unhelpful when it returns nothing. Because ‘nothing’ is easy to miss and in this case ‘nothing’ represents the bad news that `vim` is the default you perhaps didn’t know you had and don’t know how to quit.

## A postlude for exiting vim

The first time I got stuck in vim, I probably had a grand total of 7&nbsp;commands in my tool belt and no clue why my terminal changed away from the behaviour I knew. But I had been hanging out with developers long enough to be familiar with programmer memes, and so it was that [those jokes](https://programmerhumor.io/linux-memes/me-too-friend-me-too-2/) about [exiting vim](https://thenewstack.io/how-do-you-exit-vim-a-newbie-question-turned-tech-meme/) made me understand that “oooh wait-a-minute, _this_ must be what being ‘stuck in vim’ is all about” 😆 and suddenly [the jokes](https://programmerhumor.io/linux-memes/vim-2/) made sense — but also I understood that I could literally search for “how to exit vim” to get myself unstuck and back to the Git operation.
