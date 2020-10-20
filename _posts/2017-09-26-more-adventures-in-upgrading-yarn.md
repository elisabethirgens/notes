---
layout: post
title:  "More adventures in upgrading Yarn"
date:   2017-09-26 21:00:00 +0200
---

Yarn has been released in a stable version. One of my co-workers upgraded to yarn 1.1.0 on the build server, and encouraged everyone using Yarn locally to also upgrade on their machine.

## 🙋

That’s me. I know I have Yarn locally, because I had [fun times upgrading Yarn]({{ site.baseurl }}/2017/08/yarn-upgrade-adventures/) two months ago. But now that I’m being more patient and critical… what am I actually using it for locally?

## 🤔 📖 🔍

Right. A project I work on frequently, is set up with Yarn to handle it’s npm packages. Does that *necessarily* mean that I need it installed locally?! Maybe no? But in this case yes, because:
* Yarn handles PostCSS with plugins for this project.
* To run it locally, I need Yarn to build the CSS on my machine.

## 🎓

Poked around in the `package.json`, read some [docs](https://yarnpkg.com/en/docs) (they’re pretty nice!) and more about the `yarn.lock` file. It’s auto-generated, includes everything needed to lock versions of all packages in the dependency tree — not just the top-level. We have it checked in to GitHub. I don’t think I’ve needed Yarn locally to do anything with this file, but I’m assuming that if/when I do add, upgrade or remove any dependencies, I would also then need Yarn installed locally.

---

Let’s check the current status of all the things.

```bash
$ yarn --version
0.27.5
```

I know now that Yarn was installed with Homebrew, but how would I check that if I didn’t remember? And I’m not quite clear on where Yarn is/should be installed on my machine.

```bash
$ which yarn
/usr/local/bin/yarn
```

I think this is the Yarn I want to upgrade. (Do I have others? I remember there was something with multiple Python installations. Maybe that’s competely different? IDK. Moving on…)

```bash
$ brew doctor
Your system is ready to brew.
```

```bash
$ brew update
Permission denied (publickey).
fatal: Could not read from remote repository.
```

## 😢

There are apparently lots of different issues you can get with brew and permissions. But after reading about lots of them, I kinda suspected it was SSH causing problems for me now.

I’m not entirely sure what I did with my SSH config file. I know I had added something to it ages ago to fix the [not loading passphrase on Sierra keychain](https://blog.elao.com/en/tech/ssh-agent-does-not-automatically-load-passphrases-on-the-osx-sierra-keychain/) problem. But looks like I didn’t have the same option as I found suggested both here and there now. (Did I have a different fix, that worked for a while but then gave up a couple of weeks ago? I have been bugged a lot for the passphrase lately, but ignored looking into it before now.) Anyway…

* I updated my `.ssh/config` with [this suggested workaround](https://blog.elao.com/en/tech/ssh-agent-does-not-automatically-load-passphrases-on-the-osx-sierra-keychain/).
* Learnt how to [test my SSH connection](https://help.github.com/articles/testing-your-ssh-connection/)!
* …and yay, now brew happily upgraded and updated everything I asked it to.

```bash
$ yarn --version
1.1.0
```

## 🎉
