---
layout: post
title: "Hello Storage in Proton Drive"
date: 2024-01-06
---

I finally managed to say to [goodbye to Dropbox]({{ '/2023/12/goodbye-old-storage/' | url }}), and am now ready to figure out what is next.

## Do I still need storage?

I’ve never had a hard drive die on me in all my years of owning computers. (Hm. Is that true? It’s very possible I’ve forgotten, because it was long ago and because I _did_ have backup, making the experience completely unmemorable.) When I think about what would happen if this laptop disappeared or failed on me right now, it strikes me that the consequences don’t seem quite as dramatic as earlier years. I would loose a lot of files that matter to me, but not _everything_. My password vault and markdown files are synced and backed up in iCloud, all my most important work is now code on GitHub (which is a _very_ different scenario compared to the importance of work in progress and client files in [jobs I had before]({{ '/2020/09/to-all-jobs-i-had-before/' | url }})). I&nbsp;use [Things](https://culturedcode.com/things/) with their [cloud sync service](https://culturedcode.com/things/cloud/). All recent years of photos are also on my phone. 

Not sure I’ve ever thought about this in relation to backup before; that more and more of my digital life is backed up in a multitude of services — compared to my first computers, where almost everything was stored solely on their hard drives. But either way, I am convinced that storing files somewhere other than only this laptop is a worthwhile insurance for the kind of accidents that can happen to a laptop.

## I trust Proton

Proton is a technology company building products with privacy as default. I signed up for my [Proton Mail](https://proton.me/mail) account in 2017, and have been super happy with the product, web app and iOS app. It’s been fun to see them launch more products. So far, I have only used [Proton VPN](https://protonvpn.com/), but I have intentions of migrating to the new password manager [Proton Pass](https://proton.me/pass). Their cloud storage has been under development for a couple of years, and less than two months ago, the [Proton Drive macOS app](https://proton.me/blog/proton-drive-mac-app) was released.

The end-to-end encryption, the Swiss privacy laws and how all their apps are [open source](https://proton.me/community/open-source) — this is all fantastic 🥇. But also, and honestly this is the most essential in how I choose which companies to rely on; I trust Proton to successfully build strong digital products that are great to use.

## Take my money!

My current plan is **Mail Plus** at 47.88&nbsp;€ for 12 months. With this subscription I already have Proton Drive, but only 15&nbsp;GB. I am ready for **Proton Unlimited** at 119.88&nbsp;€ for 12 months, giving me 500&nbsp;GB total storage across all products. The upgrade was super smooth, automatically giving me credit on the payment for the unused portion of my previous plan that had 8 months left.

## Setting up and moving in

Installing the macOS app was a breeze, and so far it seems great. Simple and minimal, which is exactly what I wanted and expected. The icon in the menu bar shows a badge for syncing 🔄 or synced ✅. Initially, I thought that “I probably should” finish setting up new cloud storage before quitting Dropbox. But I ended up taking my chances on some days without backup, and now I have the luxury of moving my stuff in steps, tidy up a bit and create a new file structure. This also means I get to incrementally test how Proton Drive works, without trying to move all my 150&nbsp;GB in one go.

I’ve seen two types of minor hiccups. When I moved a directory over and then immediately started renaming and moving files around, I got some sync errors that were logged. But the files were then synced later, so it was just a notification. I’ve also seen a couple of files duplicated. The originally named file was empty, and then the version of the file that had succeeded in syncing had a longer file name that included ‘Name Clash’. Easily enough spotted and fixed.

So, are upload speeds fast? Ha! Not at all! But there’s a reason for it taking time:

> Unlike iCloud, which does not offer end-to-end encryption by default for files and folders, Proton Drive uses end-to-end encryption for all your data across all devices. File encryption happens automatically on your device before uploading to the cloud. That means nobody — not even Proton — can see your files’ contents. End-to-end encryption is also used for all metadata, such as file names and modified date.<br><br>
— [proton.me/blog/proton-drive-mac-app](https://proton.me/blog/proton-drive-mac-app)

I have no idea if this will bug me. But for now, it gives me another reason to move in slowly and actually look at my stuff in the process. 

