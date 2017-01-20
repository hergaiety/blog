---
title: A Modern Terminal Workflow — Part 1 / 5
subtitle: Conquer the CLI using the latest tools made by developers for developers.
date: 2017/01/19
tags:
    - Devtools
---

Perhaps you’re a tinkerer, a javascript ninja, or something else entirely it’s essential to have tools that help you do what you do best and look good doing it.

This is an opinionated walkthrough using tools both new and old that are performant and work well together. Through a combination of Git, NeoVim, Zsh, Tmux and iTerm2 this article will take you step by step in writing a dotfiles repo to set up a MacOS programming environment.

Optionally, skip ahead and [see the final result](https://github.com/sharpshark28/modern-terminal-workflow).

## What is a Dotfiles repo?

A dotfile is simply a file that begins with a `.` before the filename such as `.vimrc`. These are commonly program configurations.

Git can host dotfiles and setup scripts to set up a new machine with your tools configured exactly the way you want them. An ideal setup script can be run after a fresh clone of the git repo to symlink its configuration dotfiles with the host machine for a portable terminal workflow.

## Getting Started

### Updating Xcode

Before we get started, ensure Xcode is up to date. It’s an easy step to miss and takes some time but is *essential for NeoVim to build*.

1. Update Xcode to the latest version using the appstore.
2. `xcode-select --install` to install xcode’s cli tools.

### Creating the local Git Repo

``` bash Terminal
mkdir ~/dotfiles # make a new dotfiles directory
cd ~/dotfiles # enter the new dotfiles directory
git init # ready the directory for git version control
touch init.sh zshrc tmux.conf vimrc # creating the config files
```

## The Initialize Script

Like many Git projects a starting point is required. Through an init shell script a series of commands can be written in a way that can be reproduced on as many machines as desired.

``` bash Terminal
vim init.sh
```

### Bash Script

A shell script needs an interpreter. We will be installing Zsh later in this script, but MacOS will be running Bash out of the box and thus that is what we will set the interpreter as.

``` bash init.sh
#!/bin/bash
```

## Creating Necessary Directories

NeoVim expects a few directories to exist and so it’s best we add them now.

``` bash init.sh
mkdir -p ~/.config ~/.config/nvim
```

### Installing System Dependencies

Throughout this walkthrough we’ll be installing package managers of varying types. Luckily here we can leverage a MacOS built in tool called Brew which does just this. Brew knows how to find, download, and install CLI applications out of the box and with the addition of an additional tool called Cask it can install GUI applications as well.

``` bash init.sh
brew install zsh tmux neovim/neovim/neovim python3 ag reattach-to-user-namespace
brew tap caskroom/cask
brew cask install iterm2
```

* **Zsh** is a powerful shell and an alternative to MacOS’s default Bash. This will be covered in more detail in part 3.
* **Tmux** is a terminal multiplexer. Using some keyboard hotkeys you can use tabs and split panes for better multitasking.
* **NeoVim** is a modern alternative to Vim, a terminal based code editor with efficiency and code reading in mind. This will be covered in more detail in part 2. NeoVim has a strange path due to being in active development at the moment.
* **Python** is installed to extend NeoVim’s plugin support.
* **Ag** is a code-searching tool similar to Ack but faster. This will be covered more in part 2.
* **Reattach-to-user-namespace** is a MacOS Sierra fix to ensure the workflow has access to the clipboard so share copy and paste functionality as one would expect in the correct namespace.
* **iTerm2** is a terminal replacement with a great level of customizability and integration with Tmux.

### Upgrading NeoVim to Have Python Support

``` bash init.sh
pip3 install neovim
```

## Installing Fonts

Brew's Cask capability can be extended to allowing the installation of fonts to the filesystem. 

There are many programmer fonts available to choose from, but _Fira Code has stolen my heart_ to the point of it being used on this very blog article. Monospaced fonts are ideal for programming because every character is the same width meaning code naturally aligns vertically. Fira Code is designed with programming ligatures making commonly used operators combine together into a single symbol. => <= `=> =<`

``` bash init.sh
brew tap caskroom/fonts
brew cask install font-fira-code
```

## Setting ZSH as Default Shell

``` bash init.sh
chsh -s /usr/local/bin/zsh
```

## Setting Configs

### Removing Any Existing Configs

Some cleanup in case these files already exist.

``` bash init.sh
rm ~/.zshrc ~/.tmux.conf ~/.config/nvim/init.vim 2> /dev/null
```

### Linking Configs

Symlinks can allow the file system point from where configs are expected to be to this repo.

``` bash init.sh
ln -s ~/dotfiles/zshrc ~/.zshrc
ln -s ~/dotfiles/tmux.conf ~/.tmux.conf
ln -s ~/dotfiles/vimrc ~/.config/nvim/init.vim
```

## Wrapping Up

1. Run your newly written init.sh with `bash init.sh` and then log out.
2. Upon logging back in, launch iTerm2.

We’re now running in Zsh and instead of vim we can use `nvim`.

> Optionally `vim` can launch `nvim` if you add `alias vim="nvim"` to your init.sh

# What’s Next
Part 2 will cover configuring NeoVim.

{% post_path a_modern_terminal_workflow_2 %}
