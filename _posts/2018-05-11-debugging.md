---
layout: post
title:  "Debug the Missing CSS Analysis (Hey Jenkins!)"
date: 2018-05-11
---

When I make pull requests to our design system, we have set up automatic comments on GitHub with CSS analysis. They went missing recently, so let’s debug! I dug a bit on my own, asked for help, learnt a boatload — and forced myself to write out these notes afterwards to learn even more.

## Parker 📊

This is a really neat [stylesheet analysis tool](https://github.com/katiefenn/parker/) — built by Katie Fenn — that I have installed on my machine. I can run it on local files, or remote using curl:

```
curl http://www.katiefenn.co.uk/css/shuttle.css -s | parker -s
```

Our project has a Python script that runs Parker using `$(npm bin)/parker` “as the parker executable” according to a code comment at the top. I have no idea what that means, but found something that looks like it might be relevant… `nargs` ?! 🤔 Sooo… hm… apparently that is [a&nbsp;parameter](https://docs.python.org/3/library/argparse.html#the-add-argument-method) to define the number of arguments, but this is the key part:

`argparse` is a module for getting a script to run bash commands. Found an [Argparse Tutorial](https://docs.python.org/3.6/howto/argparse.html) and will save reading that for later. But I understand now that our script can run this tool because;

Parker is an [npm module](https://www.npmjs.com/package/parker) and we’ve got it included in the `package.json`:

```
  "devDependencies": {
    "parker": "^0.0.10",
  }
```

Cool! I can now see Parker in `node_modules` and have understood this part of the setup. Thanks to my previous efforts to [Understand Better How to 'npm'](https://elisabethirgens.github.io/notes/2018/02/npm/) 👌

## Jenkins 👋

Hey, hi! Oh yes, we run into each other in the hallway and nod all the time, but I don’t _really_ know you very well. Let us sit down and get better acquainted: [jenkins.io/doc](https://jenkins.io/doc/)

* Open source automation server written in Java 🌎
* Can automate tasks related to building, testing, and deploying software 🚀
* The main feature is Jenkins Pipeline 🔧

> A continuous delivery pipeline is an automated expression of your process for getting software from version control right through to your users and customers.

## Jenkinsfile 👀

Digging around different repos in our GitHub organization, I can see that most of our apps share a function coming from a workflow library. But the design system isn’t a Java app, so it looks different. And starts with `node`. I read in the Jenkins docs that I can create pipelines with different languages, including Node.js but ha! I know enough about our architecture to understand that this node must be something completely different. Here we go, a [glossary](https://jenkins.io/doc/book/glossary/) that says:

> Node: A machine which is part of the Jenkins environment and capable of executing Pipelines or Projects. Both the Master and Agents are considered to be Nodes.

Soooo… what language exactly is this Jenkinsfile?

## Groovy 🕺

The [Groovy language docs](http://docs.groovy-lang.org/) seem nice when you already know what you need, but I found an explanation on Wikipedia that was enlightening:

> Most valid Java files are also valid Groovy files. Although the two languages are similar, Groovy code can be more compact, because it doesn’t need all the elements Java needs.

All right, now that I know which language I’m looking at, I can add [Groovy support in Atom](https://atom.io/packages/language-groovy) and get syntax highlighting for this Jenkinsfile.

## Back to the debugging 🕵️‍♀️

Thanks to co-workers’ useful PR descriptions, and figuring out _when_ the Parker comments went missing, I had a specific code line as a suspect and it contained:

```
script: 'git log --grep="[release]" -1 --format="%H"'
```


## grep and regex 🔍

Regular expressions was one of those things I knew existed thanks to [xkcd](https://xkcd.com/208/). Now I know a bit more than just how it’s “apparently something awesome”, but let’s make note of a definition and links:

> grep is a command-line utility for searching plain-text data sets for lines that match a regular expression

* [wikipedia.org/wiki/Regular_expression](https://en.wikipedia.org/wiki/Regular_expression)
* [Regex Accelerated Course and Cheat Sheet](http://www.rexegg.com/regex-quickstart.html#ref)

##  The fix and the commit message 🐛

```
                          👇          👇
script: 'git log --grep="\\\\[release\\\\]" -1 --format="%H"'

Fix regex bug to bring back Parker PR comments

The jenkinsfile would grep for letters r e l e a s e individually,
which is the case in most commit messages of a certain length, then
compare the latest commit to itself, find no css changes and skip the
parker-analysis script. Escaping will make the git log grep run as
intended, and oh yeah: we need escaping for both groovy and regex.
```

I got a lot of help from a co-worker to figure that out, and learnt how to:

* Comment out parts of the Python script so we could run it locally and test the output.
* Read the script and understand what it does, including a deep dive into git and [detached head](https://www.atlassian.com/git/tutorials/using-branches/git-checkout).
* Replay! This will let me modify the Jenkinsfile and run the pipeline again to test the change.

---

Wohooo! Now the design system pull requests get comments again with stats on the CSS, helping us to keep the quantity low and quality high.
