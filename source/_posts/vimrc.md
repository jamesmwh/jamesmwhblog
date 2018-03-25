---
title: vimrc
date: 2017-08-24 13:40:41
tags:
---
" All system-wide defaults are set in $VIMRUNTIME/debian.vim and sourced by
" the call to :runtime you can find below.  If you wish to change any of those
<!-- more --> 
" settings, you should do it in this file (/etc/vim/vimrc), since debian.vim
" will be overwritten everytime an upgrade of the vim packages is performed.
" It is recommended to make changes after sourcing debian.vim since it alters
" the value of the 'compatible' option.
" This line should not be removed as it ensures that various options are
" properly set to work with the Vim-related packages available in Debian.
runtime! debian.vim
" Uncomment the next line to make Vim more Vi-compatible
" NOTE: debian.vim sets 'nocompatible'.  Setting 'compatible' changes numerous
" options, so any other options should be set AFTER setting 'compatible'.
"set compatible

" Vim5 and later versions support syntax highlighting. Uncommenting the next
" line enables syntax highlighting by default.
if has("syntax")
  syntax on
endif

" If using a dark background within the editing area and syntax highlighting
" turn on this option as well
"set background=dark

" Uncomment the following to have Vim jump to the last position when
" reopening a file
"if has("autocmd")
"  au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
"endif

" Uncomment the following to have Vim load indentation rules and plugins
" according to the detected filetype.
"if has("autocmd")
"  filetype plugin indent on
"endif

" The following are commented out as they cause vim to behave a lot
" differently from regular Vi. They are highly recommended though.
"set showcmd		" Show (partial) command in status line.
"set showmatch		" Show matching brackets.
"set ignorecase		" Do case insensitive matching
"set smartcase		" Do smart case matching
"set incsearch		" Incremental search
"set autowrite		" Automatically save before commands like :next and :make
"set hidden		" Hide buffers when they are abandoned
"set mouse=a		" Enable mouse usage (all modes)

" Source a global configuration file if available
if filereadable("/etc/vim/vimrc.local")
  source /etc/vim/vimrc.local
endif
set nu
set tabstop=2
set softtabstop=2
set shiftwidth=2
set number
set laststatus=2
set cursorline
set showcmd
set scrolloff=3
set ruler
set mouse=a
set selection=exclusive
set selectmode=mouse,key
set autoindent
set completeopt=preview,menu
syntax enable
set background=dark
colorscheme molokai

:inoremap ( ()<ESC>i
:inoremap ) <c-r>=ClosePair(')')<CR>
:inoremap { {<CR>}<ESC>i<CR><ESC>ki<TAB><TAB>
:inoremap } <c-r>=ClosePair('}')<CR>
:inoremap [ []<ESC>i
:inoremap ] <c-r>=ClosePair(']')<CR>
:inoremap " ""<ESC>i
:inoremap ' ''<ESC>i
function! ClosePair(char)
		if getline('.')[col('.') - 1] == a:char
			return "\<Right>"
		else
			return a:char
		endif
endfunction
filetype plugin indent on
set completeopt=longest,menu

set nocompatible               " be iMproved
filetype off                   " required!
 
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()
 
" let Vundle manage Vundle
" required!
Bundle 'gmarik/vundle'
 
" My Bundles here:
"
" original repos on github
Bundle 'tpope/vim-fugitive'
Bundle 'Lokaltog/vim-easymotion'
Bundle 'Lokaltog/vim-powerline'
Bundle 'tpope/vim-commentary'
Bundle 'scrooloose/nerdtree'
Bundle 'scrooloose/nerdcommenter'
Bundle 'terryma/vim-multiple-cursors'
Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
Bundle 'tpope/vim-rails.git'
" vim-scripts repos
Bundle 'L9'
Bundle 'FuzzyFinder'
" non github repos
Bundle 'git://git.wincent.com/command-t.git'
" ...
 
filetype plugin indent on     " required!
"
" Brief help  -- 此处后面都是vundle的使用命令
" :BundleList          - list configured bundles
" :BundleInstall(!)    - install(update) bundles
" :BundleSearch(!) foo - search(or refresh cache first) for foo
" :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
"
" see :h vundle for more details or wiki for FAQ
" NOTE: comments after Bundle command are not allowed..
"
" vim-powerline plugin
""set laststatus=2
""set t_Co=256
""let g:Powerline_symbols = 'unicode'
""set encoding=utf8
set guifont=PowerlineSymbols\ for\ Powerline
set nocompatible
set t_Co=256
"let g:Powerline_symbols = 'unicode'

" nerdtree plugin
nmap <F2> :NERDTreeToggle<cr>
let mapleader=","
" REQUIRED. This makes vim invoke Latex-Suite when you open a tex file.
filetype plugin on

" IMPORTANT: win32 users will need to have 'shellslash' set so that latex
" can be called correctly.
set shellslash

" IMPORTANT: grep will sometimes skip displaying the file name if you
" search in a singe file. This will confuse Latex-Suite. Set your grep
" program to always generate a file-name.
set grepprg=grep\ -nH\ $*

" OPTIONAL: This enables automatic indentation as you type.
filetype indent on

" OPTIONAL: Starting with Vim 7, the filetype of empty .tex files defaults to
" 'plaintex' instead of 'tex', which results in vim-latex not being loaded.
" The following changes the default filetype back to 'tex':
let g:tex_flavor='latex'

:inoremap #head #include<iostream> <CR>#include<cmath> <CR>#include<cstdlib><CR>#include "MathGL.h"<CR>static double tol = 10e-8;<CR><CR>using namespace std;<CR><CR>
:inoremap #init int main(int argc, char *argv[])<CR>{<CR>return 0;<CR>}<ESC>ki<CR><CR><ESC>kki<TAB>
:inoremap #plot double high[2] = {1.0, 1.0};<CR>double low[2] = {-1.0, -1.0};<CR>mglInitDrawingArea(low[0], low[1], high[0], high[1]);<CR>mglInitialization(argc, argv);<CR><CR><CR>mglFlush();
:inoremap fori for(int i = 0; i < n; i++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap forj for(int j = 0; j < n; j++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap fork for(int k = 0; k < n; k++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap forp for(int p = 0; p < n; p++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap forq for(int q = 0; q < n; q++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap fort for(int t = 0; t < n; t++){<CR>}<ESC>i<CR><ESC>ki<TAB>

:inoremap for1i for(int i = 1; i <= n; i++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap for1j for(int j = 1; j <= n; j++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap for1k for(int k = 1; k <= n; k++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap for1p for(int p = 1; p <= n; p++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap for1q for(int q = 1; q <= n; q++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap for1t for(int t = 1; t <= n; t++){<CR>}<ESC>i<CR><ESC>ki<TAB>
:inoremap :// //----------------------------------------
:inoremap :sp cout<<"-----------set point-------------"<<endl;


