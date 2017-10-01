---
layout: post
title:  "Knuth, Metafont and meta-design"
date:   2017-10-01 19:00:00 +0200
categories: thinking
---

I think I cried a bit the first time I read Rune Madsen’s article [On meta-design and algorithmic design systems](https://runemadsen.com/blog/on-meta-design-and-algorithmic-design-systems/). That was 2½ years ago. I was self-employed, and had been working on too many projects that were not quite right for me. That article gave me a fantastic feeling that **this!!!** 😍 omg, this is what I want to do. There may also have been an element of relief — that despite struggling then, despite being late to finding my thing in life and despite having limited formal education… I was on the right track! And that track would take me somewhere really interesting.

---

> Meta-design is much more difficult than design; it’s easier to draw something than to explain how to draw it.

👆 That is Donald Knuth from The Metafont Book. Rune Madsen also uses the quote in [this talk](https://runemadsen.com/talks/uxcampcph/), where he follows up with this comment I really enjoy: 👇

> This idea of designers transitioning from people who draw things to people who write code that draws things is really powerful.

## 🙋

This sounds fun! Can I do that? Have I already done that at some level? How can I dive deeper into this? Well, this lazy Sunday I could read…

## …more about Metafont

* [Metafont](https://en.wikipedia.org/wiki/Metafont) is a language to define vector fonts.
* Knuth developed it to accompany his TeX typesetting system.
* It is a stroke-based, drawing glyphs along a path.
* (Huh, vertices…? Oh, that is the plural of vertex. 🎓 )

This is different from outline font formats like TrueType and OpenType. And this is cool, because I feel like I instinctively understand the potential of stroke-based. It’s probably like refraining from outlining paths in Illustrator, to maintain the actual description of them. The moment you outline paths, you loose information and are stuck with a very precise — but inflexible object.

MyFonts introduces nicely [what Knuth has to do with typography](https://www.myfonts.com/person/Donald_E_Knuth/). In Knuth’s book about the language, The Metafont Book, I found the paragraph where he talks about meta-design:

> Meta-design is much more difficult than design; it’s easier to draw something than to explain how to draw it. One of the problems is that different sets of potential specifications can’t easily be envisioned all at once. Another is that a computer has to be told absolutely everything. However, once we have successfully explained how to draw something in a sufficiently general manner, the same explanation will work for related shapes, in different circumstances; so the time spent in formulating a precise explanation turns out to be worth it.

The main parts of a metafont are:
* administrative details (like numbering the glyphs and positioning them in a box)
* details to draw the basic stroke characteristics (like serifs or bowls)
* high-level descriptions for each character (without specific stroke details)

I like how he thanks his wife especially for her support “during the eight years that I have been working intensively on mathematical typography.” 😂 It reads like a warning. Get out of this rabbit hole while you can. And I think I will. (But I did enjoy reading the preface and first chapter!)
