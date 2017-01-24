---
title: A Modern Terminal Workflow — Part 5 / 5
subtitle: Configuring iTerm2
date: 2017/02/01
tags:
  - Dotfiles
  - Devtools
  - Terminal
  - iTerm2
---

Open iTerm’s preferences with “⌘,” then tick the following settings:

1. “Load preferences from a custom folder or URL”
2. Choose ~/dotfiles
3. “Save changes to folder when iTerm2 quits”

## Use ZSH as Shell

1. Profiles tab
2. General sub-tab
3. Command: /usr/local/bin/zsh

## Theme: Dracula

``` bash Terminal
git remote add -f iterm-dracula https://github.com/dracula/iterm.git
git subtree add --prefix=iterm-dracula/ iterm-dracula master --squash
```

1. Profiles tab
2. Colors sub-tab
3. Color Presets…
4. Import…
5. ~/dotfiles/iterm-dracula/Dracula.itermcolors

## Font: Fira Code

Designers have logos, programmers have... well, frameworks and languages I suppose — but visually a great way to build a brand are our tools and our style. Themes are a great start, but it doesn't have to stop there. Our entire terminal is made up of text, so make that text look beautiful.

> Put simply: Fira Code is a free monospaced font with programming ligatures.

What does any of that mean? It's what you want for highly legible code and looking badass in the process.

**NOTE** _Currently the Fira Code font is only supported in [iTerm's nightly builds](https://www.iterm2.com/downloads/nightly/#/section/home) at the time of writing. Eventually this will simply be part of the final release._

1. Profiles tab
2. Text sub-tab
3. Change Font
4. Family: Fira Code (I enjoy size 18) (This is already installed if you ran init.sh)

## Cursor Guide

Even if you're so good at terminal that you never lose your cursor, do yourself a favor and turn on the cursor guide. Subconciously a gentle highlight of the current line will draw your eye right to where you need to be.

1. Profiles tab
2. Colors sub-tab
3. “Cursor Guide”
4. Set color (I prefer 255, 255, 255, 35)

## Tmux Tab Switching

A clever hack to enable `Ctrl Tab` and `Ctrl Shift Tab` tmux tab switching is to let iTerm handle those shortcuts, then send the default `Ctrl B n` and `Ctrl b p` hex codes to the terminal. This pairs well with Vim’s tabbing being the same but without holding Ctrl. (Special Thanks to [Dan Lowe](http://tangledhelix.com/blog/2012/04/28/iterm2-keymaps-for-tmux/))

1. Keys
2. New > “Ctrl Tab” > Send Hex Codes > 0x02 0x6E
3. New > “Ctrl Tab” > Send Hex Codes > 0x02 0x70

* `Ctrl Tab` to switch to next tmux tab
* `Ctrl Shift Tab` to switch to previous tmux tab

# Outro

TK
