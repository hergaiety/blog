---
title: Self Code Review with Git Add Patch
description: Reduce errors and typos while building confidence with every chunk you commit.
date: 2017/05/04
tags:
  - Git
  - Workplace
  - Code Review
---

Code reviews reduce logical errors, call out typos, and prevents accidentally committing more code than intended ([1](https://www.atlassian.com/agile/code-reviews)). They're essential for _all sized teams_ pushing to the same code base while _maintaining sanity_.

Should a developer find themselves discovering any accidental "oops!" in their pull request it's a good indicator of a flaw in workflow. **Introducing the interactive self code review:**

``` bash
git add --interactive
```

Interactive adding in git offers a choose-your-own-adventure style "What Now>" series of options.

## The Useful Bit: _Git Patch_

Today let's look at the _**p**atch_ option. We can skip to the patch option in the future with this handy shortcut:

_Example pretends we have file.ext and have added a line that defines a version..._

``` bash
git add -p

diff --git a/file.ext b/file.ext
index sha1..sha2 sha3
-- a/file.ext
++ b/file.ext
{
  "name": "example json",
  +"version": "1.0.0",
  "private": true,
Stage this hunk [y,n,q,a,d,/,e,?]?
```

Looks like a huge chunk of stuff! Broken down, the response describes what file was modified followed by a chunk of color coated git diff.

### Now What? Staging Hunks of Code

Many options are provided in the "Stage this hunk?" prompt following a git add patch.

Pressing `?` in response to the prompt explains each valid response. These are some essentials:

* **y** - stage this hunk
* **n** - do _not_ stage this hunk
* **q** - quit

You'll find that by going through this process you can read every line you'd like to add to a commit and make better choices about them.

### Splitting `s`

These "magical" feeling chunks aren't always smart enough. Sometimes there's a need to split (with the `s` response) a chunk into smaller chunks. This comes up more often than you'd think if you're developing empathetically.

### `a` Add or `d` Don't Add Entire File

An `a` response will stage the current hunk and all the following within the current file automatically. This is **_not_ recommended because you're opting to skip parts of your personal code review**.

However, `d` is a nice way to skip adding anything from an entire file and can save a lot of time.

### Manually Editing

Typos or "oops!" can be quickly corrected with the `e` response. This will open just the chunk for quick adjustments including line adding and removal.

# Summary

Git patch has become a core part of my workflow to **ensure quality** and boost **personal confidence in the code I ship**. Give it a try today!
