---
title: A Modern Terminal Workflow — Part 2 / 5
subtitle: Configuring Neovim
date: 2017/01/24
tags:
  - Dotfiles
  - Devtools
  - NeoVim
  - Vim
---

[Vim is about precision editing at the speed of thought](https://vimeo.com/53144573). Vim is also about quickly navigating a project to find and read old code.

> Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. ...[Therefore,] making it easy to read makes it easier to write.
> ― _Robert C. Martin, Clean Code: A Handbook of Agile Software Craftsmanship_

NeoVim is a modern drop-in replacement for Vim. In fact it is easy to share a Vim config with NeoVim via a symlink, but there are some caveats which are outside the scope of this article.

# Core Config

##### Note: Syntax highlighting and color may not work as expected within Tmux until it is configured in Part 4 correctly.

There’s a certain magic to writing your editor config with that very same editor. I suggest handwriting these configs so you can learn as you type.

`nvim vimrc`

## Setting Sensible Defaults

``` vim vimrc
" Set standard file encoding
set encoding=utf8
" No special per file vim override configs
set nomodeline
" Stop word wrapping
set nowrap
  " Except... on Markdown. That's good stuff.
  autocmd FileType markdown setlocal wrap
" Adjust system undo levels
set undolevels=100
" Use system clipboard
set clipboard=unnamed
" Set tab width and convert tabs to spaces
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab
" Don't let Vim hide characters or make loud dings
set conceallevel=1
set noerrorbells
" Number gutter
set number
" Use search highlighting
set hlsearch
" Space above/beside cursor from screen edges
set scrolloff=1
set sidescrolloff=5
```

## Opinionated Defaults

### Remapping `<Leader>` to `<Space>`

``` vim vimrc
let mapleader="\<SPACE>"
```

The `<Leader>` key is what is pressed before another key to activate some command via a shortcut. By default Vim uses the rather awkward key `\`. Many respected Vim users choose `<Space>` as their leader key instead and I agree with this change.

### Disable mouse support

``` vim vimrc
set mouse=r
let $NVIM_TUI_ENABLE_CURSOR_SHAPE=1
```

These dotfiles are going to rock this world so hard we don't need mice where we're going. Keep those hands on the keyboard and power on.

### Setting Arrow Keys to Resize Panes

``` vim vimrc
nnoremap <Left> :vertical resize -1<CR>
nnoremap <Right> :vertical resize +1<CR>
nnoremap <Up> :resize -1<CR>
nnoremap <Down> :resize +1<CR>
" Disable arrow keys completely in Insert Mode
imap <up> <nop>
imap <down> <nop>
imap <left> <nop>
imap <right> <nop>
```

_This was the config best decision I ever made._ **Relying on arrow keys results in less efficient code editing.** Should you find this frustrating, turn those frustrations into learning experiences to find the quickest way to have the cursor reach the target.

## Dealing with Buffers / Tabs

### Return to the last file opened

``` vim vimrc
nmap <Leader><Leader> <c-^>
```

* `Space Space` to open previously opened file buffer

## Next / Previous Buffer (Tab)

``` vim vimrc
nnoremap <Tab> :bnext!<CR>
nnoremap <S-Tab> :bprev!<CR><Paste>
```

* `Tab` to switch to next buffer
* `Shift Tab` to switch to previous buffer

This keybinding becomes more intuitive after installing the plugin suggested below to convert buffers to onscreen tabs with vim-airline.

# Plugins to Enhance Functionality

## Plugin Manager

Stock, even heavily configured, Vim is lacking features offered by other GUI applications. While the objective is not to convert Vim into something it isn't it is essential to implement some missing functionality through plugins.

There are several plugin managers out there but vim-plug is the most minimal while being fast in uptime and concurrent plugin installation.

``` vim vimrc
call plug#begin('~/.local/share/nvim/plugged')
# PLUGINS GO HERE!!!
call plug#end()
```

### To Install Plugins

Between `call plug#begin` and `call plug#end` insert the keyword `Plug` followed by the path to the plugin in Github such as `Plug 'username/project`. See further examples in the suggested plugins below.

After adding a `Plug` and saving the vimrc file run the install command by hitting colon followed by `PlugInstall`.

``` vim 
:PlugInstall
```

## Unite

As stated earlier, Vim is not a GUI. Unite is a commonly used resource for plugins to open panels and other temporary interfaces onscreen. **Unite is required for many plugins to work as expected.**

``` vim vimrc plugin path
Plug 'Shougo/unite.vim'
```

## Theme: Dracula

``` vim vimrc plugin path
Plug 'dracula/vim'
```

Dracula is dark yet vibrant, needs no additional configuration, and is supported in a [wide variety of apps](https://draculatheme.com/) for a consistent experience.

``` vim vimrc plugin settings
color Dracula
```

## Indent Guides

``` vim vimrc plugin path
Plug 'Yggdroot/indentLine'
```

Indentation guides provide a subconcious way of understanding how your code fits together horizontally as well as assuring that indentation is correct at a glance.

``` vim vimrc plugin settings
let g:indentLine_enabled = 1
let g:indentLine_char = "⟩"
```

## Git Gutter

``` vim vimrc plugin path
Plug 'airblade/vim-gitgutter'
```

As code is added, modified, or removed a visual aid will be placed alongside the number gutter. gitgutter takes advantage of NeoVim's async capabilities to never slow you down.

## Tabs & a Status Bar

``` vim vimrc plugin path
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

Programming in vim can abstract away much of what's happening behind the scenes. In many ways, this is great — but visual reminders are useful for making day-to-day programming a nobrainer.

vim-airline is widely popular, and surprisingly beautiful, without making vim look too much like a GUI. This plugin and config will show **current mode, current file path, % scrolled through file, tabs for current buffers, and more.**

It automatically works with plugins it recognizes, such as CtrlP! _(Which we’ll install next…)_

``` vim vimrc plugin settings
let g:airline#extensions#tabline#enabled=1let g:airline_powerline_fonts=1
set laststatus=2
```

## Fuzzy Finder

``` vim vimrc plugin path
Plug 'ctrlpvim/ctrlp.vim', { 'on': 'CtrlP' }
```

**The quickest way to jump to a file in your project is with a fuzzy finder.** Similar experiences can be found in popular code editors like Atom.io or Sublime. With vim the same experience can be achieved at _lightning speeds when paired with Ag and NeoVim._ I've tried other fuzzy finders like fzf, but have found ctrlp to have the best experience and most reliable.

``` vim vimrc plugin settings
nnoremap <Leader>p :CtrlP<CR>
nnoremap <Leader>t :CtrlP<CR>
```

* `Space t` or `Space p` opens Fuzzy Finder

## Find in Files

``` vim vimrc plugin path
Plug 'mhinz/vim-grepper'
```

**Sometimes you just need to find some text somewhere in your project.** The Silver Searcher, also known as Ag does just this and it does so very quickly. Grepper uses Ag’s speed combined with NeoVim’s async abilities to provide a fast way to find code anywhere in your project or buffers.

``` vim vimrc plugin settings
nnoremap <Leader>fp :Grepper<Space>-query<Space>
nnoremap <Leader>fb :Grepper<Space>-buffers<Space>-query<Space>-<Space>
```

* `Space f p` to type a search to find matches in entire **p**roject
* `Space f b` to type a search to find matches in current **b**uffers

## Project as File Tree

``` vim vimrc plugin path
Plug 'Shougo/vimfiler.vim', { 'on': 'VimFiler' }
```

While _not_ my preferred way to navigate a project, it's handy to have a file tree to see directory structure and browse for a file manually.

``` vim vimrc plugin settings
map ` :VimFiler -explorer<CR>
map ~ :VimFilerCurrentDir -explorer -find<CR>
```

* `Space backtick` to toggle File Tree
* `Space ~` to open File Tree from current buffer’s directory

## Autocomplete

``` vim vimrc plugin path
Plug 'Shougo/deoplete.nvim', { 'do': ':UpdateRemotePlugins' }
```

A pretty standard feature of many code editors, an async dropdown tabbable suggestion menu as you type.

``` vim vimrc plugin settings
let g:deoplete#enable_at_startup = 1
inoremap <expr><tab> pumvisible() ? "\<c-n>" : "\<tab>"
```

## Linting

``` vim vimrc plugin path
Plug 'w0rp/ale'
```

Async as you type code linting at its finest. Zero config needed.

## Sneaking — Efficient Moving

``` vim vimrc plugin path
Plug 'justinmk/vim-sneak'
```

The secret to never needing to `wwwww`, or worse `lllll` is learning how to Sneak around your code. Efficient targeting comes from understanding where you want to jump to and pressing the appropriate sneak keys to get there. Key bindings listed below.

``` vim vimrc plugin settings
let g:sneak#s_next = 1
nmap f <Plug>Sneak_f
nmap F <Plug>Sneak_F
xmap f <Plug>Sneak_f
xmap F <Plug>Sneak_F
omap f <Plug>Sneak_f
omap F <Plug>Sneak_F
```

* `f <key>` to jump to next `<key>`
* `F <key>` to jump to previous `<key>`
* `f` to following match
* `s <key><key>` to jump to next `<key><key>`
* `S <key><key>` to jump to previous `<key><key>`
* `s` to following match

# Language Specific

The web is a very diverse space. I suggest searching [VimAwesome](http://vimawesome.com/) for the languages you program in most often to find what plugins may assist you personally.

# What’s Next

Part 3 will cover configuring Zsh.

{% post_link a_modern_terminal_workflow_3 %}
