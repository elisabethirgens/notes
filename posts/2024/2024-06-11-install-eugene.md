---
layout: post
title: "Install Eugene"
date: 2024-06-11
---

I am diving into learning some PostgreSQL this week, and since I get to decide how to do that, I choose to start with taking a look at a tool that my friend Robin has recently started building:

> [eugene](https://github.com/kaaveland/eugene) is a linter and command line tool for reviewing SQL migration scripts for postgres.

Turns out that figuring out how to run eugene on my machine is one of those things that starts out blurry, and after a surprisingly short amount of time, during the evening the same day, suddenly feels crystal clear and obvious. It was first _after_ I had played around with installing in different ways that many things made a lot of sense — and such is the way of _computer things becoming obvious_. I know I will soon forget what I was confused about, so here are some notes about what I learnt along the way.

## Cargo and crates 📦

The instructions mention `cargo install eugene` and I don’t have Cargo installed yet. But I already know that eugene is written in Rust, and made my way to [rust-lang.org/tools/install](https://www.rust-lang.org/tools/install) for official instructions. Which at the time of writing for macOS are:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

We do not run random commands without understanding them first 🫡<br>
so let us deconstruct that concoction:

- `curl` is a tool for transferring data using URLs
- `--proto '=https'` tells curl to use the protocol for HTTPS
- `--tlsv1.2` tells curl which [TLS version](https://everything.curl.dev/usingcurl/tls/versions.html) 👀
- `-sSf` silent mode / but show error if curl fails / let HTTP fail silently (h/t [explainshell](https://explainshell.com/explain?cmd=curl+-sSf))
- `https://sh.rustup.rs` is the URL to download the install script
- `| sh` to pipe the downloaded script into my shell

Let’s take a proper look! When I visit the URL in a browser, I see a file downloaded as `rustup-init.sh`. I wondered how and why the `.rs` Rust file is turned into a `.sh`&ensp;_thinking intensifies_ 🤔&ensp;Oh.&nbsp;Right. 😆 That is no Rust file. The `.rs` is only part of the domain, and the top-level domain for Serbia. But I see now why I initially read it wrong — and also why it’s popular for URLs related to Rust!

```
#!/bin/sh

# This is just a little script that can be downloaded from the internet to
# install rustup. It just does platform detection, downloads the installer
# and runs it.
```

Okay, I am ready to follow instructions to install Cargo. And I quickly see this message:

```
Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.
```

- Verify install with `cargo --version`
- also use `rustup --version` to see that I now have the rustup toolchain manager

## cargo install eugene?

Nope. I got an error, did some searching and confused myself into thinking this was not the installation option I was looking for, and jumped onwards to a different installation option. (That turned out to be a detour, but I had a lovely walk though the woods! No regrets.)

## Download as a binary!

Alternative installation: download from [github.com/kaaveland/eugene/releases](https://github.com/kaaveland/eugene/releases) Okay, so I know I have other binaries in different locations, and I know I can add a PATH to my dotfile `.zprofile` or `.zshrc`. But that doesn’t mean it’s entirely clear to me where to put this specific binary on my machine.

- `echo $PATH` gives me a jumble I can’t read with too many directory paths listed
- `tr ':' '\n' <<< "$PATH"` gives me a list with line breaks that I can read!

This is a long list of things I recognize, and things I don’t recongnize, and hm… I need to find a different way to figure out where to put this binary. I suspect that “it doesn’t matter” where I put this file as long as PATH can find it, but my fear of doing something _less than optimal_ means I want to understand which is the _optimal_ directory. One thing I know I have on my computer that I can think of in the same category is `dexter`, which is an authentication helper for Kubernetes that I remember downloading directly from [github.com/gini/dexter/releases](https://github.com/gini/dexter/releases) in the same way I want to do now with `eugene`.

- `which dexter` shows me I put that binary in `/usr/local/bin/`
- `cd /usr/local/bin && ls` shows me that I recognise everything I find in here as something I have put there, while if I list directory contents in any of the _other_ directories named `bin`, they are filled with binaries not installed by me, so I think I found my optimal directory!

### …and which binary do I want?

- `arch` will verify my machine's architecture type

The output I get is technically `arm64` which is the same as `aarch64`. <br>
Okay, so one of these. But why are there two?

- `eugene-aarch64-apple-darwin` 9.38 MB
- `eugene-aarch64-apple-darwin.sha256` 94 Bytes

I recognize SHA-256 as a hash algorithm, but I have not had those in the front of my brain since doing CS50 and dealing with [hash functions for my spell-checker]({{ '/2021/09/hash-functions/' | url }}). And I am not sure what it means in the context of these binaries. With the difference in file size, I am guessing the `sha256` is basically a compressed version?! Not sure what that means for how to run them, I will just try both. 🧪😁

### Unidentified developer

> The binary isn't signed and notarized, so on macos it'll give you a warning. If you want to proceed anyway, you can use `xattr -d com.apple.quarantine eugene` to remove it.

I could’t get that `xattr` command to fly at this point, but I remembered what I had done to grant an exception for `dexter` with these steps with Finder and clicking into System Settings > Privacy & Security, as described by Apple on [Open a Mac app from an unidentified developer](https://support.apple.com/en-gb/guide/mac-help/mh40616/mac).

### chmod

Still not able to run `eugene`, but I see the permissions are wrong. This makes me think of how it’s nice and all that people are taught how to be careful with a command like `chmod` but this is one of those tools where I have needed to unlearn that it is dangerous and “to stay away”. That I now do actually know what I am doing, and I don’t need to be afraid of changing permissions anymore.

- `chmod u+x eugene-aarch64-apple-darwin` gave this binary the same permissions as dexter and the others

I kinda understood that I still couldn’t run `eugene` because there was nothing called that. I noticed that I could now run `eugene-aarch64-apple-darwin` and so I made an `alias eugene="eugene-aarch64-apple-darwin"` in my `.zshrc` — and then I could successfully run `eugene` 🥳

Making that alias was when it started to dawn on me that I was probably supposed to rename the downloaded binary. It was also very helpful describing the hoops I had jumped through on [github.com/kaaveland/eugene/issues/48](https://github.com/kaaveland/eugene/issues/48) and getting confirmation about which alternative hoops I could use.

Let’s go again! 🎬

## Download as a binary, take 2!

When I play around with this a second time, it now seems obvious to me that it’s my job to actively name the binary when I download the file from releases. I see now that the browser prompts me for a name when I save the link. And even it I just hit enter, and then get the `eugene-aarch64-apple-darwin` name, it might have made sense to move the file with something like this (instead of preserving the full release name when moving to `/usr/local/bin/`):

- `sudo mv eugene-aarch64-apple-darwin /usr/local/bin/eugene` to move and rename 💁🏻‍♀️
- `xattr -d com.apple.quarantine eugene` now works nicely when run from the same directory

I like how smooth that last command is, compared to clicking around in Finder and System Settings > Privacy & Security. And I have written documentation at work related to dexter I now want to update!

## cargo install eugene, take 2!

While it was useful to learn how to install this as a binary, I jumped away a bit too quickly from the initial installation with Cargo. When read the error message from Cargo, I see that I need to install cmake.

- `brew install cmake`
- `cargo install eugene` is now successful
- `sudo rm /usr/local/bin/eugene` to remove the binary <br>(more commands I have needed to _unlearn_ to never use 😅)
- `which eugene` to verify that the eugene found is now installed by Cargo<br> (because I can see it in here: `.cargo/bin/eugene`)

```
~ ᐅ eugene --help
eugene is a tool for writing safer schema changes for PostgreSQL

eugene can run your migration scripts and detect which locks that is taken by each
individual SQL statement and summarize which operations that conflict with those
locks, in other words what the script must wait for and what
concurrent transactions that would be blocked.
```

## Writing documentation

As a person who likes writing documentation, I am interested in how documentation is written. It cannot explain everything to everyone, any kind of README.md has to make some assumptions. And for a tool like Eugene, especially in it’s very early days!, it is perfectly reasonable to assume that anyone who for example doesn’t have Cargo installed on their machine, are able to find out what that is and how to get it. You can’t search for ‘cargo’ alone, but a search for ‘cargo install’ will send you to Rust. That said, I&nbsp;think this [update to the installation docs](https://github.com/kaaveland/eugene/commit/a55d9c937757725ee05b07668d72fa4c8013a65d) after my adventure yesterday looks great.
