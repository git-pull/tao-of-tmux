# Cheatsheets {#appendix-cheatsheets}

## Commands

### Session

| Command          | Action                                                   |
|------------------|----------------------------------------------------------|
| no command       | Short-cut for `new-session`                              |
| `attach-session` | Attach or switch to a session                            |
| `choose-session` | Put a window into session choice mode                    |
| `has-session`    | Check and report if a session exists on the server       |
| `kill-session`   | Destroy a given session                                  |
| `list-sessions`  | List sessions managed by server                          |
| `lock-session`   | Lock all clients attached to a session                   |
| `new-session`    | Create a new session                                     |
| `rename-session` | Rename a session                                         |

### Window

| Command              | Action                                               |
|----------------------|------------------------------------------------------|
| `choose-window`      | Put a window into window choice                      |
| `find-window`        | Search for a pattern in windows                      |
| `kill-window`        | Destroy a given window                               |
| `last-window`        | Select the previously selected                       |
| `link-window`        | Link a window to another                             |
| `list-windows`       | List windows of a session                            |
| `move-window`        | Move a window to another                             |
| `new-window`         | Create a new window                                  |
| `next-window`        | Move to the next window in a sesssion                |
| `previous-window`    | Move to the previous window in session               |
| `rename-window`      | Rename a window                                      |
| `respawn-window`     | Reuse a window in which a command has exited         |
| `rotate-window`      | Rotate positions of panes in a window                |
| `select-window`      | Select a window                                      |
| `set-window-option`  | Set a window option                                  |
| `show-window-options`| Show window options                                  |
| `split-window`       | Splits a pane into two                               |
| `swap-window`        | Swap two windows                                     |
| `unlink-window`      | Unlink a window                                      |

### Pane

| Command         | Action                                                    |
|-----------------|-----------------------------------------------------------|
| `break-pane`    | Break a pane from an existing into a new window           |
| `capture-pane`  | Capture the contents of a pane to a buffer                |
| `display-panes` | Display an indicator for each visible pane                |
| `join-pane`     | Split a pane and move an existing one into the new space  |
| `kill-pane`     | Destroy a given pane                                      |
| `last-pane`     | Select the previously selected pane                       |
| `list-panes`    | List panes of a window                                    |
| `move-pane`     | Move a pane into a new space                              |
| `pipe-pane`     | Pipe output from a pane to a shell command                |
| `resize-pane`   | Resize a pane                                             |
| `respawn-pane`  | Reuse a pane in which a command has exited                |
| `select-pane`   | Make a pane the active one in the window                  |
| `swap-pane`     | Swap two panes                                            |

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
