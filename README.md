# Beamer's nvim config
Nvim config tested on FreeBSD with lazy plugin manager

## Pre-requisits
install lua51 and luarocks51 and git

## On OpenBSD
Installing pkg_add luarocks-lua51 is enough, it will also install various lua versions. You will get reminder to create the necessary simlinks for luarocks.
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
pkg install lua51 git
```
You might need to simlink lua51 to lua:
```
ln -s /usr/local/bin/lua51 /usr/local/bin/lua
```


## Getting started
- Backup your original nvim configuration in ~/.confing/nvim/
- Clone this repo to your nvim config folder
- Upon nvim start Lazy screen should popup, and offer you sync and install for all the plugins.
- Restart nvim, check for any errors in the bottom.
- Tom make sure if everything works run `:checkhealth` after nvim start. Scroll through the list and check for ERRORS.

## Troubleshooint
### I'm getting clone failed error.

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

