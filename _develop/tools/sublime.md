---
title: Sublime Text 3
layout: develop
---

Since I use sublime text as editor more and more, here some tips and tricks
I found helpful at work.


Specific Key Bindings
-------------------------------------------------

[
  { "keys": ["alt+g"], "command": "git_status" },
  { "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"github"} }
]


Goto
-------------------------------------------------

Use the shortcut `Ctrl/⌘ + P` to:

- open any file
- use `@...` jump to a symbol in the file
- use `#...` to search within file
- use `:...` to jump to line

You may also combine a starting file selection with one of the in file searches
like `index:30` or `index@mkdir`.

Shortcuts are also:

- `Ctrl/⌘ + R` to directly open the symbol search
- `Ctrl/⌘ + G` for the goto line jump

Or you may directly jump in the file:

- `Ctrl/⌘ + M` to the closing bracket

### Bookmarks

With `Ctrl + F2` you may make a bookmark for the current line and step through them
using `F2`. At the end delete all of them using `Ctrl + Shift + F2`.


Editing
-------------------------------------------------

### Multiple cursors

1. Use `Ctrl/⌘ + D` to duplicate the cursor to the next occurrence of the same word
  this may be done multiple times. Go back with `Ctrl/⌘ + U`.
2. You may also manually set multiple cursors with `Ctrl/⌘ + Mouseclick`.
3. `Alt + F3` (`Ctrl + ⌘ + G` on Mac) can be used to directly select all occurrences
  of the current selected word.
4. A block may be selected and using `Ctrl/⌘ + Shift + L` sets a cursor on each
line of the selection.

If you now edit something it will change on all cursor positions.

### Selections

The following shortcuts are available here:

- `Ctrl/⌘ + L` to select the whole current line
- `Ctrl/⌘ + D` to select the word
- `Ctrl/⌘ + Shift + J` to select the complete block which is on the same indention
  level
- `Ctrl/⌘ + Shift + M` to select all within the same bracket
- `Ctrl/⌘ + Shift + Space` to select everything in the same scope
- `Ctrl/⌘ + Shift + A` to select all within the same HTML tag
- `Alt + Shift + Up` to expand selection upwards
- `Alt + Shift + Down` to expand selection downwards

### Move lines up and down

You may switch lines and move the current line up or down using
`Ctrl + Shift + Up` and `Ctrl + Shift + Down` (`Ctrl + ⌘ + ...` on Mac).

### Input shortcuts

Insert line `Ctrl/⌘ + Shift + Enter' before current or `Ctrl/⌘ + Enter` after current.

Copy `Ctrl/⌘ + C` and Cur `Ctrl/⌘ + X` works on current line if no selection.

Use `Ctrl/⌘ + V` to insert and `Ctrl/⌘ + Shift + V` to insert with correct indention.
Also `Ctrl/⌘ + Shift + D` may be used to duplicate selected content.


Use `Ctrl/⌘ + KK` to delete till end of line, `Ctrl/⌘ + Backspace` to delete to start
of line or `Ctrl/⌘ + Shift + K` to delete the current line.

`Ctrl/⌘ + KU` and `Ctrl/⌘ + KL` makes selection upper case or lower case.

Search and Replace
-------------------------------------------------

- `Ctrl/⌘ + F` to open find dialog
- `Ctrl/⌘ + H` to open replacement dialog
- `Ctrl/⌘ + Shift + F` to open multi file find and replace dialog

Within the dialog you may:

- `F3` - Search Forward Using Most Recent Pattern
- `Shift + F3` - Search Backwards Using Most Recent Pattern
- `Alt + F3` - Select All Matches Using Most Recent Pattern
- `Alt + R` - Toggle Regular Expressions
- `Alt + C` - Toggle Case Sensitivity
- `Alt + W` - Toggle Exact Match
- `Enter` - Find Next
- `Shift + Enter` - Find Previous
- `Alt + Enter` - Find All
- `Ctrl/⌘  + Alt + Enter` - Replace All

In Multifile search:

- `F4` - Next File Match
- `Ctrl + F4` - Previous File Match

You may enter a multi line search pattern, use `Ctrl + Enter` therefore.

Commands
-------------------------------------------------

Use `Ctrl/⌘ + Shift + P_` to open the complete command list and search with some
letters within.


Display
-------------------------------------------------

Toggle sidebar using `Ctrl/⌘ + KB`.

Switch between tabs: `Ctrl/⌘ + PgUp` and `Ctrl/⌘ + PgDown` or `Ctrl/⌘ + Shift + t`
to open last closed tab.
