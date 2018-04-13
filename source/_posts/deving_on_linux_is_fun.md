---
title: Dev'ing on Linux is Fun!
description: Sometimes necessity gives you an excuse to learn some new fun stuff.
date: 2018/04/12
tags:
  - Dotfiles
  - Devtools
---

I **love** playing with my dotfiles. No, really, I could have played video games before bed but here I am up late _again_ customizing my tooling stack. It's a weird passion I have. I blame my former mentor [Toran Billups](https://github.com/toranb), but I digress.

# Why Linux?

In the past six years I've bounced between being a web app developer on Windows and MacOS. It should go without saying that Windows has given me numerous struggles, especially in an enterprise software environment.

Recently we hit a wall. Ember would take over ten minutes to build and the more complicated apps were closer to twenty-five minutes. I've been not only throwing away countless development hours watching slow builds and build failures, but worse yet it's been causing burnout.

So we flipped the desk. I chose Linux over MacOS because, well, I'd hoped it would be fun and different... it has been!

## The Result

![Dracula themed terminal prompt](/images/posts/deving_on_linux_is_fun.png)

Put simply, I'm finally able to use the tools that even on MacOS didn't run well. I was able to refer back to [my previous articles on writing dotfiles](https://wrotenwrites.com/a_modern_terminal_workflow_1/) while making adjustments for the platform, the fact that it's 2018, and to change things up just a little. I find it beautiful and familiar.

### Terminal — Hyper

I push my terminal a little, but not too hard. As a visual person doing web development, [Hyper](https://wrotenwrites.com/a_modern_terminal_workflow_1/) is perfect for me.

It feels lightning quick on my linux box and is simply gorgeous with [dracula theme](https://draculatheme.com/hyper/) applied. I followed their "Install using config file" instructions while manually git cloning [the repo](https://github.com/dracula/hyper) for Hyper to find. The configuration is a `.js` file which is bonus points for me.

### Shell — Fish

[Previously I recommended using Zsh](https://wrotenwrites.com/a_modern_terminal_workflow_3/) with a bunch of customizations. Now, I just [install Fish](https://fishshell.com/) which is configured nicely right out of the box.

An [unofficial dracula theme](https://github.com/nesl247/fish-theme-dracula) is available as well! I kept the prompt it comes with too which is nice.

### NeoVim and Tmux

Overall I'm still rocking the same [NeoVim setup](https://wrotenwrites.com/a_modern_terminal_workflow_2/) and [Tmux setup](https://wrotenwrites.com/a_modern_terminal_workflow_4/) I've recommended in the past. Some personal minor adjustments like `number relativenumber` which is a new favorite vim config of mine, and I'm pretty satisfied with it.

