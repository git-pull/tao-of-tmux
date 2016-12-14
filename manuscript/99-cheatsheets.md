# Cheatsheets {#appendix-cheatsheets}

## Commands

### Session

| Command       | Action                                                 |
|---------------|--------------------------------------------------------|
| no command    |                                                        |
| `new-session` |                                                        |

### Window

| Command       | Action                                                 |
|---------------|--------------------------------------------------------|
| `new-window`  |                                                        |

## Config

## Formats

## Keybindings

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-b`             | Send the prefix key (C-b) through to the           |
|                  | application.                                       |

### Miscellaneous

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-z`             | Suspend the tmux client.                           |
|`r`               | Force redraw of the attached client.               |
|`t`               | Show the time.                                     |
|`~`               | Show previous messages from tmux, if any.          |

### Copy/Paste

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`#`               | List all paste buffers.                            |
|`[`               | Enter copy mode to copy text or view the history.  |
|`]`               | Paste the most recently copied buffer of text.     |
|`Page Up`         | Enter copy mode and scroll one page up.            |

### Session Traversal

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`L`               | Switch the attached client back to the last        |
|                  | session.                                           |
|`s`               | Select a new session for the attached client       |
|                  | interactively.                                     |

### Window traversal

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`0 to 9`          | Select windows 0 to 9.                             |
|`w`               | Choose the current window interactively.           |
|`M-n`             | Move to the next window with a bell or activity    |
|                  | marker.                                            |
|`M-p`             | Move to the previous window with a bell or activity|
|                  | marker.                                            |

### Pane

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`x`               | Kill the current pane.                             |

### Pane traversal

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`;`               | Move to the previously active pane.                |
|`Up, Down`        | Change to the pane above, below, to the left, or to|
|`Left, Right`     | the right of the current pane.                     |



### Pane moving

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-o`             | Rotate the panes in the current window forwards.   |
|`M-o`             | Rotate the panes in the current window backwards.  |
|`{`               | Swap the current pane with the previous pane.      |
|`}`               | Swap the current pane with the next pane.          |

### Pane resizing

| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`M-1 to M-5`      | Arrange panes in one of the five preset layouts:   |
|                  | even-horizontal, even-vertical, main-horizontal,   |
|                  | main-vertical, or tiled.                           |
|`C-Up, C-Down`    | Resize the current pane in steps of one cell.      |
|`C-Left, C-Right` |                                                    |
|`M-Up, M-Down`    | Resize the current pane in steps of five cells.    |
|`M-Left, M-Right` |                                                    |


| Short cut        | Action                                             |
|------------------|----------------------------------------------------|
|`!`               | Break the current pane out of the window.          |
|`"`               | Split the current pane into two, top and bottom.   |
|`$`               | Rename the current session.                        |
|`%`               | Split the current pane into two, left and right.   |
|`&`               | Kill the current window.                           |
|`'`               | Prompt for a window index to select.               |
|`,`               | Rename the current window.                         |
|`-`               | Delete the most recently copied buffer of text.    |
|`.`               | Prompt for an index to move the current window.    |
|`:`               | Enter the tmux command prompt.                     |
|`=`               | Choose which buffer to paste interactively from a  |
|                  | list.                                              |
|`?`               | List all key bindings.                             |
|`D`               | Choose a client to detach.                         |
|`c`               | Create a new window.                               |
|`d`               | Detach the current client.                         |
|`f`               | Prompt to search for text in open windows.         |
|`i`               | Display some information about the current window. |
|`l`               | Move to the previously selected window.            |
|`n`               | Change to the next window.                         |
|`o`               | Select the next pane in the current window.        |
|`p`               | Change to the previous window.                     |
|`q`               | Briefly display pane indexes.                      |
