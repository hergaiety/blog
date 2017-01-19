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

* *Zsh* is a powerful shell and an alternative to MacOS’s default Bash. This will be covered in more detail in part 3.
* *NeoVim* is a modern alternative to Vim TK. This will be covered in more detail in part 2. NeoVim has a strange path due to being in active development at the moment.
* *iTerm2* TK
* *Tmux* TK
* *Ag* is a code-searching tool similar to Ack but faster and will be covered more in the next article.
* *Reattach-to-user-namespace* is a MacOS Sierra fix to ensure the workflow has access to the clipboard so share copy and paste functionality as one would expect in the correct namespace.
* *Python* is installed to extend NeoVim’s plugin support.

### Upgrading NeoVim to Have Python Support

``` bash init.sh
pip3 install neovim
```

## Installing Fonts

``` bash init.sh
brew tap caskroom/fonts
brew cask install font-fira-code
```

...TK...

``` bash init.sh
echo "-= Setting Zsh as default shell =-"
chsh -s /usr/local/bin/zsh
echo "-= Removing any existing configs =-"
rm ~/.zshrc ~/.tmux.conf ~/.config/nvim/init.vim 2> /dev/null
echo "-= Symlinking new configs =-"
ln -s ~/dotfiles/zshrc ~/.zshrc
ln -s ~/dotfiles/tmux.conf ~/.tmux.conf
ln -s ~/dotfiles/vimrc ~/.config/nvim/init.vim
echo "-= Log out and Log Back In to see changes =-"
```

Run your newly written init.sh with bash init.sh and then log out. Upon logging back in, launch iTerm2. We’re now running in Zsh and instead of vim we can use `nvim`.

TK how to alias nvim to vim

# What’s Next
Part 2 will cover configuring NeoVim. TK
