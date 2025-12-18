# Personal notes


## Features I'd expect from an IDE

### Multi-line select and movement
Multi-line select and moving those lines up and down without breaking indentation.

In VSCode, this is achieved with Opt+Arrows.
In my config, I have a remapping of Opt+j and Opt+k to move up and down, both in normal and visual mode.

### Multi-line select and duplication 
Select a line and duplicate it, without breaking indentation. Or select more than one and duplicate them.

In VSCode, this is achieved with Opt+Shift+Arrows.
In my config, I have a remapping of Opt+Shift+j and Opt+Shift+k to move up and down, both in normal and visual mode.

### Integrated terminal

The native terminal can be opened with `:terminal`. I have installed a plugin called `toggleterm`, and mapped it to `leader + t`, to switch to/from terminal easier.

## Learn

Nvim tutor: `:Tutor`.
Help: `:help`

## Load Files
Files in nvim are loaded into a buffer. If an external tool (e.g. an AI agent, or a 3rd party tool) modifies a file that is open, you might see an old version. 

Command `:e` (for _edit_) will reload the file.

## Save Files
The classic vi `:w` will save the current file. However, if for instance an LSP has modified many files, those changes will all be in buffers.
Run `:wa` (write all) to flush all buffers. Otherwise looking for content with Telescope, or git/jj, will not show new contents.

## Navigate Files

Move cursor:
 - `hjkl` to move in 4 directions
- `w`/`e` to move forward a word (beginning or end), and `b/ge` to move backward a word

Search files: `leader + s (search) + f (file)`
  - some files are ignored and not shown by Telescope. Settings could be modified, but also the core vim command `:e path/to/file` can be used
Search INSIDE files: `leader + s (search) + g (grep)`

Search files in current Neovim project: `leader + s + n` 
Go back to navigator view: `:Explore`. This just goes to the directory where the current file is. Might need another plugin for a better experience.
Search help: `leader + s + h`
Go to line: `:<line-number>` or `<line-number>gg`
End of line: `$`
Start of line: `^`

## Navigate code in files
The command `g`, when over a symbol, will open some options related to the LSP. Especially useful are:
- `grr`: [g]o to [r]eferences
- `gd`: [g]o to [d]efinition
- `grn`: [r]e[n]ame

### Edit block
I have added mappings to perform line movement both from normal mode and visual mode.
Mapping uses "<A-k>" and "<A-j>" to move a line, where "A" stands for the Meta key. The terminal running nvim defines what the Meta key is (often the left Opt key in MacOs), and can be configured per terminal.

A way to replace many occurrences of a string in a file is with `:%s/find/replace`.

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
