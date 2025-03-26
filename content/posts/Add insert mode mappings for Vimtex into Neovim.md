---
title: "Add Insert Mode Mappings for Vimtex Into Neovim"
date: 2025-03-25T23:26:37Z
draft: false
---

I use [vimtex](https://github.com/lervag/vimtex/) to aid my way of writing LaTeX in Neovim, but _vimtex_ is written in _vimscript_ and my Neovim configuration is in Lua.
As a result, when I am not careful I may spend more time than acceptable to configure something.

Here is how to use [vim.fn](https://neovim.io/doc/user/lua.html#vim.fn) to access functions from plugins written in _vimscript_ if you use [lazy.nvim](https://github.com/folke/lazy.nvim) as your plugin manager.

This is the recommended configuration from _vimtex_'s repo using _lazy_.
```lua
{
  "lervag/vimtex",
  lazy = false,     -- we don't want to lazy load VimTeX
  -- tag = "v2.15", -- uncomment to pin to a specific release
  init = function()
    -- VimTeX configuration goes here, e.g.
    vim.g.vimtex_view_method = "zathura"
  end
}
```
If you want to access the `vimtex#imaps#add_map` function to add a new insert mode map you can use several options, in particular [vim.cmd](https://neovim.io/doc/user/lua.html#vim.cmd()) and `vim.fn`.
I went with with the later because it allows for a more _Lua_-like syntax by transforming _Lua_ tables into _vimscript_ ones.

However, you may be tempted to add any piece of configuration for _vimtex_ inside of the plugin spec above.
I am here to tell you...

> DO NOT CALL `vim.fn` INSIDE THE PLUGIN SPEC!

I tried that, which means that I called `vim.fn` inside of the function definition provided as value to the `init` parameter.
If you do the same, since the plugin will not be loaded before it is loaded---silly, yes, but that's what is happening---Neovim will scream that your function is unknown, because it is at the moment.

What you want to do, since this is a [filetype](https://neovim.io/doc/user/filetype.html) thing, is to write this function call in the corresponding filetype configuration.
In my case---and most cases if you are configuring with _Lua_---this will be in the file `after/ftplugin/tex.lua`.
In there you add
```lua
--- ~/.config/nvim/after/ftplugin/tex.lua
...
vim.fn['vimtex#imaps#add_map']({lhs = '---', rhs = '\\textemdash', wrapper = 'vimtex#imaps#wrap_trivial'})
...
```
And it's done!

This insert mode mapping will be triggered by pressing `<localleader>---` and will insert a `\textemdash` command.
I know that writing `---` in LaTeX is exactly the same as using the `\textemdash` command, but I like to have the command, that's how I write and that's why I did it.
To learn why the code above is like that, see [:h vimtex-imaps](https://github.com/lervag/vimtex/blob/master/doc/vimtex.txt).

The moral of this entry is, as usual: **learn your tools**.
