---
layout: post
title: "Poke at Postgres"
date: 2024-06-12
---

I haven’t worked a lot with databases yet. Does a bit of MySQL way back in my days of hacking WordPress count? At work there haven‘t been many databases in my immediate vicinity until more recently. However my current team is more full stack that many of my previous teams, and I now work on applications that have data in PostgreSQL. _Now is a good time a time as ever to dive in!_

## SQL is a query language

This is clear to me. When I did [CS50](https://github.com/elisabethirgens/cs50) there was a lecture and two problem sets where we wrote SQL queries. I often find it useful to skim though lists of a technology, there is something about connecting dots and putting things in relation to each other. SQL is a [query language](https://en.wikipedia.org/wiki/Query_language) and a different one is GraphQL. Which I am not sure I had quite grasped is also a query language and not ‘some kind of database of sorts’ until writing these notes right now. Useful dots to connect!

## Types of databases

I know there are different types of databases and I reckon it will be useful to also read up a bit on that. Easier said than done when there are so many different lists and classifications. But I think this will do for now for me to put things in relation 😏 to each other:

- Hierarchical databases
- Relational databases (examples PostgreSQL, MySQL)
- Non-relational databases (examples MongoDB and Redis)
- Columnar databases (examples BigQuery, MariaDB)
- Object-oriented databases

At this point I have no clue what [postgresql.org/about](https://www.postgresql.org/about/) mean when they describe PostgreSQL as a **object-relational database system**, but I can understand that later.

## Database administration

I understand that to work with Postgres I need an admin tool, and from the very long list of possible alternatives, I make note of these three:

- `psql` seems like the most common CLI
- `pgAdmin` is a web or desktop application with a GUI
- `phpPgAdmin` is not what I will look further into now, but reading about it was an interesting link back to when I used the web-based [phpMyAdmin](https://en.wikipedia.org/wiki/PhpMyAdmin) 15 years ago to admin MySQL for WordPress and I had not seen that interface in a really long time!

But now I am procrastinating. After [installing Eugene]({{ '/2024/06/install-eugene/' | url }}) yesterday, I was reading this post about <br>[Using short lived postgres servers for testing](https://kaveland.no/posts/2024-05-27-shortlived-postgres-servers/)

There are gaps in my understanding of things that need to be filled for me to be able to do what Robin describes in his blog post, and this is when I am reminded of having a plan to start using ChatGPT for learning. I haven’t exactly been living under a rock, but also I have not been in a hurry to sign up. <br>Again: _now is a good time a time as ever to dive in!_

## Hello, ChatGPT!

> I am a frontend developer looking to learn more about PostgreSQL, how can I get started to understand more about databases?

The response I get is an extensive study plan, a “structured approach to help you learn efficiently” with steps to understand the basics, get started with PostgreSQL, hands-on practice, advanced topics, integration with frontend and continuous learning. I like it. Not going to follow this exactly as described, but it makes it clear that a good next step for me is to go install PostgreSQL already. But how? This is the kind of thing I can get a bit lost in trying to find _the optimal approach_ as if making “the wrong choice” is irreversible. Anyway…

> What are the potential advantages and disadvantages of installing PostgreSQL with the Interactive installer by EDB vs using homebrew?

Ooo, now we are talking. This response is really helpful, and makes it easy for me to see that Homebrew is the way to go for me now. (I really like using Homebrew! but I guess there is something about not always being clear on when I might want to use a version manager to install a thing, makes me hold back a bit from running to brew install without considering the alternatives.)

## brew install

```
==> Caveats
==> postgresql@16
This formula has created a default database cluster with:
  initdb --locale=C -E UTF-8 /opt/homebrew/var/postgresql@16
For more details, read:
  https://www.postgresql.org/docs/16/app-initdb.html

postgresql@16 is keg-only, which means it was not symlinked into /opt/homebrew,
because this is an alternate version of another formula.

If you need to have postgresql@16 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/postgresql@16/bin:$PATH"' >> ~/.zshrc

```

- Update my `.zshrc` in [/dotfiles/commit/](https://github.com/elisabethirgens/dotfiles/commit/c853d87bbc5ac192c675ca3a76fa38453fe50ee1) to find the brew installed postgresql

## hello psql 👋

Can I now run for example `psql --help` and these other commands? Yes!

|            |                                                                         |
| ---------- | ----------------------------------------------------------------------- |
| `psql`     | is the PostgreSQL interactive terminal                                  |
| `initdb`   | initializes a PostgreSQL database cluster                               |
| `pg_ctl`   | is a utility to initialize, start, stop, or control a PostgreSQL server |
| `postgres` | postgres is the PostgreSQL server                                       |

and `psql --list` shows me a list of databases that were created in the brew install.

## What’s next, ChatGPT?

> I have used Homebrew to install postgresql@16 and when I run `psql --list` I can see the default database cluster created by the formula. How can I import data from a CSV file to this database?

I wasn’t quite sure what to expect from using ChatGPT to guide my learning like this. I am pleasantly surprised! The official [PostgreSQL Tutorial](https://www.postgresql.org/docs/current/tutorial.html) is extremely dense and covers everything under the sun.

Had I searched the web for ‘csv to postgres’ like I previoulsy would have done, I’d probably need to wade though a flood of varying quality tutorials and blogposts describing _not quite_ what I needed. The recipe I&nbsp;got from ChatGPT on this prompt, describes 3 specific steps in a way I can skim though and quickly conclude that “Oh! Right. Well, I got this” 🦾
