# Neovim & NvChad Mastery Plan

A progressive learning path from basic Lua syntax to advanced Neovim configuration and NvChad customization.

## Prerequisites
- Basic programming knowledge (you have this ✓)
- Neovim installed
- NvChad setup completed

## Phase 1: Lua Fundamentals (Days 1-7)

### Exercise 1.1: Basic Lua Syntax
Create a file `lua-basics.lua` and practice:
```lua
-- Variables and types
local name = "NeoVim"
local version = 0.9
local is_awesome = true

-- Tables (Lua's primary data structure)
local config = {
  theme = "catppuccin",
  line_numbers = true,
  plugins = {"telescope", "treesitter"}
}

-- Functions
local function greet(user)
  return "Hello " .. user
end

print(greet("Neovim User"))
```

**Task**: Write 5 different Lua functions that manipulate tables and strings.

### Exercise 1.2: Lua Table Manipulation
```lua
-- Practice table operations
local plugins = {}
table.insert(plugins, "lspconfig")
table.insert(plugins, "null-ls")

-- Iterate through tables
for i, plugin in ipairs(plugins) do
  print(i, plugin)
end

-- Key-value pairs
for key, value in pairs(config) do
  print(key, value)
end
```

**Task**: Create a plugin manager simulator using tables and functions.

### Exercise 1.3: Modules and Require
Create `utils.lua`:
```lua
local M = {}

function M.capitalize(str)
  return str:sub(1,1):upper() .. str:sub(2)
end

function M.merge_tables(t1, t2)
  for k, v in pairs(t2) do
    t1[k] = v
  end
  return t1
end

return M
```

**Task**: Create 3 utility modules with different helper functions.

## Phase 2: Neovim Lua API Basics (Days 8-14)

### Exercise 2.1: Vim API Exploration
```lua
-- Get current buffer info
local bufnr = vim.api.nvim_get_current_buf()
local filename = vim.api.nvim_buf_get_name(bufnr)
print("Current file: " .. filename)

-- Set options
vim.api.nvim_set_option('number', true)
vim.api.nvim_set_option('relativenumber', true)
```

**Task**: Create a script that displays current buffer statistics.

### Exercise 2.2: Key Mappings
```lua
-- Basic key mapping
vim.api.nvim_set_keymap('n', '<leader>w', ':w<CR>', {noremap = true, silent = true})

-- Using vim.keymap.set (newer API)
vim.keymap.set('n', '<leader>q', ':q<CR>', {desc = "Quit current buffer"})
```

**Task**: Create 10 custom keymaps for different modes (normal, insert, visual).

### Exercise 2.3: Autocommands
```lua
-- Create autocommand group
local group = vim.api.nvim_create_augroup("MyCustomGroup", {clear = true})

-- Auto-save on focus lost
vim.api.nvim_create_autocmd("FocusLost", {
  group = group,
  pattern = "*",
  command = "wa"
})
```

**Task**: Create autocommands for file-type specific settings.

## Phase 3: NvChad Configuration (Days 15-21)

### Exercise 3.1: Understanding NvChad Structure
Explore these directories:
```
~/.config/nvim/
├── init.lua
├── lua/
│   ├── core/
│   ├── plugins/
│   └── custom/
```

**Task**: Map out NvChad's file structure and understand each component's purpose.

### Exercise 3.2: Custom Configuration
Edit `lua/custom/chadrc.lua`:
```lua
local M = {}

M.ui = {
  theme = "catppuccin",
  transparency = false,
  statusline = {
    theme = "default",
  },
}

M.plugins = "custom.plugins"
M.mappings = require "custom.mappings"

return M
```

**Task**: Customize 5 different UI elements in your chadrc.lua.

### Exercise 3.3: Custom Plugins
Create `lua/custom/plugins.lua`:
```lua
local plugins = {
  {
    "folke/which-key.nvim",
    keys = { "<leader>", "<c-r>", '"', "'", "`", "c", "v", "g" },
    config = function()
      require("which-key").setup()
    end,
  },
}

return plugins
```

**Task**: Add 3 new plugins with proper configuration.

## Phase 4: Advanced Customization (Days 22-35)

### Exercise 4.1: Custom Statusline
```lua
-- In lua/custom/plugins.lua
{
  "nvim-lualine/lualine.nvim",
  config = function()
    require("lualine").setup {
      options = {
        theme = "auto",
        component_separators = { left = "", right = ""},
        section_separators = { left = "", right = ""},
      },
      sections = {
        lualine_a = {"mode"},
        lualine_b = {"branch", "diff", "diagnostics"},
        lualine_c = {"filename"},
        lualine_x = {"encoding", "fileformat", "filetype"},
        lualine_y = {"progress"},
        lualine_z = {"location"}
      },
    }
  end,
}
```

**Task**: Create a completely custom statusline with git info, LSP status, and custom components.

### Exercise 4.2: LSP Configuration
Create `lua/custom/configs/lspconfig.lua`:
```lua
local config = require("plugins.configs.lspconfig")
local on_attach = config.on_attach
local capabilities = config.capabilities

local lspconfig = require("lspconfig")

-- Python
lspconfig.pyright.setup {
  on_attach = on_attach,
  capabilities = capabilities,
  filetypes = {"python"},
}

-- JavaScript/TypeScript
lspconfig.tsserver.setup {
  on_attach = on_attach,
  capabilities = capabilities,
}
```

**Task**: Configure LSP for 5 different programming languages you use.

### Exercise 4.3: Custom Telescope Extensions
```lua
local telescope = require("telescope")

telescope.setup {
  extensions = {
    fzf = {
      fuzzy = true,
      override_generic_sorter = true,
      override_file_sorter = true,
    },
  },
}

