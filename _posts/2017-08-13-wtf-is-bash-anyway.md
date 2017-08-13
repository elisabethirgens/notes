---
layout: post
title:  "wtf is bash anyway?!"
date:   2017-08-13 20:00:00 +0200
categories: learning
---

Bash. This word keeps popping up, without me having more than an extremly shallow understanding of what it means and why I should care. So let’s fix that by writing notes. ✨

I know it’s related to what I do in my terminal, and Wikipedia can tell me that:

> Bash is a Unix shell and command language

But… what exactly is a Unix shell…? 🤔

> a command-line interpreter or shell that provides a traditional Unix-like command line user interface.

Are you kidding, Wikipedia? How was that a helpful first line to introduce what [Unix shell](https://en.wikipedia.org/wiki/Unix_shell) is… 😠 “Traditional?!” Anyway, the next sentence is more comprehensible:

> Users direct the operation of the computer by entering commands as text for a command line interpreter to execute, or by creating text scripts…

A-ha. The general article on [shell](https://en.wikipedia.org/wiki/Shell_(computing)) is a lot friendlier, and it explains nicely that it’s a user interface for access to the operating system by either:
* a command-line interface (CLI)
* or graphical user interface (GUI)

Makes sense! 👌 And I’m reading how it’s called a shell because it is a layer around the kernel. Cool. Back to [the article on bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). The history is interesting, but the rest quickly becomes more specific than I’m interested in now. I search for *bash introduction* and find an abundance of sites created by people who seem to be very afraid of CSS. They are also obviously written as introductions for *other people* than me, because they make me want to **not** learn about bash.


But oh wait-a-minute… 👉 [The Bash Guide’s inception](http://guide.bash.academy/inception/) looks perfect for me:

> Bash is a shell program designed to listen to my commands and do what I tell it to.

> Bash is a simple tool in a vast toolbox of programs that lets me interact with my system using a text-based interface.

> The bash shell is a binary program that runs either interactively or non-interactively, usually in a text-based interface provided by a terminal emulator program.

This is great. It assumes nothing and explains everything. And I’m already feeling smart because they also repeat stuff I already understand: Input! Output! How I can run programs that start, communicate and end. Cool! But before I dive into reading about [Commands And Arguments](http://guide.bash.academy/commands/), I&nbsp;want to learn about configuration — because I keep having to deal with that at work.

I know I have some dotfiles for bash, but I have little clue what we’ve put in them or why there are several different files. Let’s see…

## `.bashrc `
This file is a script that runs every time I start a a new terminal session. Something something “when ever bash is started interactively” …hm, okay?! Not quite sure what that means, but it sounds like this is the file that’s most relevant for me to use for configuration most of the time.

## `.bash_profile`
This runs only at the start of a new login. Apparently it’s mostly historical reasons why there is a difference?! It doesn’t sound like I need to spend too much time on learning about that.

## `.bash_aliases`
Hey, this file is easy enough to understand — because I use several of these aliases all the time. I&nbsp;just didn’t realize before now, that this is where they are defined. 😆

---

There’s plenty more to figure out! But this will do nicely for now. The sun has set (quite literally, it’s getting cold out here) and my drink is empty, so… 👋
