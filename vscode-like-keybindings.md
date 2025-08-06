# VS Code-like Keybindings for Neovim

Transform your Neovim into a VS Code-like experience with these essential keybindings.

## File Operations
| Keybinding | Action | VS Code Equivalent |
|------------|--------|-------------------|
| `<leader>ff` | Find files | `Ctrl+P` |
| `<leader>fg` | Find in files | `Ctrl+Shift+F` |
| `<leader>fb` | Find buffers | `Ctrl+Tab` |
| `<leader>fr` | Recent files | `Ctrl+R` |
| `<leader>fs` | Save file | `Ctrl+S` |

## Editor Operations
| Keybinding | Action | VS Code Equivalent |
|------------|--------|-------------------|
| `<leader>/` | Toggle comment | `Ctrl+/` |
| `<leader>d` | Duplicate line | `Shift+Alt+↓` |
| `<leader>x` | Close buffer | `Ctrl+W` |
| `<leader>z` | Toggle zen mode | `Ctrl+K Z` |
| `<leader>w` | Quick save | `Ctrl+S` |

## Navigation & LSP
| Keybinding | Action | VS Code Equivalent |
|------------|--------|-------------------|
| `gd` | Go to definition | `F12` |
| `gr` | Find references | `Shift+F12` |
| `K` | Hover info | `Ctrl+K Ctrl+I` |
| `<leader>rn` | Rename symbol | `F2` |
| `<leader>ca` | Code actions | `Ctrl+.` |

## Terminal & Debugging
| Keybinding | Action | VS Code Equivalent |
|------------|--------|-------------------|
| `<leader>tt` | Toggle terminal | `Ctrl+\`` |
| `<leader>tf` | Float terminal | - |
| `<leader>db` | Toggle breakpoint | `F9` |
| `<leader>dc` | Continue debug | `F5` |
| `<leader>ds` | Step over | `F10` |

## Git Integration
| Keybinding | Action | VS Code Equivalent |
|------------|--------|-------------------|
| `<leader>gg` | Lazygit | `Ctrl+Shift+G` |
| `<leader>gb` | Git blame | - |
| `<leader>gd` | Git diff | - |
| `<leader>gs` | Git status | - |
| `<leader>gc` | Git commits | - |

## Setup Instructions

Add these to your `lua/custom/mappings.lua` or equivalent:

```lua
local M = {}

M.general = {
  n = {
    -- File operations
    ["<leader>ff"] = { "<cmd>Telescope find_files<CR>", "Find files" },
    ["<leader>fg"] = { "<cmd>Telescope live_grep<CR>", "Find in files" },
    ["<leader>fb"] = { "<cmd>Telescope buffers<CR>", "Find buffers" },
    ["<leader>fr"] = { "<cmd>Telescope oldfiles<CR>", "Recent files" },
    ["<leader>fs"] = { "<cmd>w<CR>", "Save file" },
    
    -- Editor operations
    ["<leader>/"] = { "gcc", "Toggle comment", opts = { remap = true } },
    ["<leader>d"] = { "yyp", "Duplicate line" },
    ["<leader>x"] = { "<cmd>bd<CR>", "Close buffer" },
    ["<leader>w"] = { "<cmd>w<CR>", "Quick save" },
    
    -- Navigation & LSP
    ["<leader>rn"] = { "<cmd>lua vim.lsp.buf.rename()<CR>", "Rename symbol" },
    ["<leader>ca"] = { "<cmd>lua vim.lsp.buf.code_action()<CR>", "Code actions" },
    
    -- Terminal
    ["<leader>tt"] = { "<cmd>ToggleTerm<CR>", "Toggle terminal" },
    ["<leader>tf"] = { "<cmd>ToggleTerm direction=float<CR>", "Float terminal" },
    
    -- Git
    ["<leader>gg"] = { "<cmd>LazyGit<CR>", "LazyGit" },
    ["<leader>gb"] = { "<cmd>Gitsigns blame_line<CR>", "Git blame" },
    ["<leader>gd"] = { "<cmd>Gitsigns diffthis<CR>", "Git diff" },
  },
  
  v = {
    ["<leader>/"] = { "gc", "Toggle comment", opts = { remap = true } },
  }
}

return M
```

## Required Plugins

Make sure you have these plugins installed:

- `telescope.nvim` - For file finding
- `toggleterm.nvim` - For terminal integration
- `lazygit.nvim` - For git integration
- `gitsigns.nvim` - For git signs and blame
- `comment.nvim` - For commenting
- Your preferred LSP setup

## YouTube Learning Resources

- 🎥 [TJ DeVries - Neovim Plugin Development](https://youtube.com/watch?v=n4Lp4cV8YR0)
- 🎥 [ThePrimeagen - Neovim Lua Configuration](https://youtube.com/watch?v=w7i4amO_zaE)
- 🎥 [chris@machine - Complete Neovim Setup](https://youtube.com/playlist?list=PLhoH5vyxr6Qq41NFL4GvhFp-WLd5xzIzZ)
- 🎥 [Josean Martinez - Neovim Setup From Scratch](https://youtube.com/watch?v=vdn_pKJUda8)
- 🎥 [Elijah Manor - Neovim Plugin Development](https://youtube.com/watch?v=HXxjNWE9eT4)