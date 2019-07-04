---
layout: post
title:  "All Roads Lead To React"
date:   2019-07-04 21:00:00 +0200
categories: learning
---

There’s a security alert I have been eyeing for a while. Since it was java related and technically another team’s application, I hadn’t picked it up earlier… but today was the day. GitHub found a vulnerability and suggested remediation:

```
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>[2.9.9,)</version>
</dependency>
```

## Do I manually update the pom.xml? 🤔

Let’s find out. Jenkins is by far the most eager commiter in this file, but I can also find humans bumping versions. I also found that we don’t specify versions directly for that dependency, but have them grouped together like so:

```
    <properties>
        <jackson.version>2.9.8</jackson.version>
    </properties>
```
```
    <artifactId>jackson-databind</artifactId>
    <version>${jackson.version}</version>
```

And there we go; I see that the previous version bump to that was committed by a developer. So now I know where and what version number to change.

Figuring out what to do by reading code and git history FTW 💪

## How can I verify that this works?

Don’t really know what I’m doing with this upgrade, but there are plenty things I can check. Does the app build? Tests pass? Run locally as before? Work fine when deployed to a test environment? Yes. Yes, yes and yes. Then there is every reason to suspect we are good to go. I still like being extra clear with opening pull requests like this and describe my process. Including the _“I have no idea what I’m doing, but I’m guessing this is okay to do like so”_ for the reviewer to take into consideration. I even babysat this deploy in jenkins, which I don’t usually do anymore.

Yay. All is fine and the GitHub alert is now gone. 🏆

## …but what is jackson?

It’s July and time for rabbit holes, so who even is this Jackson character and which concepts can I learn a bit more about today?

> the original use case for Jackson was JSON data-binding, it can now be used for other data formats as well, as long as parser and generator implementations exist

* It’s a JSON parser for Java (but now also more than JSON)
* The Jackson Project lives on [FasterXML/jackson](https://github.com/FasterXML/jackson)
* [fasterxml.com](http://fasterxml.com/) has the most amazing retro website

There are three core modules:

* `jackson-core` for low-level incremental ("streaming") parser and generator abstractions
* `jackson-annotations` with general purpose annotations used on value and handler types
* `jackson-databind` seems to be the “main” project building on the other two as foundations

## …and what actually is data binding?

The internet has a lot of less than helpful content about data binding, but found this:

> Data binding makes the link between the user and the data source, which is usually a database. When you submit a form on a website, the data binding is what sends your information to database. <br>– [What is Data Binding?](https://dev.to/flippedcoding/what-is-data-binding-ghn) by Milecia McG

> It connects the front-end of your website to the back-end server.

Sounds good! But I’m getting a bit confused again when I see that Wikipedia is listing React, Vue, Angular and so on as “data binding frameworks and tools”. Hm.

Sometimes it’s easier to grasp a thing **in relation to another thing** I’m already familiar with. Wikipedia lists data binding in the category “data management”. I see the pages in this category are everything from backup and copyright to metadata, so now I understand more how broad this concept actually is. Let’s wikipedia downwards instead of up! 👇

| React | “One-way data binding with props” is the first mention under notable features |
| Angular |“two-way data binding is its most notable feature, largely relieving the server backend of templating responsibilities” |
| Polymer | “Both One-way and Two-way data binding” |
| Ember | “Ember also provides dependency injection, declarative two-way data binding, computed properties, and automatically-updating templates” |

I also found this description in a [Vue and AngularJS comparison](https://vuejs.org/v2/guide/comparison.html#Data-binding) that was helpful:

> AngularJS uses two-way binding between scopes, while Vue enforces a one-way data flow between components. This makes the flow of data easier to reason about in non-trivial applications.

## Is data binding and data flow the same?

Hm. I want to say “No, but related?!” Or is it just more common to call it flow if it’s one way? Not sure it matters, but fun to realize I’ve stumbled across this from a humble attempt at making a GitHub security alert go away. Learnt a lot today!

> There are two approaches about how data should flow in WebApps, Unidirectional data flow (React) and two-way binding (Angular). <br>–&nbsp;[Unidirectional data flow vs two-way binding](https://medium.com/@luillyfe/unidirectional-data-flow-vs-two-way-binding-e34f1f08677) by Fermin Blanco

Wheee, also found a lovely comic by erty: [JavaScript Comic: Data Binding](https://erty.me/comics/js-comics/6) 💕  
