---
title: A Modern Terminal Workflow — Part 3 / 5
description: Configuring Zsh
date: 2017/02/10
tags:
  - Dotfiles
  - Devtools
  - Zsh
---

Zsh is a UNIX command interpreter alternative to the default Mac OS shell Bash. Someone who knows Bash already knows the basics of Zsh.

**So then why?** Zsh is increasing in popularity with those who want more from their terminal. Zsh offers features like syntax highlighting, variables, history commands and other advanced features outside the scope of this article. I install it for the customization potential it offers and appreciate that I can grow to [learn new features over time](https://www-s.acm.illinois.edu/workshops/zsh/why.html).

# Config

In part 1 the init script set Zsh as the default shell by running `chsh -s /usr/local/bin/zsh`. The next time you log in Zsh is the new default. Or running `zsh` will launch the Zsh shell.

`nvim zshrc`

## Enabling Color Prompts

##### Note: Syntax highlighting and color may not work as expected within Tmux until it is configured in Part 4 correctly.

Enabling color is an important first step.

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

## Autostart Tmux

The command below does a simple check to confirm Tmux is installed before attempting to run it automatically.

``` vim zshrc
if [ "$TMUX" = "" ]; then tmux; fi
```

In part 4 Tmux will be discussed in greater detail. For now, know that running it only enhances the possibilities so there is no reason not to autostart Zsh running with Tmux. iTerm2, which will be discused in Part 5, also plays explicitly supports Tmux.


If you instead desire to run Tmux manually you may do so by running the `tmux` command at any point.

## Auto CD

``` vim zshrc
setopt auto_cd
```

A wise man once said, we only have so many keystrokes in our lives. With this simple command we can eliminate 3 of the most common ones, `cd<space>`. Now when you type a directory name or filepath and press enter the cd command is assumed.

## Spellcheck / Typo Correction

``` vim zshrc
setopt correctall
alias git status='nocorrect git status'
```

Zsh has some powerful typo correction capabilities. This is less annoying than it sounds and I love the time it saves me when I mistype a long command.

It does, however, mistake `git status` as a typo. An alias is included above to correct this behavior.

# Plugins to Enhance Functionality

## Package Manager

Stock Zsh behaves as you'd expect it to. But why stop there? Installing plugins to Zsh can enhance its base functionality with very little overhead.

``` vim zshrc
if [[ ! -f ~/.antigen.zsh ]]; then
  curl https://raw.githubusercontent.com/zsh-users/antigen/master/antigen.zsh > ~/.antigen.zsh
fi
source ~/.antigen.zsh
```

Above is the configuration to `curl` the plugin manager antigen which will make installing plugins a breeze.

## Syntax Highlighting

``` vim zshrc
antigen bundle zsh-users/zsh-syntax-highlighting
```

Code has syntax highlighting, why doesnt the terminal prompt? This package highlights valid and invalid commands as one would expect. It’s amazing this isn’t built in functionality.

[Learn More](https://github.com/zsh-users/zsh-syntax-highlighting)

## Autocomplete

``` vim zshrc
antigen bundle zsh-users/zsh-autosuggestions
```

Once again, code has autocomplete, why not the terminal prompt? Allows for repeating previously typed commands with ease.

[Learn More](https://github.com/zsh-users/zsh-autosuggestions)

## Git Shorthand

``` vim zshrc
antigen bundle git
```

This plugin includes a lot of powerful shorthands for git. The easiest to remember and one I use most often is simply shortening `git` to `g`.

# What’s Next
Part 4 will cover configuring Tmux.

{% post_link a_modern_terminal_workflow_4 %}
