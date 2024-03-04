# alpha-nvim-bofh-excuse

## synopsis

fork of https://github.com/BlakeJC94/alpha-nvim-fortune. instead of inspirational quotes, these are just BOFH excuses on the nvim alpha-dashboard (Only the `dashboard` theme is supported for now.)

### credits

Many thanks to `@mhinz` (original author for vim-startify), `@BlakeJC94` (original other of the fork for alpha) and `@chuckwagoncomputing` (who provided the list of excuses)

## Quick start
 It simple adds a
`excuse()` function for use in the plugin that generates a formatted BOFH excuse at
the footer of the landing page when using the `dashboard` theme.
First follow the instructions at `https://github.com/goolord/alpha-nvim/`. To
add `alpha-nvim-bofh-excuse` with `Packer`, install the packages with the folloing
lines in your `init.lua`:

```lua
return require('packer').startup(function()
    use 'wbthomason/packer.nvim'
    use {
        'goolord/alpha-nvim',
        requires = {'burgr033/alpha-nvim-bofh-excuse'},
        config = function() require("config.alpha") end,
    }
end)
```

Then in `.config/nvim/lua/config/alpha.lua`, use the following lines:
```lua

local alpha = require("alpha")
local dashboard = require("alpha.themes.dashboard")
local excuse = require("alpha.excuse")

-- Set header
dashboard.section.header.val = {
    -- "                                                     ",
    -- "                                                     ",
    "                                                     ",
    "  ███╗   ██╗███████╗ ██████╗ ██╗   ██╗██╗███╗   ███╗ ",
    "  ████╗  ██║██╔════╝██╔═══██╗██║   ██║██║████╗ ████║ ",
    "  ██╔██╗ ██║█████╗  ██║   ██║██║   ██║██║██╔████╔██║ ",
    "  ██║╚██╗██║██╔══╝  ██║   ██║╚██╗ ██╔╝██║██║╚██╔╝██║ ",
    "  ██║ ╚████║███████╗╚██████╔╝ ╚████╔╝ ██║██║ ╚═╝ ██║ ",
    "  ╚═╝  ╚═══╝╚══════╝ ╚═════╝   ╚═══╝  ╚═╝╚═╝     ╚═╝ ",
    "                                                     ",
    -- "                                                     ",
    -- "                                                     ",
    -- "                                                     ",
}

-- Set menu
dashboard.section.buttons.val = {
    dashboard.button( "e", "  > New file" , ":ene <BAR> startinsert <CR>"),
    dashboard.button( "f", "  > Find file", ":cd $HOME/Workspace | Telescope find_files<CR>"),
    dashboard.button( "r", "  > Recent"   , ":Telescope oldfiles<CR>"),
    dashboard.button( "s", "  > Settings" , ":e $MYVIMRC | :cd %:p:h | split . | wincmd k | pwd<CR>"),
    dashboard.button( "q", "  > Quit NVIM", ":qa<CR>"),
}

-- Set footer
dashboard.section.footer.val = excuse()

-- Send config to alpha
alpha.setup(dashboard.opts)
```

