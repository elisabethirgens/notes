---
layout: post
title: "Adventures in Upgrading to Python3"
date: 2018-07-13
---

Wo-hooo. Deploy scripts at work have been upgraded to Python3. I know this will break the deploy of the design system I work on, and I also need to figure out how to get my machine up to speed.

## First attempt at using upgraded deploy scripts

When I run a deploy command in a project, the script will check if there have been changes to the it’s own repo and update. This happens often, so I know this drill.

```bash
Updates successfully applied.
Please re-run script to deploy with newest version
```

This makes sure all developers always use the latest version of the deploy scripts. So far so good.

```bash
This program requires python3, but was unable to
find a python3 on your system.
```

A-ha. This work machine doesn’t actually have Python3 installed at all. (And now I realize I should get the upgraded deploy scripts working on one of the projects using our standard setup before the slightly different one on the design system.)

## Start with understanding current Python installs

```bash
python --version
Python 2.7.13
```

(I thought this was the version that comes with Mac OS, but realise later that it’s not.) Mac OS installs an older Python with the system, which is why [LPTHW]({{ '/2017/12/python/' | url }}) got me to install Python3. (But that my not-work machine.) The book recommended installing from python.org directly. I’m always confused when getting different recommentations like this. What are the pros and cons of installing like that vs using Homebrew? One thing I can think of, is that the usage and target groups are very different.

- The book needs to not complicate the setup for its users.
- But developers in our dept need to deal with brew anyway.

Also versions and upgrading later:

- The books would want to make sure readers use the exact same version all the time.
- But at work we’re maybe going to need minor upgrades all the time?

And where will brew install Python? Do I need to know?<br>
Reading more about [docs.brew.sh/Homebrew-and-Python](https://docs.brew.sh/Homebrew-and-Python)

## 🤔

When onboarding a new co-worker recently, I remember that we found there was something weird and outdated about the setup on my machine. “If it’s working, don’t touch it” was the advice then.

```bash
which python
/usr/local/opt/python/libexec/bin/python
```

But now I’m wondering if I should remove this before installing Python3? Does it matter? Will it break something?

```bash
# make bash find the python that brew installed
export PATH="/usr/local/opt/python/libexec/bin:$PATH"
```

💡 **Pro newbie bash tip:** when people tell you what to put in your dotfiles, insist on also getting a comment to go with it. Otherwise you end up with so many snippets and no idea what they do or why you put them there. This must have been one of the times where I did ask for an explanation. Yay.

And this comment must mean that if bash now is able to find the python it needs without this hack, then `.bashrc` doesn’t need this anymore. So I assumed it was a good idea to remove now. And oh, now I got something else. Deleting it will return this instead and _this_ is the system python.

```bash
which python
/usr/bin/python
python --version
Python 2.7.10
```

## Install Python3 on my machine

```bash
brew install python3
Error: python 2.7.13_1 is already installed
To upgrade to 3.7.0, run `brew upgrade python`
```

Hm… This was not as advertised. Do I need to be concerned about brew wanting to upgrade…?

```
which python
/usr/bin/python
which python2
/usr/local/bin/python2
```

```
python --version
Python 2.7.10
python2 --version
Python 2.7.13
```

This must be system python and brew python. I got the impression that I probably won’t need a brew python2, so let’s assume it’s okay to upgrade like this.

I often find the brew docs confusing, but this page is quite helpful: [docs.brew.sh/FAQ](https://docs.brew.sh/FAQ)

- `brew doctor` shows that all is fine
- `brew update` found a couple of things to update
- `brew outdated` ah, this was useful and super informative

```
postgresql (9.5.1, 10.1) < 10.4 [pinned at 10.1]
python (2.7.10_2, 2.7.13_1) < 3.7.0
```

This also answered a question I got about if I had pinned my python. Nope, mysql and postgresql are pinned, but nothing else.

- `brew upgrade` happily upgraded all the things 🎉

Might have been a while since I did that. I get a bit wary of upgrading, should probably just upgrade more. (Recently had problems with running an older `node 9.5.0` instead of `v10.6.0`)

```
==> Upgrading 17 outdated packages, with result:
python 2.7.13_1 -> 3.7.0
```

So now…

```
python --version
Python 2.7.10

python2 --version
-bash: /usr/local/bin/python2: No such file or directory

python3 --version
Python 3.7.0
```

Brew reported a couple of `==> Caveats` I wasn’t sure about, but asked folks on slack and got clear on every single one of those too. Awesome!

---

✅ I’ve got Python3 installed and upgraded scripts work on my machine<br>
✅ I learnt so much about dealing with brew installs<br>
✅ …and how to understand the output from `which` and `version`

It all seems obvious after writing these notes. But it wasn’t at all obvious to me 3 days ago – and now in 3 weeks I can look back and remind myself of the benefits of this rabbit hole.
