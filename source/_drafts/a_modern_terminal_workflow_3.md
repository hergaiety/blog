---
title: A Modern Terminal Workflow — Part 3 / 5
subtitle: Configuring Zsh
date: 2017/03/02
tags:
  - Dotfiles
  - Devtools
  - Zsh
---

Zsh is a UNIX command interpreter alternative to the default Mac OS shell Bash. Someone who knows Bash already knows the basics of Zsh.

**So then why?** Zsh is increasing in popularity from those who want more from their terminal. Zsh offers features like syntax highlighting, variables, history commands and other advanced features outside the scope of this article. I install it for the customization potential it offers and like that I can grow to [learn new features over time](https://www-s.acm.illinois.edu/workshops/zsh/why.html).

# Config

In part 1 the init script set Zsh as the default shell by running `chsh -s /usr/local/bin/zsh`. Logging out then back in will begin using Zsh by default or the command `zsh` will launch the Zsh shell.

`nvim zshrc`

## Enabling Color Prompts

##### Note: Syntax highlighting and color may not work as expected within Tmux until it is configured in Part 4 correctly.

Enabling color is an essential but important first step.

``` vim zshrc
autoload colors zsh/terminfo
colors
```

## Minimal Prompt

> This is my [Prompt]. There are many like it but this one is mine.

Example:

![Prompt Example](/images/posts/a_modern_terminal_workflow_3_prompt.png)

``` vim zshrc
precmd() { print "" }
PS1="⟩"
RPS1="%{$fg[magenta]%}%20<...<%~%<<%{$reset_color%}"
```

A prompt can be a place to put a lot of information at a glance. I'm of the opinion that information belongs hidden behind commands and called upon as needed.

This prompt consists of an empty line placed above the prompt to separate it from finished commands. The left prompt (PS1) is simply a right arrow character showing where a command can be typed. The right prompt (RPS1) is an ellipsis shortened version showing up to 20 characters from the right of the current path.

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
