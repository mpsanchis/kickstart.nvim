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

## Basics
Modes:
- [v]isual
- [V]isual line
- [i]nsert
- normal (Esc /  <C-c>)

Commands:
- [d]elete
- [y]ank (copy)
- [c]hange (delete and go to insert mode)
- [v]isually select

Basic function is `Command + Count + Motion`.

## Load Files
Files in nvim are loaded into a buffer. If an external tool (e.g. an AI agent, or a 3rd party tool) modifies a file that is open, you might see an old version. 

Command `:e` (for [e]dit) will reload the file.

## Create Files
The command `:enew` will generate a new buffer, that can be saved later.
The command `:new` will generate a new buffer, but splitting the screen.

## Save Files
The classic vi `:w` will save the current file. However, if for instance an LSP has modified many files, those changes will all be in buffers.
Run `:wa` (write all) to flush all buffers. Otherwise looking for content with Telescope, or git/jj, will not show new contents.

## Navigate Within Files

Move cursor:
 - `hjkl` to move in 4 directions
- `w`/`e` to move forward a word (beginning or end), and `b/ge` to move backward a word

Move to matching bracket/parenthesis: `%`

### Search files (find/fd) and content (grep/rg)
Search files: `leader + s (search) + f (file)`
  - some files are ignored and not shown by Telescope. Settings could be modified, but also the core vim command `:e path/to/file` can be used
Search INSIDE files: `leader + s (search) + g (grep)`

Search files in current Neovim project: `leader + s + n` 
Go back to navigator view: `:Explore` (or `:Ex`). This just goes to the directory where the current file is. Might need another plugin for a better experience.
Search help: `leader + s + h`

### Line movements
- Go to line: `:<line-number>` or `<line-number>gg`
- End of line: `$`
- Start of line: `^` or `_`
- Jump ([f]orward) to the next character in line: `f<character>`.
- Jump (backward) to the previus character in line: `F<character>`.
- Jump ([t]ill) the next character, but stay one position before: `t<character>`.
- Jump ([T]ill) the next character, but stay one position before: `T<character>`.
- [I]nsert mode at the beginning of the line, or [A]t the end of the line.

Note that many of these can be used as a motion in `command + count + motion` (e.g.: `d<fx>` will delete until the next `x`).

## Navigate code in files
The command `g`, when over a symbol, will open some options related to the LSP. Especially useful are:
- `grr`: [g]o to [r]eferences
- `gd`: [g]o to [d]efinition
- `grn`: [r]e[n]ame

The symbols `[` (pre) and `]` (post) allow to move among methods and braces from Normal mode. Pressing them will show a help. Some useful combinations are:
- `[m` for "previous method start"
- `]m` for "next method start"

### Comment line
The command `g` also allows to comment lines, both in visual and normal mode:
- `gcc` to comment current line
- `gc{motion}` to comment lines covered by {motion} (such as `gc1j` to comment current and line below)
- `gc`, in visual mode, to comment lines highlighted in visual mode.

### Edit block
I have added mappings to perform line movement both from normal mode and visual mode.
Mapping uses "<A-k>" and "<A-j>" to move a line, where "A" stands for the Meta key. The terminal running nvim defines what the Meta key is (often the left Opt key in MacOs), and can be configured per terminal.

A way to replace many occurrences of a string in a file is with `:%s/find/replace`.

To replace in many files, one workflow that works is:
1. Find matches with telescope (<leader><s><g>)
2. Send matches to quickfix list (<C><q>)
3. Apply find and replace with "change file do" `:cfdo %s/find/replace | update | bd`.

Note the 3rd command does:
3.1 Find and replace in every file
3.2 Save all files (like `:wa`, but with all files that were modified)
3.3 Delete all buffers (`bd`) to keep memory usage low

### Redo/Undo
- `u` undoes the last action
- `<C-r>` redoes the last action

## Navigate windows
Sometimes "popup" windows appear in nvim, like when running ":Lazy" to manage plugins.
The command "<C-w>" opens a menu to manage windows, with many options similar to tmux. Some useful keys are:
- "<C-w> h/j/k/l" moves cursor to window that was split, using h/j/k/l motions
- "<C-w> q" closes current window (where cursor is)

## Navigate files
If jumping between files, the following is useful to go:
- back: `<C-o>` (ctrl+o, `o` as out of a location)
- forth: `<C-i>` (ctrl+i, `i` as into a location, such as a schema)

When in file explorer view, the following can be used:
- `%` to create a file and open it
- `D` to open prompt to delete a file
- `Enter` to open a file or directory
- `-` to go up one level in the dir tree

## Execute Code
The main way of executing code is by opening a terminal and running commands there. However, there are shortcuts for small commands:
- `:%!<command>` will:
  - select the whole buffer (`%`)
  - pass it to an external command and replace content with stdout (`!`)

An example of this is to `:%!jq .`, which will format a JSON, like `cat file.json | jq . > file.json` would do.
This can be triggered from visual mode, and nvim will autocomplete the selection with `'<'>`, which means "currently selected".

Commands can also be executed and their output only shown if we run:
- `:!<command>`, like `:!ls`, will keep the output in a visible buffer at the bottom

## Plugins, Extensions

### LSPs, linters, formatters

They are managed with Mason, a nvim plugin that can install language analyzers. You can interact with it via `:Mason`:
- `Enter` shows the description of an extension
- `i` installs an extension

Mason stores downloaded extensions outside of nvim config, in `~/.local/share/nvim/mason/`

### Code information

The equivalent of "hovering over" with the mouse in VSCode is done with `K` in normal mode, to get information about a type, for instance.

### File navigation

TBD: how to navigate files faster? There could be plugins for this. 
- 'mini.nvim' is already installed, so [mini.files](https://github.com/nvim-mini/mini.files) might be interesting.
- 'oil.nvim' is what many people use: https://github.com/stevearc/oil.nvim
- 'yazi.nvim' is used by people who use yazi as a file manager: https://github.com/mikavilpas/yazi.nvim
Note: would be nice to have something that displayed repo overview in filesystem, and also moved cursor to "current file" if exists (coming from a file)

# Doubts 
- How to visualize the project directories? -> tree or oil 
- How to "scroll" around? -> https://github.com/folke/snacks.nvim/blob/main/docs/scroll.md
- How to find comfortably in file? --> https://github.com/folke/flash.nvim
- How to move around when in "insert" mode, without going back to normal mode? -> patience
- How to collapse a JSON section? --> https://fx.wtf/
- How to format a file quickly? --> fx.wtf as well for json, otherwise conform.nvim  
- How to find and replace globally? (I do `:%s/foo/bar` for current file) --> look for plugins?
- How to find, filtering by file type? (apart from `fd` + `rg`?) --> see in telescope config?
- How to jump words in terminal? b/w works, but insert mode jumps back to end of line. --> see alternatives like tmux (or: https://github.com/nvim-pack/nvim-spectre)
