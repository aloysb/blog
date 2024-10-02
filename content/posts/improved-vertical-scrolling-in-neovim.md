---
title: 'Improved Vertical Scrolling in Neovim'
date: 2024-10-05T09:07:37+10:00
draft: false
tags: 
    - neovim
category: neovim
---

# Improved Vertical Scrolling in Neovim

Neovim is great.

What I really like about Neovim and similar tools is the fact that you can customize it to fit your workflow, rather than the other way around.

When reading code in Neovim, I often use `Ctrl-U/D` to scroll vertically through a file.

One minor issue is that you quickly end up with the active line at the top or bottom edge of your window.

You can use `zz` to center the active line, making it more comfortable, or you can configure Neovim to automatically do it for you.

```lua
-- better vertical nav - center the active line after scrolling half a page
vim.keymap.set('n', '<C-d>', '<C-d>zz', { desc = 'Scroll downwards' })
vim.keymap.set('n', '<C-u>', '<C-u>zz', { desc = 'Scroll upwards' })
```

Add this snippet to your config, and every time you hit `Ctrl-U/D`, you will also send `zz`.

This will keep the active line centered as you scroll through the file.

Enjoy,
Aloys.

