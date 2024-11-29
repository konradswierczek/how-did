# Build nvim
sudo apt update
sudo apt install npm

```bash
sudo apt update
sudo apt install xclip
```

```lua
-- ~/.config/nvim/init.lua
vim.opt.clipboard:append("unnamedplus")
vim.g.clipboard = {
    name = "xclip",
    copy = {
        ["+"] = "xclip -selection clipboard",
        ["*"] = "xclip -selection clipboard",
    },
    paste = {
        ["+"] = "xclip -selection clipboard -o",
        ["*"] = "xclip -selection clipboard -o",
    },
    cache_enabled = 0,
}

```
