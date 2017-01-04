# Window {#windows}

If this is the beginning of the Windows chapter, I guess you can assume we'll
cover [panes](#panes) next. Windows are the containers within
[session](#session) that hold panes.

![Window](images/info/window.png)

You can see the current open windows through the status bar.

## (Re)naming windows

Just like with sessions, windows can have names. And it is important to label
them to keep track of what you're doing inside them.

![Renaming](images/06-window/rename.png)

`Prefix` + `,` will turn the tmux status line into an input field where the current
active window's name can be altered.

## Traversing Windows

`Prefix` + `1`, `Prefix` + `2`, and so on... will get you to navigate to windows
by their index.

Prompt for a window index (useful for indexes greater than 9) with `Prefix` +
`'`.

I> ### POWER MOVE: Search + Traverse Windows for Text
I> 
I> You can forward to a window with a match of a text string by doing `Prefix` +
I> `f`.

You can move to the last selected window with `Prefix` + `l`.

You can bring up a list of current windows with `Prefix` + `w`. The benefit of
this is it also gives you some info on what's inside the window. Very helpful if
you're juggling around a lot of things!

## Moving Windows

`$ tmux move-window` can be used to move windows.

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

### Layouts {#window-layouts}

`Prefix` + `space` switches layouts.

To do specific touch-ups you can (resize panes)[#resizing-panes].
