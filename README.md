# nnn.vim

File manager for vim/neovim powered by n³.

<p align="center">
  <img width="934" src="https://user-images.githubusercontent.com/7200153/77138110-8dd94600-6aab-11ea-925f-8e159b8f0ad4.png">
  <small>colorscheme <a href="https://github.com/pgdouyon/vim-yin-yang">yin</a></small>
</p>

### Requirements

1. n³
2. Neovim or Vim 8.1 with terminal support

### Install

n³ must be installed. Instructions
[here](https://github.com/jarun/nnn/wiki/Usage#installation).

Then install the plugin using your plugin manager:

```vim
" using vim-plug
Plug 'mcchrish/nnn.vim'
```

### Usage

To open n³ as a file picker in vim/neovim, use the command `:NnnPicker` or
`:Np` or the key-binding `<leader>n`. The command accepts an optional path
to open e.g. `:NnnPicker path/to/somewhere`.

Run the plugin, [select file(s)](https://github.com/jarun/nnn/wiki/concepts#selection)
and press <kbd>Enter</kbd> to quit the n³ window. Now vim will open the first
selected file and add the remaining files to the arg list/buffer list.

Pressing <kbd>Enter</kbd> on a file in n³ will pick any earlier selection, pick
the file and exit n³.

Note that pressing <kbd>l</kbd> or <kbd>Right</kbd> on a file would open it
instead of picking.

To discard selection and exit, press <kbd>^G</kbd>.

vim config `set hidden` may be required for the floating windows to work.

Complete plugin documentation - `:help nnn`.

### Configuration

#### Custom mappings

```vim
" Disable default mappings
let g:nnn#set_default_mappings = 0

" Set personalized mappings
nnoremap <silent> <leader>nn :NnnPicker<CR>


" OR override
" Start n³ in the current file's directory
nnoremap <leader>n :NnnPicker %:p:h<CR>
```

#### Layout

```vim
" Opens the n³ window in a split
let g:nnn#layout = 'new' " or vnew, tabnew etc.

" Or pass a dictionary with window size
let g:nnn#layout = { 'left': '~20%' } " or right, up, down

" Floating window (neovim latest and vim with patch 8.2.191)
let g:nnn#layout = { 'window': { 'width': 0.9, 'height': 0.6, 'highlight': 'Debug' } }
```

#### Action

It's possible to set extra key-bindings for opening files in various ways.
No default is set so that n³'s key-bindings are not overridden.

```vim
let g:nnn#action = {
      \ '<c-t>': 'tab split',
      \ '<c-x>': 'split',
      \ '<c-v>': 'vsplit' }
```

With the above example, when inside an n³ window, pressing <kbd>^T</kbd> will
open the selected file in a tab instead of the current window. <kbd>^X</kbd> will
open in a split an so on. Multi-selected files will be loaded in the buffer list.

#### Persistent session

n³ sessions can be used to remember the location when it is reopened.

```vim
" use the same n³ session within a vim session
let g:nnn#session = 'local'

" use the same n³ session everywhere (including outside vim)
let g:nnn#session = 'global'
```

Note: If desired, an n³ session can be disabled temporarily by passing
`session: false` as an option to `nnn#pick()`.

#### Command override

It's possible to override the default n³ command and add some extra program options.

```vim
" to start n³ in detail mode:
let g:nnn#command = 'nnn -d'

" OR, to pass env variables
let g:nnn#command = 'NNN_TRASH=1 nnn -d'
```

#### `nnn#pick()`

The `nnn#pick([<dir>][,<opts>])` function can be called with a custom directory
and additional options such as opening file in splits or tabs. It's a more
configurable version of the `:NnnPicker` command.

```vim
call nnn#pick('~/some-files', { 'edit': 'vertical split' })
" Then add custom mappings
```

`opts` can be:

- `edit` - type of window the select file will be open.
- `layout` - same as `g:nnn#layout` and overrides it if specified.

#### Environment variables

n³ will detect env variables defined in `vimrc`.

```vim
let $NNN_TRASH=1
```

#### Setup for `init.lua`

Use the same option names as you would in Vimscript, e.g.:

```lua
require('nnn').setup{
    set_default_mappings = false,
    session = 'global',
    layout = { left = '20%' }
}
```

### Credits

Main n³ program: https://github.com/jarun/nnn