telescope.load_extension("fzf")
```

**Task**: Create custom Telescope pickers for project-specific searches.

## Phase 5: Plugin Development (Days 36-49)

### Exercise 5.1: Simple Plugin Structure
Create `lua/custom/my-plugin/init.lua`:
```lua
local M = {}

M.setup = function(opts)
  opts = opts or {}
  -- Plugin initialization
end

M.toggle_feature = function()
  -- Custom functionality
  print("Feature toggled!")
end

return M
```

**Task**: Create a simple plugin that manages your custom snippets.

### Exercise 5.2: Advanced Plugin Features
```lua
local M = {}

local config = {
  auto_save = true,
  highlight_group = "Search",
}

M.setup = function(user_config)
  config = vim.tbl_deep_extend("force", config, user_config or {})
  
  -- Create highlight group
  vim.api.nvim_set_hl(0, config.highlight_group, {fg = "#ff0000"})
  
  -- Set up autocommands
  local group = vim.api.nvim_create_augroup("MyPlugin", {clear = true})
  vim.api.nvim_create_autocmd("BufWritePre", {
    group = group,
    callback = M.process_buffer,
  })
end

M.process_buffer = function()
  if config.auto_save then
    vim.cmd("write")
  end
end

return M
```

**Task**: Build a productivity plugin with configuration options and autocommands.

## Phase 6: Master Level Customization (Days 50-70)

### Exercise 6.1: Custom Completion Source
```lua
-- Create custom nvim-cmp source
local source = {}

source.new = function()
  return setmetatable({}, { __index = source })
end

source.get_trigger_characters = function()
  return { "@" }
end

source.complete = function(self, params, callback)
  local items = {
    { label = "@username", kind = 1 },
    { label = "@email", kind = 1 },
  }
  callback({ items = items })
end

require("cmp").register_source("custom", source.new())
```

**Task**: Create a context-aware completion source for your workflow.

### Exercise 6.2: Advanced Key Mapping System
```lua
local M = {}

local mappings = {
  leader = {
    f = {
      name = "File operations",
      f = { "<cmd>Telescope find_files<cr>", "Find files" },
      r = { "<cmd>Telescope oldfiles<cr>", "Recent files" },
      s = { "<cmd>w<cr>", "Save file" },
    },
    g = {
      name = "Git operations",
      s = { "<cmd>Git status<cr>", "Status" },
      c = { "<cmd>Git commit<cr>", "Commit" },
    }
  }
}

M.setup = function()
  local wk = require("which-key")
  wk.register(mappings.leader, { prefix = "<leader>" })
end

return M
```

**Task**: Build a comprehensive key mapping system with contextual menus.

### Exercise 6.3: Custom Dashboard
```lua
local M = {}

M.create_dashboard = function()
  local buf = vim.api.nvim_create_buf(false, true)
  vim.api.nvim_set_current_buf(buf)
  
  local lines = {
    "  ███╗   ██╗███████╗ ██████╗ ██╗   ██╗██╗███╗   ███╗",
    "  ████╗  ██║██╔════╝██╔═══██╗██║   ██║██║████╗ ████║",
    "  ██╔██╗ ██║█████╗  ██║   ██║██║   ██║██║██╔████╔██║",
    "  ██║╚██╗██║██╔══╝  ██║   ██║╚██╗ ██╔╝██║██║╚██╔╝██║",
    "  ██║ ╚████║███████╗╚██████╔╝ ╚████╔╝ ██║██║ ╚═╝ ██║",
    "  ╚═╝  ╚═══╝╚══════╝ ╚═════╝   ╚═══╝  ╚═╝╚═╝     ╚═╝",
    "",
    "  Recent Files:",
  }
  
  vim.api.nvim_buf_set_lines(buf, 0, -1, false, lines)
  -- Add recent files, key mappings, etc.
end

return M
```

**Task**: Build a fully functional dashboard with project shortcuts and statistics.

## Daily Practice Routine

### Week 1-2: Foundation Building
- 30 minutes Lua syntax practice
- 30 minutes exploring Neovim API documentation
- Create one small utility function daily

### Week 3-4: NvChad Integration
- Modify one NvChad configuration daily
- Add one new plugin per week
- Document all changes

### Week 5-7: Advanced Features
- Build one custom command/function daily
- Contribute to NvChad community discussions
- Share configurations with others

### Week 8-10: Mastery Projects
- Build a complete plugin
- Create a custom theme
- Optimize performance and workflow

## Assessment Milestones

### Beginner (Day 14):
- [ ] Comfortable with Lua syntax
- [ ] Can modify basic Neovim settings
- [ ] Understands NvChad structure

### Intermediate (Day 35):
- [ ] Created custom plugins
- [ ] Configured LSP for multiple languages
- [ ] Built custom key mapping system

### Advanced (Day 49):
- [ ] Developed original plugins
- [ ] Contributed to community
- [ ] Optimized workflow significantly

### Master (Day 70):
- [ ] Expert-level configuration
- [ ] Teaching others effectively
- [ ] Contributing to Neovim ecosystem

## Resources and References

- [Neovim Lua API Documentation](https://neovim.io/doc/user/lua.html)
- [NvChad Documentation](https://nvchad.com/)
- [Lua Programming Guide](https://www.lua.org/manual/5.4/)
- [Learn Lua in Y Minutes](https://learnxinyminutes.com/docs/lua/)

## Progress Tracking

Create a simple progress tracker:
```lua
-- In lua/custom/progress.lua
local M = {}

M.log_progress = function(exercise, status)
  local file = io.open(vim.fn.stdpath("config") .. "/progress.log", "a")
  file:write(os.date("%Y-%m-%d") .. " - " .. exercise .. " - " .. status .. "\n")
  file:close()
end

return M
```

Remember: Practice daily, document your progress, and don't be afraid to break things while learning!