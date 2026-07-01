---
layout: post
title: "It’s always the phone book"
date: 2026-07-01
---

I have no idea when I last updated the site at [elisabethirgens.com](https://elisabethirgens.com/) but I‘m guessing it’s been at least 5&nbsp;years. I can’t find out either, because version control is nowhere in sight. So I am basically the dev who talks about Git at conferences, and yet never set up a repo for that particular site. The project was a WordPress site I rigged sooo very many years ago, that “deployment” happened by moving files in the [Coda](https://en.wikipedia.org/wiki/Coda_(web_development_software)) editor that included Panic’s lovely FTP client [Transit](https://en.wikipedia.org/wiki/Transmit_(file_transfer_tool)). 🥰

Apparently, I am also the developer who has kinda specialized in software maintenance, but at the same time had my personal site depending on a ridiculously outdated version of php. When the hosting service flagged they would start charging extra for that ancient version, I clicked a button to upgrade and… not too surprising, my website went blank. I might try to salvage older content at some point, there are some texts there that I’d love to still have online. But right now, I am happy for an excuse to start fresh.

With a git repo! and super simple publishing with GitHub Actions to GitHub Pages. That means I first need learn a bit more about what this DNS control thing wants from me. For me, DNS was first a thing that the hosting provider handled. And now, it is a thing that the SRE team at work handles. I know that it is an important protocol for the internet and might even have guessed that it is in the application layer along with https and ftp and ssh. It is the phone book of the Internet. And I know we joke about how  “it’s always DNS”. But I don’t think I’ve actually done anything with DNS myself before.

## Domain Name Service

Wikipedia describes that DNS: _translates readily memorized domain names to the numerical IP addresses needed for locating and identifying computer services and devices with the underlying network protocols._ Yup, sounds like a phone book. The phone book has a set of resource records. The records have a type and properties that people have agreed upon for building the Internet.

| Type | What this record is for |
| :--- | :--- |
| A | Address record, the most basic record for IP addresses |
| AAAA | Also address record, but for IPv6 addresses |
| MX | Mail Exchange record, a list of mail exchange servers that accept email for a domain |
| NS | Name server record |
| CNAME | Canonical name record, an alias of one name to another |
| PTR | Pointer to a canonical name, for reverse DNS lookups |
| TXT | Text record |

## Ready to set up a custom domain for my GitHub Pages site

The new repo `elisabethirgensdotcom` now exists and has a static deploy to GitHub Pages. Next I want to customize the domain name and need to dive into the GitHub Docs for [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) 😅

## pseudo resource record ALIAS

> An ANAME, ALIAS. apex CNAME, CNAME flattening, or sometimes also top-level redirection record is a pseudo record type and a commonly used but not RFC-standardized record type. Its implementation varies. It serves as an alternative to CNAMEs especially for the bare domain name and where such records should co-exist with others. It causes the DNS software vendor to synthetically generate A and AAAA records similar to the ones of the ANAME-records destination. If the destination changes these synthetic A and AAAA records change automatically as well. The actual mechanisms used are often considered proprietary.

Hm, okay. I got confused by GitHub Docs describing how I needed to set “at least one `ALIAS`, `ANAME`, or `A` record” without specifying how I pick which one.

## apex domain

I didn’t know this phrase and got tripped up by it. Now I understand they just mean a domain like `elisabethirgens.com` is an apex domain but `www.elisabethirgens.com` is not. Subdomains are also not apex domains. Dictionaries define apex as “the top or highest point of something”.

## Confirm my DNS record is configured correctly

What I do appreciate about the GitHub Docs, is that they show how I can confirm that I did the thing. All good documentation should be written to include how to verify that you did the thing. 

And look! I did the thing 🎉

```
dig elisabethirgens.com  +noall +answer -t A

elisabethirgens.com.	300	IN	A	185.199.110.153
elisabethirgens.com.	300	IN	A	185.199.111.153
elisabethirgens.com.	300	IN	A	185.199.108.153
elisabethirgens.com.	300	IN	A	185.199.109.153
```

## Verify a custom domain for GitHub Pages

This is an important step, making sure that the DNS records I have set on my domain can not be misused by GitHub users who are NOT me, in a takeover attack. And again, the GitHub Docs gives a `dig` command to verify that I have successfully verified my domain. Yay!

## dig - DNS lookup utility

> dig is a flexible tool for interrogating DNS name servers. It performs DNS lookups and displays the answers that are returned from the name server(s) that were queried.

## Also e-mail and other cleanup

I don’t use the e-mails with my domains much any more, I mostly use my Proton address. But I do want be able to receive anything sent to them, and it would be useful to not need a separate provider or client. And now that DNS is less bewildering, setting up these e-mails with my domain as addresses in Proton Mail is completely achievable. The Proton Mail app has a great wizard and also the docs are quite readable: [proton.me/support/custom-domain](https://proton.me/support/custom-domain)

Since this is the first time I visited the DNS control for my domain, it revealed a graveyard of domain names I once owned but never used and have since let go of. But the DNS records that were automatically creating along with them, they where still there for me to clean up now.

# 💁🏻‍♀️ 

So yeah, I know DNS now (think Neo who knows kung fu). Which is a good thing, because the next time my site goes blank, it might very well be DNS.