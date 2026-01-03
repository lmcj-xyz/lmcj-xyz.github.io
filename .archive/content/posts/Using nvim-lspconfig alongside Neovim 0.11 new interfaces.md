---
title: "Using nvim-lspconfig Alongside Neovim 0.11 New Interfaces"
date: 2025-03-27T14:05:58Z
draft: true
---

[Neovim 0.11](https://gpanders.com/blog/whats-new-in-neovim-0-11/) has dropped, and with it, some new very nice features.

In particular `vim.lsp.config` and `vim.lsp.enable` to harness the built-in LSP functionality of Neovim.

Some people seem confused as to how can one use the curated configurations provided by [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) together with these new interfaces.
Here I will show you how I did it.
It is extremely easy, and it will take you just a few minutes.

> Disclaimer: Read the whole thing before copying and pasting anything, it will take you five minutes.

# Tutorial
If you have the `nvim-lspconfig` plugin enabled, you may know this is a data-only repository where users have contributed sensible configurations for a big number of LSP implementations for different languages.
This plugin essentially will create a table with the default configuration suggested in it and put it in your computer.
And normally if you wanted to extend this configuration---you may take a different approach---the recommendation is to modify the settings within the `config` option of the plugin and inside of the table from the `setup` function.
Let's take the following example for my own configuration of [ltex-ls](https://github.com/valentjn/ltex-ls) before Neovim 0.11:
```lua
```lua
{
    'neovim/nvim-lspconfig',
        config = function()
            local eng_dict = {}
            for word in io.open(vim.fn.stdpath("config") .. "/spell/en.utf-8.add", "r"):lines() do
            table.insert(eng_dict, word)
            end
            lspconfig.ltex.setup({
                filetypes = { "latex", "tex", "bib", },
                settings = {
                    ltex = {
                        enabled = {'bib', 'context', 'latex', 'plaintex', 'tex'},
                        language = 'en-GB',
                        dictionary = {
                            ["en-GB"] = eng_dict,
                        },
                    }
                }
            })
        end,
}
```
In there, you see the line containing `lspconfig.ltex.setup` which if you don't want any extra configuration is enough to call and provided the `ltex` LSP implementation is installed and reachable, it will do its thing.
However, you can see how I am adding options to the table inside that function call, and also I have outside the definition of a variable with essentially just takes the spelling list from Neovim and gives it to the LSP so that you create a custom dictionary.
Well, the same configuration in Neovim 0.11 looks like this:
```lua
{
    'neovim/nvim-lspconfig',
        config = function()
            lspconfig.ltex.setup({})
        end,
}
```
Which loads the configuration by default...but then where is my extension configuration?
You can do one of two things, to do everything in your `init.lua`, or to modularize it.

## Modular approach
I decided to modularize it and put it into the file `~/.config/nvim/lsp/ltex.lua` which looks like this:
```lua
--- ~/.config/nvim/lsp/ltex.lua
local eng_dict = {}
for word in io.open(vim.fn.stdpath("config") .. "/spell/en.utf-8.add", "r"):lines() do
    table.insert(eng_dict, word)
end
return {
    filetypes = { "latex", "tex", "bib", },
    settings = {
        ltex = {
            enabled = {'bib', 'context', 'latex', 'plaintex', 'tex'},
            language = 'en-GB',
            dictionary = {
                ["en-GB"] = eng_dict,
            },
        }
    }
}
```
And then I can call in my `init.lua` the interface
```lua
--- ~/.config/nvim/init.lua
vim.lsp.enable({ 'ltex' })
```
> Be cautious, you have to call `ltex` in this case because the file in the `~/.config/nvim/lsp` directory is called like that. It doesn't have to be called as the LSP implementation, just needs to agree with the file you are looking for.
> Also, don't add anything that is not currently a file in the `lsp` directory, it won't load the configuration. And the configuration of the `nvim-lspconfig` plugin will enable a plugin that doesn't have any extra configuration for you.

This can be modularized further, but for the sake of the tutorial I think this is best.

## Single file approach
The other option is to call the other new interface `vim.lsp.config` in your `init.lua`
If you do that, our example will look like this
```lua
local eng_dict = {}
for word in io.open(vim.fn.stdpath("config") .. "/spell/en.utf-8.add", "r"):lines() do
    table.insert(eng_dict, word)
end
vim.lsp.config.ltex = {
    filetypes = { "latex", "tex", "bib", },
    settings = {
        ltex = {
            enabled = {'bib', 'context', 'latex', 'plaintex', 'tex'},
            language = 'en-GB',
            dictionary = {
                ["en-GB"] = eng_dict,
            },
        }
    }
}
vim.lsp.enable({'ltex'})
```
Notice that here, you are modifying the table `vim.lsp.config.ltex` and then enabling it.

And you are set.

# Foreword
Remember that Lua is a programming language, so you can do programming language like things.

See the [entry by Gregory Anders](https://gpanders.com/blog/whats-new-in-neovim-0-11/) for any more details in the new features.
In there this is an extra warning on the required options you must declare for this to work, but since `nvim-lspconfig` will enable those options, you don't have to worry about them unless you want to modify them.
