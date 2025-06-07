# Beamer's nvim config
Nvim config tested on FreeBSD with lazy plugin manager

## Pre-requisits
install lua51 and luarocks51 and git
```
pkg install lua51-lua lua51 git
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
