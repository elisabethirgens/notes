---
layout: post
title:  "Set up my new Macbook"
date:   2017-09-24 21:00:00 +0200
---

I have a brand new MacBook (wohooo!) and it’s been quite some time since I set up a new laptop. I want to do everything from scratch, and with an understanding of what I’m installing and why. No more blindly copy/pasting commands I don’t know what do. I’ve done that enough the past 3-4 years, and it’s time I learn what’s what. Let’s go!

---

## 🌱 Get started
Unwrap. Turn on. Go through the basic set up. Start installing applications. These are the ones I’ll start with. There will be others, but that can happen when the need for them arises.

### Applications to grab right away
* 1password
* Alfred
* Atom
* Dropbox
* iAWriter
* iTerm2
* RescueTime
* Slack
* Soulver
* Spotify
* Things

### Browsers to make a nice dock
* Firefox, Firefox Developer Edition, Chrome, Chrome Canary, Opera, Vivaldi

### Good to know about this MacBook
* macOS Sierra 10.12
* Display 12-inch (2304 x 1440)
* 500 GB Flash Storage

---

## 🔨 Highlights from the onboarding guide
We have an onboarding guide at work, and going through this again now should be interesting. It’s been 2 years since we set up my work laptop, I didn’t understand any of it at the time. So this is a good opportunity to learn properly how I to turn a regular Mac into a developer’s Mac.

### Something something Xcode, huh!?

> Open Terminal and enter the following command:

```bash
xcode-select --install
```

Well, this can be improved. The way it’s phrased now, it’s training me — as the very first thing to do as a developer on this team — to blindly paste a command without knowing what it does.

What is Xcode and why do I want it?

* Xcode is an integrated development environment.
* An IDE “provides comprehensive facilities for software development” says [Wikipedia](https://en.wikipedia.org/wiki/Integrated_development_environment).
* “…normally consists of a source code editor, build automation tools and a debugger.”
* Other examples are Visual Studio, IntelliJ, Eclipse.

But… wait-a-minute. It seems that it’s not actually Xcode we’re after. `xcode-select` refers to something else and it’s surprisingly difficult to find anything updated about it. But after some digging, I found [a RailsApps project tutorial](http://railsapps.github.io/xcode-command-line-tools.html) that does a decent job of explaining more:

> You don’t need the full Xcode package to get the Xcode Command Line Tools. You only need the full Xcode package if you are doing development of applications for the Apple operating systems.
> MacOS Sierra will alert you when you enter a command in the terminal that requires Xcode Command Line Tools.

### Xcode Command Line Tools

I now haz them. 👌 And as a bonus, I have learnt that the purpose of that command, was to install a toolkit to let me use commands like: `git`.

I can check if I have them installed and print path of the directory:

```bash
$ xcode-select -p
/Library/Developer/CommandLineTools
```

I now have 114 files (binaries?) in this directory:

```
/Library/Developer/CommandLineTools/usr/bin/
```

Cool. I can see git in there. But it’s also basically the only thing I recognize, so I wonder if I could/should have installed git some other way…? 🤔

> There are several ways to install Git on a Mac. The easiest is probably to install the Xcode Command Line Tools.

That is what [git-scm.com](https://git-scm.com/book/id/v2/Getting-Started-Installing-Git) recommends. Okay, good to know. 👍 Also noted that the [GitHub for Mac](https://desktop.github.com/) install is an option, if helping someone get started with git.

### SSH keys

Yay. This was fun to see again. It was not long ago that I had problems with the passphrase, my co-workers tried to be helpful by slacking me [GitHub’s guide for setting your SSH keys](https://help.github.com/articles/connecting-to-github-with-ssh/) and it didn’t really help at all, because I didn’t really know what SSH keys were, and wasn’t able to get anything from trying to read the guides… But now I do! ✨

Setting them up went well, also understanding what I was doing.

### Homebrew

I know this is a package manager I want, but it’s worth remembering that it
was not long ago that I learnt that. The suggested command to install Homebrew:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
```

And my attempts at understanding it:

* the url is to a script (not the actual file as I originally thought)
* this script will check a bunch of stuff for me and install Homebrew
* looks like it also checks for `xcode-select`
* I know that curl has something to do with transferring data
* Ooo, awesome; now I can see that `curl` is one of the binaries I installed as those Xcode Command Line Tools.

Okay, that last part of the command is clear enough for now.

* the first part is apparently a ruby command
* the `-e` is a flag that will run the script, or something along those lines?!
* I don’t understand what the `/usr/bin/` part does as part of the command, and this is different from what is suggested in our onboarding guide. But that is old and this is new, so let’s go with the official suggestion.

> Installation successful! 🎉

And I’m taking note about how the script installs Homebrew to `/usr/local` now. (That was one of the things that tripped me up in my recent [adventures in upgrading Yarn]({{ site.baseurl }}/2017/08/yarn-upgrade-adventures/).)

---

## ✏️ Jekyll

These notes run on Jekyll, so let’s get that set up, so I can publish this post.

* Ruby 2.0 came with macOS Sierra, but I need a newer version.

### Ruby version manager
* It sounds like using a version manager like `rbenv` might be smart.
* And `ruby-build` is an installer (a plugin for `rbenv`) that will let me set up different versions of Ruby in my projects.
* I followed the instructions on [github.com/rbenv/](https://github.com/rbenv/rbenv#homebrew-on-macos)
  * `brew install rbenv` will also install ruby-build.
  * Run `rbenv init` to set up the integration with my shell.
  * Add `eval "$(rbenv init -)"` to `.bash_profile` to load rbenv automatically.
  * …and verify that it’s properly set up with a rbenv-doctor script. Cooool!

### Ruby

* Installing “the current stable version” with `rbenv install 2.4.2`
* Then setting this newer version to the default with `rbenv global 2.4.2`
* Okay, I now have a version of Ruby that Jekyll is happy with. ✌️

### RubyGems

This is a package manager for Ruby, just like npm is for JS.

> …that provides a standard format for distributing Ruby programs and libraries (in a self-contained format called a "gem"), a tool designed to easily manage the installation of gems, and a server for distributing them.
https://en.wikipedia.org/wiki/RubyGems

* commands start with `gem`
* oh… and once again, now I see that this was installed as Xcode Command Line Tools.
* Jekyll itself is a gem in the directory on RubyGems.org
* Now those gemfiles I see everywhere make more sense.

The last requirements listed to install Jekyll are… GCC and Make. It’s getting late, so right now I’m not going to find out what they are. But I have them and they too were installed when I started off with running
`xcode-select --install` — so it’s fun to see that I now know a lot more about what it does, and why I definitely want to run that when setting up a new Mac.

Ran through (and sort of understood most of) the instructions on how to install Jekyll and…

SUCCESS!! 👊

I am now running Jekyll locally and can publish these notes.
