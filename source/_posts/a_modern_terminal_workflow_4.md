---
title: A Modern Terminal Workflow — Part 4 / 5
description: Configuring Tmux
date: 2017/02/20
tags:
  - Dotfiles
  - Devtools
  - Tmux
---

Multiplexing the terminal, huh? Tmux is a simple yet powerful way to work with multiple terminal based programs simultaniously. With Tmux one can ditch the mouse and use keyboard shortcuts to split panes and navigate between tabs of terminal workspaces making anyone a multitasking terminal master.

Tmux was installed in Part 1 of this guide and its dotfile config can be modified with NeoVim like so `nvim tmux.conf`.

# Config

## Fix Copy to Global Clipboard

_Bah! This article starts with a fix?_

On later versions of OSX accessing the system clipboard from within tmux became problematic. This command resolves that issue utilizing the `reattach-to-user-namespace` tool already installed in `init.sh`.

``` vim tmux.conf
set -g default-shell $SHELL
set -g default-command 'reattach-to-user-namespace -l ${SHELL}'
```

## Tabs

The obvious way to multitask is with tabs. It's a great place to get started. These keybindings will make working with them more intuitive.

``` vim tmux.conf
set -g status-position top
set -g base-index 1
set -g pane-base-index 1
set -g renumber-windows on
bind-key -n C-t new-window
bind-key -n C-T new-window -c "#{pane_current_path}"
bind-key -n C-w kill-pane
```

* `Ctrl t` to open new tab
* `Ctrl T` to open new tab in same directory
* `Ctrl w` to close a pane (and tab if only one pane)

## Create Panes

A single tab can be split into multiple panes. Mastering panes not only makes the user look like a total terminal professional but can really boost efficiency. Combined with NeoVim this is as close as it gets to having your terminal act like the best parts of an IDE.

``` vim tmux.conf
bind \ split-window -h
bind | split-window -h -c '#{pane_current_path}'
bind - split-window
bind _ split-window -c '#{pane_current_path}'
```

A small tweak on the community “standard” pane splitting hotkeys.

* `Ctrl b \` to open new vertical split
* `Ctrl b |` to open new vertical split in current directory
* `Ctrl b -` to open new horizontal split
* `Ctrl b _` to open new horizontal split in current directory

# Plugins

## Plugin Manager

Unlike in previous parts of this series there isn't much to extend in terms of functionality for Tmux. However, to get the most out of Tmux it's ideal to install some well defined community made configurations.

Adding a plugin manager to Tmux is as easy as installing tpm (Tmux Package Manager) via the Terminal. This can be done with git subtrees so that when these dotfiles are cloned to other machines in the future tpm is ready to go.

``` bash Terminal
git remote add -f tpm https://github.com/tmux-plugins/tpm.git
git subtree add --prefix=tpm tpm master --squash
```

With tpm installed we can now initialize it in our Tmux Config.

``` vim tmux.conf
set -g @plugin 'tmux-plugins/tpm'
# PLUGINS GO HERE!!!
run '~/dotfiles/tpm/tpm'
```

### To Install Plugins

``` bash Terminal
tmux source ~/.tmux.conf
```

`Ctrl b I` will install any newly added plugins. A prompt will appear at the top of the terminal to show installation progress.

## Sensible Defaults

``` vim tmux.conf plugin path
set -g @plugin 'tmux-plugins/tmux-sensible
```

This corrects rendering NeoVim in color through Tmux, removes the escape key delay, configures utf8, and more.

## Moving Panes

Splitting and removing panes is easy, but what about moving between them? What if there are NeoVim panes open as well as Tmux panes?

``` vim tmux.conf plugin path
set -g @plugin 'christoomey/vim-tmux-navigator'
```

With this simple plugin this new concern is no longer. Moving between NeoVim and Tmux panes now use the same shortcuts.

* `Ctrl h, j, k, or l` to switch to split left, down, up, right

## Theme: Powerline Yellow

``` vim tmux.conf plugin path
set -g @themepack 'block/yellow'
set -g @plugin 'jimeh/tmux-themepack'
```

Much like vim-airline, this will give out lower tmux statusbar that powerline look. I've chosen gray but there are other [options](https://github.com/jimeh/tmux-themepack).

# What’s Next
Part 5 will cover configuring iTerm2.

{% post_link a_modern_terminal_workflow_5 %}
