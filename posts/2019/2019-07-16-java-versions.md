---
layout: post
title: "Detour Into Homebrew and Java Versions"
date: 2019-07-16
---

The app I’m working on won’t build, but I know it was recently updated to Java 12. Have I got Java 12 installed? Apparently not. I ran this to find which versions I currently have installed:

```
/usr/libexec/java_home -V
```

- OpenJDK 11.0.2
- Java SE 10.0.1
- Java SE 8
- Java SE 7

The onboarding guide we’ve got at work suggests (without explaining much):

```bash
brew tap caskroom/homebrew-versions
```

I remember that I can install different older versions either:

- manually by downloading from oracle.com
- or by running brew commands

But why choose one over the other? And how can I tell which way I installed the previous versions? Does it matter? (Yes! I learnt a boatload and more about all this below 👇)

## Wtf is a tap anyway?

[docs.brew.sh/Taps](https://docs.brew.sh/Taps) says they are **third-party repositories** and:

> brew tap adds more repositories to the list of formulae that brew tracks, updates, and installs from. (…) You should create your own tap for formulae you or your organisation wish to control the versioning of or those that do not meet the above standards.

```
brew tap
```

Will output this on my laptop:

```
caskformula/caskformula
homebrew/cask
homebrew/cask-versions
homebrew/core
homebrew/services
weikengchen/caskformula
```

There are two named caskformula that are shortcuts for: [caskformula/homebrew-caskformula](https://github.com/caskformula/homebrew-caskformula) and&nbsp;the fork [weikengchen/homebrew-caskformula](https://github.com/weikengchen/homebrew-caskformula). Apparently from installing Inkscape some time back, which I do vaguely remember now that I see [this issue on GitHub](https://github.com/caskformula/homebrew-caskformula/issues/51). All right then.

The other four taps refer to these projects, all on the Homebrew org:

| Repo                                                                                     | and their GitHub descriptions                                                          |
| ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [homebrew-cask](https://github.com/Homebrew/homebrew-cask)                               | 🍻 A CLI workflow for the administration of macOS applications distributed as binaries |
| [homebrew&#8209;cask&#8209;versions](https://github.com/Homebrew/homebrew-cask-versions) | 🔢 Alternate versions of Casks                                                         |
| [homebrew-core](https://github.com/Homebrew/homebrew-core)                               | 🍻 Default formulae for the missing package manager for macOS                          |
| [homebrew-services](https://github.com/Homebrew/homebrew-services)                       | 🚀 Manage background services with macOS' launchctl daemon manager                     |

Ok, so the way I understand it now, is that these are different parts of Homebrew. But I wonder about the description that taps are third-party?! Anyway, the one called cask-versions is what supports the installation of alternate versions (of Java in this case, but could be any others). The “default homebrew behaviour” is to install the current newest version. The readme says:

> not intended to be used for all and any old versions you personally require. Casks submitted here should be expected to be used by a reasonable number of people and supported by contributors long-term.

Hm. I’m confused about the content in the [homebrew-cask-versions/Casks/](https://github.com/Homebrew/homebrew-cask-versions/tree/master/Casks) directory, because it seems to include just a short list of java versions. (Only 6 and 11 now.)

[The announcement of Homebrew 1.2.0](https://brew.sh/2017/05/01/homebrew-1.2.0/#post) says that:

> Homebrew/homebrew-versions has been moved into Homebrew/homebrew-core <br> Homebrew provides better, official support for different versions.

Is the suggestion from the onboarding guide still valid — or now outdated? 🤔 Not sure.

## But what is actually a cask?

[Homebrew terminology](https://docs.brew.sh/Formula-Cookbook#homebrew-terminology)

> An extension of Homebrew to install macOS native apps

Yeah… that doesn’t help at all. But searching for `homebrew cask vs formula` and going through some links landed me on [an amazing issue](https://github.com/Homebrew/homebrew-cask/issues/7002#issuecomment-60494082) with this description:

> The difference isn’t between binary and app, but between downloaded as source code that will be compiled, or as an already compiled package. The distinction is important because the result is different. brew install macvim takes (possibly way) longer to install then brew cask install macvim. The former provides flexibility, while the later provides speed.

## 🤯😱🥳

## Whoa! That explains why…

There’s no java listed when I run `brew list`. Because those are what I’ve installed as source code to be complied, not packages ready to go. Very enlightening.

## But back to the java version…

```bash
brew cask install java12
Error: Cask 'java12' is unavailable: No Cask with this name exists.
```

Right, because casks are _previous_ versions.

```bash
brew cask install java
Warning: Cask 'java' is already installed.
To re-install java, run:
  brew cask reinstall java
```

Worked like a charm, except… doh. This now removed Java10, which I need.

```bash
brew cask install java10
Error: Cask 'java10' is unavailable: No Cask with this name exists.
```

Soooo, it seems that if a version has reached end of support, the cask is removed. Makes sense, but that also means our onboarding guide is outdated, so now I ended up trying to fix that. ✏️

The rabbit hole continues as folks on slack mention openjdk being a thing in the world.

## OpenJDK

> OpenJDK (Open Java Development Kit) is a free and open-source implementation of the Java Platform, Standard Edition (Java SE).[1] It is the result of an effort Sun Microsystems began in 2006. &mdash;&nbsp;[wikipedia.org/wiki/OpenJDK](https://en.wikipedia.org/wiki/OpenJDK)

[AdoptOpenJDK/homebrew-openjdk](https://github.com/AdoptOpenJDK/homebrew-openjdk) supports installing different versions of OpenJDK.

## Reading more in homebrew issues

Came across a comment by Homebrew maintainer Claudia Pellegrino, where she wrote up “a few random factoids” that are super interesting to read: [issue about java development casks](https://github.com/Homebrew/homebrew-cask/issues/57387#issuecomment-482822613).

---

### Unanswered questions and remaining problems

What (if any?) is the relationship between the Java that Mac OS wants to handle in system prefs —&nbsp;and the versions I need for development to run applications?

What _is_ the command I used to find which Java versions I had? [explainshell.com](https://explainshell.com/) comes up with nothing and then I don’t know where to look.

```
/usr/libexec/java_home -V
```

- Can I get back Java10 again without creating an Oracle account?
- Or can I use OpenJDK10 to run the not-updated-yet app locally?
- And how do I get rid of Java7?

```bash
brew cask uninstall java7
Error: Cask 'java7' definition is invalid: Token '{:v1=>"java7"}' in header line does not match the file name.
```

And I get the same error on `brew cask list` so I’m guessing I’ve got some general brewery debugging and clean up to do tomorrow…
