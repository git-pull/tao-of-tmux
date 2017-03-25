# Panes {#panes}

Panes are [pseudoterminals](https://en.wikipedia.org/wiki/Pseudoterminal)
encapsulating shells (e.g. Bash, Zsh). They reside within a [window](#windows).
A terminal within a terminal, which can run shell commands, scripts, programs
like vim, emacs, top, htop, irssi, weechat and so on from within them.

![](images/info/pane.png)

## Creating new panes

To create a new pane, you can `split-window` from within the current
[window](#windows) and pane you are in.

| Shortcut         | Action                                             |
|------------------|----------------------------------------------------|
|`Prefix` + `%`    | `split-window -h` (split horizontally)             |
|`Prefix` + `"`    | `split-window -v` (split vertically)               |

You can continue to create panes until you've reached the limit of what the
terminal can fit. This depends on the dimensions of your terminal. A normal
window will usually have 1 to 5 panes open.

Example usage:

{language=shell, line-numbers=off}
    # Create pane horizontally, $HOME directory, 50% width of current pane
    $ tmux split-window -h -c $HOME -p 50 vim

{width=75%}
![](images/07-pane/splitw/-h -c $HOME -p 50 vim - 2 panes.png)

{language=shell, line-numbers=off}
    # create new pane, split vertically with 75% height
    tmux split-window -p 75

{width=75%}
![](images/07-pane/splitw/-p 75.png)

{pagebreak}

## Traversing Panes {#pane-traversal}

| Shortcut         | Action                                             |
|------------------|----------------------------------------------------|
|`Prefix` + `;`    | Move to the previously active pane.                |
|`Prefix` + `Up` / | Change to the pane above, below,                   |
|`Down` / `Left` / | to the left, or to the                             |
|`Right`           | the right of the current pane.                     |
|`Prefix` + `o`    | Select the next pane in the current window.        |

I> *Movin around vimtuitively*
I>
I> If you like vim (hjkl) keybindings, add these to your [config](#config):
I>
I> {language=shell, line-numbers=off}
I>     # hjkl pane traversal
I>     bind h select-pane -L
I>     bind j select-pane -D
I>     bind k select-pane -U
I>     bind l select-pane -R

## Zoom in

To zoom in on a pane, navigate to it and do `Prefix` + `z`.

You can use any [pane traversal](#pane-traversal) to unzoom and move a pane at
the same time.

## Resizing panes {#resizing-panes}

Pane size can be adjusted within [windows](#windows) via [window layouts](#window-layouts)
and `resize-pane`. Adjusting window layout switches the proportions and order of
the panes. Resizing the panes targets a specific pane inside the window
containing it, also shrink or growing the size of the other columns or rows. It's like
adjusting your car seat or reclining on a flight, if you take up more space,
something else will also have less space.

| Shortcut         | Action              |
|------------------|---------------------|
|`Prefix M-Up`     | `resize-pane -U 5`  |
|`Prefix M-Down`   | `resize-pane -D 5`  |
|`Prefix M-Left`   | `resize-pane -L 5`  |
|`Prefix M-Right`  | `resize-pane -R 5`  |
|`Prefix C-Up`     | `resize-pane -U`    |
|`Prefix C-Down`   | `resize-pane -D`    |
|`Prefix C-Left`   | `resize-pane -L`    |
|`Prefix C-Right`  | `resize-pane -R`    |

## Outputting pane to a file

You can output the display of a pane to a file.

{language=shell, line-numbers=off}
    $ tmux pipe-pane -o 'cat >>~/output.#I-#P'

The `#I` and `#P` are [formats](#formats) for window index and pane index, so
the file created is unique. Clever!

## Summary

Panes are shells within a shell. You can keep adding panes to a tmux window
until you run out of room on your screen. Within your shell, you can `tail -F`
log files, write and run scripts, an run [curses](https://en.wikipedia.org/wiki/Curses_(programming_library))-powered
applications like vim, top, htop, ncmpcpp, irssi, weechat, mutt and so on.

You will always have at least one pane open. Once you kill the last pane in
the window, the window will close. Panes are also resizable; you can resize
panes via targetting them specifically and changing the window layout.

In the next chapter, we will go into the ways you can customize your tmux
shortcuts, status line and behavior.
