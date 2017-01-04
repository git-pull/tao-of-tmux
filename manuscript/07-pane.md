# Panes {#panes}

Panes are [pseudoterminals](https://en.wikipedia.org/wiki/Pseudoterminal) that
contain your shell (e.g. Bash, ZSH). They reside within a [window](#windows).

![Pane](images/info/pane.png)

## Traversing Panes {#pane-traversal}

| Shortcut         | Action                                             |
|------------------|----------------------------------------------------|
|`Prefix` + `;`    | Move to the previously active pane.                |
|`Prefix`+ `Up` /  | Change to the pane above, below,                   |
|`Down` / `Left` / | to the left, or to the                             |
|`Right`           | the right of the current pane.                     |
|`Prefix` + `o`    | Select the next pane in the current window.        |

I> *Movin around vimtuitively*
I>
I> Also, if you like vim (hjkl) keybindings, add these to your [config](#config):
I>
I> {language=shell, line-numbers=off}
I>     # hjkl pane traversal
I>     bind h select-pane -L
I>     bind j select-pane -D
I>     bind k select-pane -U
I>     bind l select-pane -R

## Zoom in

To zoom in on a pane, navigate it and do `Leader` + `z`.

You can use any [pane traversal](#pane-traversal) to unzoom and move a pane at
the same time.

### Resizing panes {#resizing-panes}

Panes can be resized within [windows](#windows).

Another technique that resizes panes is [window layouts](#window-layouts). The
difference is a window layout switch the proportions and order of the panes.
Resizing the panes target a specific pane inside that window.

Resizing a pane in a specific layout may subsequently resize that whole row.
