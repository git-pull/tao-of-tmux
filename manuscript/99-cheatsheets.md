# Cheatsheets {#appendix-cheatsheets}

## Commands

### Session

| Command          | Action                                                   |
|------------------|----------------------------------------------------------|
| no command       | short-cut for `new-session`                              |
| `new-session`    |                                                          |
| `kill-session`   | terminate session                                        |
| `attach-session` | attach session                                           |
| `rename-session` | rename session                                           |
| `list-sessions`  |                                                          |
| `lock-session`   |                                                          |
| `choose-session` |                                                          |
| `has-session`    |                                                          |

### Window

| Command       | Action                                                 |
|---------------|--------------------------------------------------------|
| `new-window`  |                                                        |

## Keybindings

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-b`             | Send the prefix key (C-b) through to the           |
|                  | application.                                       |

### Miscellaneous

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-z`             | Suspend the tmux client.                           |
|`r`               | Force redraw of the attached client.               |
|`t`               | Show the time.                                     |
|`~`               | Show previous messages from tmux, if any.          |
|`f`               | Prompt to search for text in open windows.         |
|`d`               | Detach the current client.                         |
|`D`               | Choose a client to detach.                         |
|`?`               | List all key bindings.                             |
|`:`               | Enter the tmux command prompt.                     |

### Copy/Paste

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`#`               | List all paste buffers.                            |
|`[`               | Enter copy mode to copy text or view the history.  |
|`]`               | Paste the most recently copied buffer of text.     |
|`Page Up`         | Enter copy mode and scroll one page up.            |
|`=`               | Choose which buffer to paste interactively from a  |
|                  | list.                                              |
|`-`               | Delete the most recently copied buffer of text.    |

### Session

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`$`               | Rename the current session.                        |

#### Session Traversal

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`L`               | Switch the attached client back to the last        |
|                  | session.                                           |
|`s`               | Select a new session for the attached client       |
|                  | interactively.                                     |

### Window

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`c`               | Create a new window.                               |
|`&`               | Kill the current window.                           |
|`i`               | Display some information about the current window. |
|`,`               | Rename the current window.                         |

#### Window Traversal

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`0 to 9`          | Select windows 0 to 9.                             |
|`w`               | Choose the current window interactively.           |
|`M-n`             | Move to the next window with a bell or activity    |
|                  | marker.                                            |
|`M-p`             | Move to the previous window with a bell or activity|
|                  | marker.                                            |
|`p`               | Change to the previous window.                     |
|`n`               | Change to the next window.                         |
|`l`               | Move to the previously selected window.            |
|`'`               | Prompt for a window index to select.               |

#### Window Moving

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`.`               | Prompt for an index to move the current window.    |

### Pane

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`x`               | Kill the current pane.                             |
|`q`               | Briefly display pane indexes.                      |
|`%`               | Split the current pane into two, left and right.   |
|`"`               | Split the current pane into two, top and bottom.   |

#### Pane Traversal

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`;`               | Move to the previously active pane.                |
|`Up, Down`        | Change to the pane above, below, to the left, or to|
|`Left, Right`     | the right of the current pane.                     |
|`o`               | Select the next pane in the current window.        |

#### Pane Moving

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`C-o`             | Rotate the panes in the current window forwards.   |
|`M-o`             | Rotate the panes in the current window backwards.  |
|`{`               | Swap the current pane with the previous pane.      |
|`}`               | Swap the current pane with the next pane.          |
|`!`               | Break the current pane out of the window.          |

#### Pane Resizing

| Shortcut        | Action                                             |
|------------------|----------------------------------------------------|
|`M-1 to M-5`      | Arrange panes in one of the five preset layouts:   |
|                  | even-horizontal, even-vertical, main-horizontal,   |
|                  | main-vertical, or tiled.                           |
|`C-Up, C-Down`    | Resize the current pane in steps of one cell.      |
|`C-Left, C-Right` |                                                    |
|`M-Up, M-Down`    | Resize the current pane in steps of five cells.    |
|`M-Left, M-Right` |                                                    |
