---
title: A Modern Terminal Workflow — Part 3 / 5
subtitle: Configuring Zsh
date: 2017/29/19
tags:
  - Dotfiles
  - Devtools
  - Zsh
---

TK Why Zsh?

## Zsh Config

``` bash Terminal
nvim zshrc
```

### Enabling Color Prompts

``` vim zshrc
autoload colors zsh/terminfo
colors
```

### Minimal Prompt

TK Example Image.

``` vim zshrc
precmd() { print "" }
PS1="⟩"
RPS1="%{$fg[magenta]%}%20<...<%~%<<%{$reset_color%}"
```

TK Why.

TK Right PS1.

### Autostart Tmux

``` vim zshrc
if [ "$TMUX" = "" ]; then tmux; fi
```

TK Why.

### Auto CD

``` vim zshrc
setopt auto_cd
```

A wise man once said, we only have so many keystrokes in our lives. With this simple command we can eliminate 3 common ones, cd. Now when you type a directory name or filepath and press enter the cd command is assumed.

### Spellcheck / Typo Correction

``` vim zshrc
setopt correctall
alias git status='nocorrect git status'
```

Zsh has some powerful typo correction capabilities. This is less annoying than it sounds and I love the time it saves me when I mistype a long command.
It does, however, mistake `git status` as a typo — so an alias is included to correct this behavior.

## Plugins


## Package Manager

``` vim zshrc
if [[ ! -f ~/.antigen.zsh ]]; then
  curl https://raw.githubusercontent.com/zsh-users/antigen/master/antigen.zsh > ~/.antigen.zsh
fi
source ~/.antigen.zsh
```

### Syntax Highlighting

``` vim zshrc
antigen bundle zsh-users/zsh-syntax-highlighting
```

Our code has syntax highlighting, why not our prompt? This package highlights valid and invalid commands as you’d expect. It’s amazing this isn’t built in functionality.

### Autocomplete

``` vim zshrc
antigen bundle zsh-users/zsh-autosuggestions
```

Once again, our code has autocomplete, why not our prompt? Repeat previously typed commands with ease.

### Git Shorthand

``` vim zshrc
antigen bundle git
```

This plugin includes a lot of powerful shorthands for git. The easiest to remember and one I use most often is simply shortening `git` to `g`.

# What’s Next
Part 4 will cover configuring Tmux.

{% post_path a_modern_terminal_workflow_4 %}
