# Windows {#windows}

Windows hold [panes](#panes). They reside within a [session](#sessions).

They also have [layouts](#window-layouts), which can be one of many preset
dimensions or a custom one done through [pane resizing](#pane-resizing).

![](images/info/window.png)

You can see the current windows through the [status bar](#status-bar)
located at the bottom of tmux.

## Creating windows

All sessions start with at least 1 window open. From there, you can create and
kill windows as you see fit.

Window indexes are a number tmux uses to determine ordering. The first window's
index is 0, unless you set it via `base-index` in your [configuration](#config).
I usually `set -g base-index 1` in my tmux configuration since 0 is after 9 on
the keyboard.

`Prefix` + `c` will create a new at the first open index. So if you're in the
first window, and there is no second window created yet, it will create the
second window. If the second window is already taken, and the third hasn't
been created yet, it will create the third window.

If the `base_index` is 1, and there are 7 windows created, with the 5th window
missing, creating a new window will fill the empty 5th index, since it's the
next one in order and nothing is filling it. The next created window would be
the eighth.

## Naming windows

Just like with sessions, windows can have names. Labelling them helps keep track
of what you're doing inside them.

![Renaming](images/06-window/rename.png)

When inside tmux, the shortcut of `Prefix` + `,` is most commonly used. It
opens a prompt in the tmux status line, where you can alter the name of the
current window.

The default numbers given to windows also become muscle memory after a while.
But naming helps you when you're in a new tmux flow and want to organize
yourself. Also, if you're sharing tmux with another user it's good practice to
give a hint what's inside the windows.

## Traversing windows

Moving around windows is done in two ways. First, by iterating through via
`Prefix` + `p` and `Prefix` + `n`, and via the window index, which takes you
directly to a specific window.

`Prefix` + `1`, `Prefix` + `2`, and so on... allows quickly navigating to
windows via their index. Unlike window names, which change, indexes are
consistent and only require a quick key combo for you to invoke.

Prompt for a window index (useful for indexes greater than 9) with `Prefix` +
`'`. If the window index is 10 or above, this will help you a lot.

I> ### POWER MOVE: Search + Traverse Windows for Text
I> 
I> You can forward to a window with a match of a text string by doing `Prefix` +
I> `f`.

Bring up the last selected window with `Prefix` + `l`.

A list of current windows can be displayed with `Prefix` + `w`. This also gives
some info on what's inside the window. Helpful when juggling around a lot of
things!

## Moving windows

Windows themselves can also be reordered one by one via `move-window` and its
associated shortcut. This is helpful if a window is worth keeping open but not
important or rarely looked at. After you move a window, you can continue to
reorder them at any point in time after.

The command `$ tmux move-window` can be used to move windows.

The accepted arguments are `-s` (the window you are moving) and `-t`, where you
are moving the window to.

You can also use `$ tmux movew` for short.

Example: move the current window to number 2:

{language=shell, line-numbers=off}
    $ tmux movew -t2

Example: move window 2 to window 1:

{language=shell, line-numbers=off}
    $ tmux movew -s2 -t1

The shortcut to prompt for an index to move the current window to is `Prefix` +
`.`.

## Layouts {#window-layouts}

`Prefix` + `space` switches window *layouts*. These are preset configurations
automatically adjusting proportions of [panes](#panes).

As of tmux 2.3, the supported layouts are:

{width=75%}
![](images/06-window/even-horizontal.png)

{width=75%}
![](images/06-window/even-vertical.png)

{width=75%}
![](images/06-window/main-horizontal.png)

{width=75%}
![](images/06-window/main-vertical.png)

{width=75%}
![](images/06-window/tiled.png)

Specific touch-ups can be done via [resizing panes](#resizing-panes).

To reset the proportions of the layout (such as after splitting or resizing
panes), you have to run `$ tmux select-layout` again for the layout.

This is different behavior than some [tiling window managers](https://en.wikipedia.org/wiki/Tiling_window_manager).
[*awesome*](https://awesomewm.org/) and [*xmonad*](http://xmonad.org/), for
instance, automatically handle proportions upon new items being added to their
layouts.

To allow easy resetting to a sensible layout across machines and terminal
dimensions, you can try this in your [config](#config):

{language=shell, line-numbers=off}
    bind m set-window-option main-pane-height 60\; select-layout main-horizontal

This allows you to set a `main-horizontal` layout and automatically set the
bottom panes proportionally on the bottom every time you do `Prefix` + `m`.

Layouts can also be custom. To get the custom layout snippet for your current
window, try this:

{language=shell, line-numbers=off}
    $ tmux lsw -F "#{window_active} #{window_layout}" | grep "^1" | cut -d " " -f2

To apply this layout:

{language=shell, line-numbers=off}
    $ tmux lsw -F "#{window_active} #{window_layout}" | grep "^1" | cut -d " " -f2
    > 5aed,176x79,0,0[176x59,0,0,0,176x19,0,60{87x19,0,60,1,88x19,88,60,2}]

    # resize your panes or try doing this in another window to see the outcome
    $ tmux select-layout "5aed,176x79,0,0[176x59,0,0,0,176x19,0,60{87x19,0,60,1,88x19,88,60,2}]"

## Closing windows

There are two ways to kill a window. First, exit or kill every pane in the
window. Panes can be killed via `Prefix` + `x` or by `Ctrl` + `d` within
the pane's shell. The second way, `Prefix` + `&`, which prompts if you really
want to delete the window. Warning: this will destroy all panes inside, and any
processes.

From inside the current window, try this:

{language=shell, line-numbers=off}
    $ tmux kill-window

Another thing, when [scripting](#scripting-tmux) or trying to kill the window
from outside, use a [target](#targets) of the window index:

{language=shell, line-numbers=off}
    $ tmux kill-window -t2

If you're trying to find the target of the window to kill, they reside in the number
in the middle section of the [status line](#status-line), and via `$ tmux
choose-window`. You can hit "return" after you're in choose-window to go back to
where you were previously.

## Summary

In this chapter, you learned how to manipulate windows via renaming and changing
their layouts. To top it off, some advanced functionality you can use to kill
windows in a pinch or in shell scripting tmux. In addition, how to save any tmux
layouts via outputting the `window_layout` template variable.

If you are in a tmux session, you'll always have at least one window open, and
you'll be in it. And within the window will be 1 shell, or "pane". When all the
panes close, the window closes too. In the next chapter, we'll go deeper into
panes.
