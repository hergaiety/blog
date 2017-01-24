---
title: A Modern Terminal Workflow — Part 4 / 5
subtitle: Configuring Tmux
date: 2017/01/30
tags:
  - Dotfiles
  - Devtools
  - Tmux
---

## Fix Copy to Global Clipboard

``` vim tmux.conf
set -g default-shell $SHELL
set -g default-command 'reattach-to-user-namespace -l ${SHELL}'
```

On later versions of OSX accessing the system clipboard from within tmux became problematic. This command resolves that issue utilizing the `reattach-to-user-namespace` tool we already installed in our `init.sh`.

## Tabs

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

``` vim tmux.conf
bind \ split-window -h
bind | split-window -h -c '#{pane_current_path}'
bind - split-window
bind _ split-window -c '#{pane_current_path}'<Paste>
```

A small tweak on the community “standard” pane splitting hotkeys.

* Ctrl b \` to open new vertical split
* `Ctrl b |` to open new vertical split in current directory
* `Ctrl b -` to open new horizontal split
* `Ctrl b _` to open new horizontal split in current directory


# Plugins

## Plugin Manager

``` bash Terminal
git remote add -f tpm https://github.com/tmux-plugins/tpm.git
git subtree add --prefix=tpm tpm master --squash
```

With tpm (Tmux Package Manager) installed we can now initialize it in our Tmux Config.

``` vim tmux.conf
set -g @plugin 'tmux-plugins/tpm'
# PLUGINS GO HERE!!!
run '~/dotfiles/tpm/tpm'
```

### To Install Plugins

``` Terminal
tmux source ~/.tmux.conf
```

` Ctrl b I` will install any newly added plugins.

## Moving Panes

``` vim tmux.conf plugin path
set -g @plugin 'christoomey/vim-tmux-navigator'
```

Now you have vim-like movement between tmux splits.

* `Ctrl h, j, k, or l` to switch to split left/down/up/right

## Sensible Defaults

``` vim tmux.conf plugin path
set -g @plugin 'tmux-plugins/tmux-sensible
```

Among other things, this corrects rendering nvim in color through thus, removes the escape key delay, configures utf8, and more.

## Theme: Powerline Yellow

``` vim tmux.conf plugin path
set -g @themepack 'block/yellow'
set -g @plugin 'jimeh/tmux-themepack'
```

Much like vim-airline, this will give out lower tmux statusbar that powerline look. I've chosen gray but there are other [options](https://github.com/jimeh/tmux-themepack) as well.

# What’s Next
Part 5 will cover configuring iTerm2.

{% post_path a_modern_terminal_workflow_5 %}
