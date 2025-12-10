---
layout: post
title: "How To Configure Neovim for Writing in Markdown"
date: 2025-10-04 01:00:00 -0600
---

![tmux terminal with Neovim](/assets/images/markdown-neovim.png)

Out of the box Neovim doesn't have great markdown support. Of course you can just start typing a markdown file, but navigation with the keyboard is very difficult and there also is no wrapping of text so lines are really long. In this post I'll walk you through some of the changes I have made to make it easier to work with markdown in Neovim.

I'm getting back into using vim more and I do really enjoy using it for writing. I like the aesthetics of writing in a terminal because if gives me typewriter vibes, but actually more like I'm writing on an old PC that doesn't even have a GUI. Something about the focus of only your words on the screen and keyboard are magical.

### Wrapping and Navigation

I used to hard wrap lines in vim at 80 characters so that I didn't have long lines and so that I could easily navigate in vim using `j`/`k`. I found that I don't like messing with the line breaks like that though especially if I have to paste the markdown into some other app. 

What you can do instead is to use soft wrapping based on the terminal window size (or tmux pane). Then to fix navigation you can update these key mappings so that using `j`/`k` navigates per line and not the entire paragraph. `0` will take you to the beginning of the line and `$` will you to the end of the line. 

Here is the configuration I added to the ftplugin `markdown.lua` file:

```
-- ~/.config/nvim/after/ftplugin/markdown.lua
vim.opt_local.wrap = true
vim.opt_local.linebreak = true
vim.opt_local.breakindent = true
vim.keymap.set("n", "j", "gj", { buffer = true })
vim.keymap.set("n", "k", "gk", { buffer = true })
vim.keymap.set("n", "0", "g0", { buffer = true })
vim.keymap.set("n", "$", "g$", { buffer = true })
```

### Spell Check

For spell check I'm just using the built in support and I've enabled it by adding these lines to the same `markdown.lua` file. This just enables spell check for markdown files and which spell "lang" file to use.

```
-- ~/.config/nvim/after/ftplugin/markdown.lua
-- ...
--
-- spell check
vim.opt_local.spell = true
vim.opt_local.spelllang = { "en_us" }
```

To fix spelling you can use these commands:

* `]s` → jump to next misspelled word
* `[s` → jump to previous
* `z=` → suggestions for the word under cursor
* `zg` → mark word as good
* `zw` → mark word as bad

I'm sure there other things that I'll add in the future, but with just these changes I've found writing in Neovim much more enjoyable and productive.
