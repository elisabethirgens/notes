---
layout: post
title: "Canvas or SVG?"
date: 2017-07-17
---

I once attended a workshop on Creative JS, and I remember we made some really cool graphics with Canvas during the day. I’m reasonably knowledgeable about the SVG format itself, but with limited experience in scripting it.

But when to Canvas and when to SVG? 🤔 Here are my notes after reading
[this comparison on Microsoft Developer Network](https://msdn.microsoft.com/en-us/library/gg193983) and about the [Canvas API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API).

- any type of graphic can mostly be created with either technology
- but for most scenarios, one will have significant advantages over the other

## SVG

- a markup language for describing graphics
- vector based; made up of shapes
- scalable 💕
- multiple elements that are part of the DOM: `<svg>`, `<path>`, `<rect>` and so on
- can be styled with CSS

## Canvas

- an API for drawing graphics via scripting
- raster based; made up of pixels
- does not support scalability
- a single HTML element: `<canvas>`
- can only be modified through script

| What                      | How                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| high fidelity diagrams    | SVG ✨                                                                                                |
| documents for printing    | definitely SVG 💪                                                                                     |
| schematics to zoom in/out | SVG is scalable 😎                                                                                    |
| static images             | SVG (over canvas) 👌                                                                                  |
| pixel manipulation        | Canvas 💥                                                                                             |
| real-time data processing | Canvas ⚡️                                                                                            |
| charts and graphs         | 📊 depends, for example on level of interactive functionality                                         |
| two-dimensional games     | 👾 depends… canvas will need to redraw and reposition shapes, while SVG can maintain shapes in memory |
