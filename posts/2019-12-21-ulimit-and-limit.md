---
layout: post
title:  "Persist ulimit Settings in macOS Catalina"
date: 2019-12-21
---

This fancy sounding heading was totally authored _after_ I understood what I wanted to do, which happened from writing up all these notes.

**Disclaimer & tl;dr** 👉 _I have yet to figure out how to do this, because I don’t want to throw a bunch of commands at my computer I don’t understand the consequences of. Wish me luck for 2020._

---

## The annoyance I want to improve

The project I’m working on uses OpenShift, and apparently I need to ramp up the system-wide resources for Minishift to run happily. Specifically: increase the number of open files per process. I’ve set a thing in my `.bashrc` and run some commands and it’s all working fine. But after every restart, I get an error in a new shell and need to repeat the process. This is in my `.bashrc` file:

```bash
ulimit -n 500000
```

But after a reboot, the terminal will complain that:

```bash
-bash: ulimit: open files: cannot modify limit: Invalid argument
```

When I check, I can see that the number has returned to 256:

```bash
launchctl limit maxfiles
maxfiles    256            unlimited
```

Then I can run this command to increase it:

```bash
sudo launchctl limit maxfiles 5000000 5000000
```

And check that it increased:

```bash
launchctl limit maxfiles
maxfiles    5000000        5000000
```

But after the next reboot, I need to repeat the command. So let’s dig into what all this stuff is, so I can try to improve the set up and learn what’s actually going on.

### `launchctl`

> launchctl interfaces with launchd to manage and inspect daemons, agents and XPC services. launchctl allows for detailed examination of launchd endpoints. <br> —&nbsp;BSD General Commands Manual


### `launchd`

> launchd manages processes, both for the system as a whole and for individual users.
> The primary and preferred interface to launchd is via the launchctl(1) tool which (among other options) allows the user or administrator to load and unload jobs. Where possible, it is preferable for jobs to launch on demand based on criteria specified in their respective configuration files. —&nbsp;BSD General Commands Manual


### `ulimit` and `limit`

A-ha. These are shell `builtin` commands. Just like `cd`, `echo` and `pwd`. 🤩

> a command or a function that is executed directly in the shell itself, instead of an external executable program which the shell would load and execute. —&nbsp;[wiki/Shell_builtin](https://en.wikipedia.org/wiki/Shell_builtin)

In the man page for `launchctl` I can find this description about `limit`👇<br> but do I wonder why it’s listed under Legacy Subcommands 🤔

> With no arguments, this command prints all the resource limits of launchd as found via getrlimit.  When a given resource is specified, it prints the limits for that resource. With a third argument, it sets both the hard and soft limits to that value. With four arguments, the third and forth argument represent the soft and hard limits respectively.

But description makes sense, this is what the sudo command above does.

---

## More words and concepts to take note of

`init` is the first process started during booting of the computer system. Read more: [wiki/Init](https://en.wikipedia.org/wiki/Init)

[Operating system service management](https://en.wikipedia.org/wiki/Operating_system_service_management) examples:
* launchd - Used by Apple macOS
* systemd - Used by many Linux distributions

`daemon` is a computer program that runs as a background process, rather than being under the direct control of an interactive user. Read more: [wiki/Daemon](https://en.wikipedia.org/wiki/Daemon_(computing))

> Traditionally, the process names of a daemon end with the letter d, for clarification that the process is in fact a daemon

> the parent process of a daemon is often, but not always, the init process

---

## But back to figuring out what to do…

Now I understand way more what those commands up there do. It works, just not permanently.<br>
Reading: [Increase the maximum number of open file descriptors in Snow Leopard?](https://config9.com/linux/macosx/increase-the-maximum-number-of-open-file-descriptors-in-snow-leopard/)

* Previously you could set the limits in a `/etc/launchd.conf` but this is not longer supported
* You can still use `launchd.plist` but is it recommended? 🧐

```
sysctl -a | grep ^kern.max
```

Cool command! What does it do?

| `sysctl` | a software utility of some Unix-like operating systems that reads and modifies the attributes of the system kernel such as its version number, maximum limits, and security settings |
| `-a` | List all the currently available non-opaque values |
| `grep ^kern.max` | …but instead of outputting the entire list, run a search and just return results that include `kern.max` |

```
kern.maxvnodes: 263168
kern.maxproc: 4176
kern.maxfiles: 49152
kern.maxfilesperproc: 24576
kern.maxprocperuid: 2784
kern.maxnbuf: 16384
```

Reading: [How to persistently control maximum system resource consumption on Mac?](https://unix.stackexchange.com/questions/108174/how-to-persistently-control-maximum-system-resource-consumption-on-mac/#answer-548808) While I don’t understand the details, the answer below _sounds_ like good advice. It explains how you’re likely to run into problems by changing these limits, and there is an alternative:

> In general, rather than tuning individual parameters on the system and throwing the system out of balance (and potentially letting a single program crash the system by taking up all the resources), if the default system limits are insufficient for your needs, I recommend turning on "Server Performance Mode", or at least giving it a try.

Official Apple advice how to: [Turn on performance mode for macOS Server](https://support.apple.com/en-us/HT202528)


> performance mode can be enabled even without macOS Server being installed to achieve similar benifits for other high-performance services<br> –&nbsp;[Enable macOS Server Performance Mode](https://gist.github.com/davidalger/a3afa2410a40ce6ae59d4e6a3b18e5c7)

🤷🏻‍♀️ Tried this, but it didn’t work. Running Minishift still fails due to too many open files.

### Should I leave it on anyway?

> Server Performance Mode does take up more memory, and makes the system much more likely to suffer if some program goes out of control consuming resources, but greatly increases the capability of the system to handle a lot more background tasks. I think Apple made the right call by not turning it on by default but also making it easy to enable.<br>–&nbsp; [What does serverperfmode=1 actually do on macOS?](https://apple.stackexchange.com/questions/264958/what-does-serverperfmode-1-actually-do-on-macos/373026#373026)

Hm. I don’t entirely understand this. I’ll leave it on for now, and made a note to revisit later.

### What are hard and soft limits?

> The two numbers represent soft and hard limits. When the soft limit is reached, the process may receive a signal but will be allowed to continue. When it reaches the hard limit, it will be blocked. &emsp;–&nbsp;[Persist ulimit settings in Mac OS X](https://coderwall.com/p/lfjoaq/persist-ulimit-settings-in-mac-os-x)

### sysctl – configure kernel parameters at runtime

The numbers are higher, and round?! 🤔 with `serverperfmode=1` turned on.

```
sysctl -a | grep ^kern.max
kern.maxvnodes: 300000
kern.maxproc: 5000
kern.maxfiles: 300000
kern.maxfilesperproc: 150000
kern.maxprocperuid: 3750
kern.maxnbuf: 16384
```

…and I learnt so much about how my machine works. But for now I will have to stick with re-running the `sudo launchctl limit maxfiles 5000000 5000000` command after each reboot.
