## `.bash_profile`

```sh
export NVM_DIR="$HOME/.nvm"

. "/usr/local/opt/nvm/nvm.sh"

parse_git_branch() {
		git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\]\n$ "
export FZF_DEFAULT_OPTS='--height 40% --layout=reverse --border'
if [ -f ~/.git-completion.bash ]; then
	. ~/.git-completion.bash
fi

eval "$(direnv hook bash)"

export LSCOLORS="EHfxcxdxBxegecabagacad"
alias ll="ls -lGaf"
alias gst="git status"
alias init-soxhub="python3.7 ~/workspace/python-scripts/init-soxhub.py"
alias rm-swp="find . -type f -name \".*.swp\" -exec rm -f {} \\;"
alias ls-swp="find . -type f -name \".*.swp\""
alias shsource="source ~/.bash_profile"
alias shedit="vim ~/.bash_profile"

[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion
HISTSIZE=""

fortune | pokemonsay

alias tmux="TERM=screen-256color-bce tmux"

export PATH="$HOME/.cargo/bin:$PATH"

#echo "lock your computer" > "$HOME/Desktop/$(date)_read.txt"
```

## Install macvim

`brew install macvim --with-override-system-vim`

## `.vimrc`

```vim
execute pathogen#infect()
syntax on
filetype plugin indent on
" system clipboard yank
set clipboard=unnamed
let mapleader=","

" MAPPING
nmap <silent> <leader>ev :e $MYVIMRC<CR>
" maps ,sv to source .vimrc
nnoremap <leader>sv :source $MYVIMRC
" maps ; to :
nnoremap ; :
" clears search buffer when ,/
nmap <silent> ,/ :nohlsearch<CR>
" // will search that word
vnoremap // y/<C-R>"<CR>

" maps pane navigation to shortcut 
" ctrl-w + j => ctrl-j
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
inoremap jk <esc>`

" OPTIONS
" Add full file path to your existing statusline
set laststatus=2
" Indenting Options
set tabstop=2 shiftwidth=2
set copyindent " copy the previous line's indent

" Buffer Options
set hidden " hides buffers when they are unsaved and a new buffer is opened
" Syntax Options
"
set showmatch " show matching paranthesis
" Search Options
"
set history=1000 " larger search history
set ignorecase " ignore case when searching
set hlsearch " highlight search terms
set incsearch " show search matches as you type
set smartcase " ignore case if pattern is all lowercase only
set backspace=indent,eol,start " backspace everything in insert
set number
set undolevels=1000 " larger undo history
set wildignore=*.swp " ignore swp files
set clipboard=unnamed " yank will copy to system clipboard
set pastetoggle=<F5> " F5 in insert allows for pasting w/o indent
set mouse=a
" split panes down for vertical
" split panes right for horizontal
set splitbelow
set splitright

" NERDTREE
map <C-n> :NERDTreeToggle<CR>
let g:NERDTreeNodeDelimiter = "\u00a0"
 
" fzf
set rtp+=/usr/local/opt/fzf

" the silver searcher
let $FZF_DEFAULT_COMMAND = 'ag --hidden --ignore .git -l -g ""'
nnoremap <C-p> :Files<CR>
nnoremap <C-b> :Buffer<CR>
nnoremap <C-f> :Ag<CR>

" Fix tmux colorscheme issues
set background=dark
set t_Co=256
colorscheme wasabi256

" silver searcher preview window
" ? on silver searcher result to preview
" Navigate preview using shift + arrow key
command! -bang -nargs=* Ag
	\ call fzf#vim#ag(<q-args>,
	\					<bang>0 ? fzf#vim#with_preview('up:60%')
	\							: fzf#vim#with_preview('right:50%:hidden', '?'),
	\					<bang>0)
set noexpandtab
:%retab!			" Retabulate the whole file
```
