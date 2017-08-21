---
title: Project Health
date: 2017/08/21
tags:
  - Empathy
  - Code Review
---

Recently I was learning automated code review tied to a continuous integration environment for my [test driven project](https://github.com/sharpshark28/json-query-chain). I was asked by a nonprogrammer what I was trying to achieve with all that nonsense. Without buzz words I had to express my intent in simple language.

**I wished to visually show that my project was healthy**. In every sense of the word, a health project _functions as you'd expect it would_.

> If I were to hand you the keys to my truck you'd expect several things to function in a particular way. Firstly, the truck should be able to drive forward and reverse with working steering and breaks. Secondly, you'd expect seat belts. Lastly, if I told you this truck has the pedals reversed you'd consider that a not quite right functional vehicle.
> The "health" of this hypothetical truck failing any of these conditions would drop with every condition it fails. Consequently, **your desire to drive** this hypothetical truck **lessens as it becomes less functional** as one would expect.

[Programs can be analyzed](https://docs.codeclimate.com/docs/list-of-engines) to avoid [code smells](https://blog.codinghorror.com/code-smells/) and ensure a project [can work (has tests)](http://blog.xebia.com/5-reasons-why-you-should-test-your-code/).

However, _this process has its flaws_. Every language has its own quirks and rules. Such a process is subject to human error, such as writing poor tests or tweaking the generally agreed upon rules the project abides by. **This means a 10/10 project analysis score for me _cannot_ be compared to another directly**.

> Imagine being handed your high school graduation test, but _you have the capability of changing most of the rules of the test_ and _so does everybody else_.

This does not mean that a project analysis is completely without merit. Project Health is a broad and wonderfully messy metric to be used as a tool to gain some insight without deep diving into the code. Luckily, in the world of open source all of these per-project rules modifications are visible.

Putting in the effort to better a project's health is a great goal to strive for to push ourselves to new heights and better the world of programming.
