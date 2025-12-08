# Personal notes


## Features I'd expect from an IDE

### Multi-line select and movement
Multi-line select and moving those lines up and down without breaking indentation.

In VSCode, this is achieved with Opt+Arrows.

### Multi-line select and duplication 
Select a line and duplicate it, without breaking indentation. Or select more than one and duplicate them.

In VSCode, this is achieved with Opt+Shift+Arrows.

## Learn

Nvim tutor: `:Tutor`.
Help: `:help`

## Load Files
Files in nvim are loaded into a buffer. If an external tool (e.g. an AI agent, or a 3rd party tool) modifies a file that is open, you might see an old version. 

Command `:e` (for _edit_) will reload the file.

## Navigate Files

Search files: `space + s (search) + f (file)`
  - some files are ignored and not shown by Telescope. Settings could be modified, but also the core vim command `:e path/to/file` can be used
Search files in current Neovim project: `space + s + n` 
Go back to navigator view: `:Explore`. This just goes to the directory where the current file is. Might need another plugin for a better experience.
Search help: `space + s + h`
Go to line: `:<line-number>` or `<line-number>gg`
End of line: `$`
Start of line: `^`


### Edit block
I have added mappings to perform line movement both from normal mode and visual mode.
Mapping uses "<A-k>" and "<A-j>" to move a line, where "A" stands for the Meta key. The terminal running nvim defines what the Meta key is (often the left Opt key in MacOs), and can be configured per terminal. 

### Navigate windows
Sometimes "popup" windows appear in nvim, like when running ":Lazy" to manage plugins.
The command "<C-w>" opens a menu to manage windows, with many options similar to tmux. Some useful keys are:
- "<C-w> h/j/k/l" moves cursor to window that was split, using h/j/k/l motions
- "<C-w> q" closes current window (where cursor is)

## Plugins, Extensions

### LSPs, linters, formatters

They are managed with Mason, a nvim plugin that can install language analyzers. You can interact with it via `:Mason`:
- `Enter` shows the description of an extension
- `i` installs an extension

Mason stores downloaded extensions outside of nvim config, in `~/.local/share/nvim/mason/`
