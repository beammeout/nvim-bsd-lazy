# Beamer's nvim config
Neovim config tested on FreeBSD with lazy plugin manager

## Pre-requisites
install `neovim`, `lua51`, `luarocks51` and `git`

### On OpenBSD
Installing luarocks with `pkg_add luarocks-lua51` is usually enough. It will also install various lua versions. You will be reminded to create the necessary simlinks for luarocks:
```
 ln -sf /usr/local/bin/luarocks-5.1 /usr/local/bin/luarocks
 ln -sf /usr/local/bin/luarocks-admin-5.1 /usr/local/bin/luarocks-admin
```
Do the same for lua, if the simlink was not automatically created:
```
ln -sf /usr/local/bin/lua51 /usr/local/bin/lua
```

### On FreeBSD
```
pkg install lua51 luarocks51
```
You might need to simlink lua51 to lua:
```
ln -s /usr/local/bin/lua51 /usr/local/bin/lua
```


## Getting started
- Backup your original nvim configuration in `~/.confing/nvim/` !
- Clone this repo to your nvim config folder `git clone https://github.com/beammeout/nvim-bsd-lazy.git ~/.config/nvim`.
- Upon nvim start Lazy screen should popup, and offer you sync and install for all the plugins.
- Any errors will appear in the lazy nvim popup.
- Tom make sure if everything works run `:checkhealth` after nvim start. Scroll through the list and check for ERRORS.

# Limitations
- Mason plugin for LSP installation by typing `:Mason` is not supported on *BSD systems. I'm keeping for folks that want to use this on Linux. Read more in this [issue](https://github.com/mason-org/mason.nvim/issues/382) 
- Some language servers can be compiled manually, others won't work at all.
- As long as the LSP is in the PATH and is executable, it should work.
- Keeping in mind that some neovim plugins are only tested on Linux, MacOs and sometimes Windows. Some weird behaviour is possible.

# Native nvim lsp
Instead of nvim-lspconfig, it is now recommended to use native nvim lsp config. More here:
[nvim-lspconfig migration](https://github.com/neovim/nvim-lspconfig?tab=readme-ov-file#important-%EF%B8%8F)
This step is necessary because nvim-lspconfig will soon be deprecated. Until then you'll get annoying deprecation notice at every start.

I've updated the nvim config with this change on a branch [native-nvim-lsp-config](https://github.com/beammeout/nvim-bsd-lazy/tree/native-nvim-lsp-config). However there are few downsides:
-  Terraformls has issues - it is not auto attached to newly open buffers
-  You need latest stable version of neovim

# Troubleshooting
## I'm getting clone failed error.

This often happens with treesitter:
```
Failed (1)                                                                                                                   
~                   ○ nvim-treesitter      ■ clone failed                                                                                      
~                       fatal: repository '/home/somehome/.local/share/nvim/lazy/nvim-treesitter' does not exist
```
In this case simply remove the whole clone lock file like this:
```
rm -rf /home/somehome/.local/share/nvim/lazy/nvim-treesitter.cloning
```
Now make sure you switch to local lazy package storage:
`cd /home/somehome/.local/share/nvim/lazy/`

And manually git clone the treesitter:
`git clone https://github.com/nvim-treesitter/nvim-treesitter.git`

Start lazy, you might get a warning, but it should work from now on.

## I can't install language servers via Mason
- See [Limitations](#limitations)

## Language servers are installed, but not recognized by neovim
- Make sure lsp executable and is in the PATH variable of your shell.
- Make sure lsp is correctly initialized in the lua config. There are examples for `lua_ls`, `pyright`, `terraformls` and `marksman` in the `lua/plugins/coding.lua` file.

## Your key bindings are a mess! I don't like them
- Cannot but agree ¯\_(ツ)_/¯ . The bindings are in `init.vim` and `lua/init.lua` files. You can change/remove them as you see fit.

## Something in this repo is wrong, doesn't work, can be done better, etc.
- Good job spotting that! You can open an issue or submit a PR, but no guarantee I will take action. Nothing personal, just want to spend some time touching grass 🍀😇.
