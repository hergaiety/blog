---
title: Easy Git Commit Targeting
description: Shortened SHA hashes and relative offsets
date: 2017/04/21
tags:
  - Git
  - Tips&Tricks
---

A generally agreed upon goal of a developer is to use the mouse as little as possible. An often overlooked moment of touching the mouse is the seemingly inevitable moment of having to target a git commit via it's SHA hash. Truth is this doesn't need to be an ordeal.

**Let's look at some alternative ways to target commits**.

## By Shortened SHA Hash

Traditionally to find the `git diff 123abc456def789ghi` on a SHA you'd use the entire SHA hash. Instead, you can type just the first few characters and Git will figure out the rest.

``` bash
git diff 123abc
```

## Tilde

A common target is the previous commit from the HEAD. Using `HEAD~` will specify the intention of one commit before the HEAD.

``` bash
git diff HEAD~
```

### Past Tilde

Adding a number after the tilde `~` will target a commit prior to the head equal to the number specified.

``` bash
git diff HEAD~3
```

## Stacked Carets 🥕🥕🥕

Alternatively, the number of caret characters after HEAD will similarly target a commit prior to HEAD equal to the number of carets.

``` bash
git diff HEAD^^^
```

## Combine These Tricks

So close! Ever want to target the commit just previous to a SHA hash? It's easier than you think.

``` bash
git diff 123abc~
```

# Summary

Through a combination of shortened SHA hashes, HEAD, and relative tilde/caret characters anyone can fly through git history with confidence.
