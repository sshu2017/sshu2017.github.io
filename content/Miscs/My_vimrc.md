title: The .vimrc File I Use and Love
date: 2020-06-10
author: sshu

I started using Vim as my major code editor in 2017, when I started my current job as a Data Scientist at [PointPredictive Inc.](https://pointpredictive.com/){:target="_blank"}, because the job requires me to SSH into remote Linux servers and edit Python and Bash scripts in the terminal. To be precise, I started with Nano, which could let me get my job done. However I felt Nano is really inconvenient to use. So I decided to switch to Vim. The initial phase of using Vim is okay, not as horrible as many people have found, except that I DID go to stackoverflow to find out how to quit Vim (Ah yes, I was one of the [1 million people who had struggled](https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/){:target="_blank"}). As time went by, the more I played around with Vim , the more I realized how powerful and versatile it is, and the more I liked it.

After almost 3 years of using Vim, I finally have my .vimrc that I feel is good enough for me. And here it is.

```vimrc
set nocompatible
        filetype off
        set rtp+=~/.vim/bundle/vundle
        call vundle#rc()
        Bundle 'gmarik/vundle'
        Bundle 'jiangmiao/auto-pairs'
        Bundle 'Lokaltog/vim-powerline'
        Bundle 'scrooloose/nerdcommenter'
        Bundle 'tmhedberg/SimpylFold'
        Bundle 'Yggdroot/indentLine'
        Bundle 'scrooloose/syntastic'
        Bundle 'flazz/vim-colorschemes'
        Bundle 'scrooloose/nerdtree'
        Bundle 'RRethy/vim-illuminate'
        Bundle 'majutsushi/tagbar'
        Bundle 'psliwka/vim-smoothie'

set vb
let g:is_bash=1
set incsearch
set hlsearch
set bg=light
syntax on
set autoindent
set smartindent
set number
set relativenumber
hi clear
syntax enable
colorscheme monokai
set shiftwidth=4
set tabstop=4
set expandtab
set laststatus=2
set showmatch
set novisualbell
set cursorline
set guicursor+=n-v-c:blinkon0
let g:PyFlakeCheckers = 'pep8, mccabe, frosted'
let g:PyFlakeOnWrite = 1

```

