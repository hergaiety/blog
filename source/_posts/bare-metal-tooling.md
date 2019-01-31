---
title: Bare Metal Tooling
description: Tooling comprehension over plugin reliance.
date: 2019/01/30
tags:
  - Vim
  - Dotfiles
  - Devtools
  - Tmux
---

# Getting to Know Your Tools

I'm obsessive over my dotfiles. They're in such a constant state of flux I'm never sure how to self document them. This was a sign. This lead me down a path to better understanding the bare-metal of my chosen tooling to increase my tooling competence.

A sign that in my continous search for the best tooling plugins, perhaps _the core problem was I didn't know my tools well enough_. Ever struggled to remember what your custom Tmux bindings were? Why did I change them anyway... maybe the default `ctrl + b` bindings aren't so bad after all.

Recently I was looking to add a commenter plugin to Vim only to stumble across [this stack overflow result with nearly 2k upvotes](https://stackoverflow.com/questions/1676632/whats-a-quick-way-to-comment-uncomment-lines-in-vim/1676690#1676690<Paste>) using zero plugins or configuration.

![Comment](https://i.stack.imgur.com/lu6aU.gif)

![Uncomment](https://i.stack.imgur.com/2Y7eH.gif)

I'll say that again. _Zero plugins or configuration_, just knowing instead how to leverage `ctrl + v` to vertically select in Vim followed by a `shift + i` to insert or `x` to delete.

The same goes for navigation trees. Most new Vim users, including myself, immediately jump to [NERDtree](https://github.com/scrooloose/nerdtree) or similar plugins and then proceed to learn how they work. Instead, we could just [leverage netrw](https://blog.stevenocchipinti.com/2016/12/28/using-netrw-instead-of-nerdtree-for-vim/) or perhaps [use neither](https://shapeshed.com/vim-netrw/).

---

My dotfiles are still constantly in flux. Though, every iteration it manages to get smaller. I'm increasingly leveraging the raw power of the cores of my chosen tooling (Fish, Tmux and Vim) rather than stacking up a pile of new plugins every few weeks. Learning the bare-metal of your tools can drastically boost tooling competence.

