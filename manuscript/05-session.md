# Session {#sessions}

Welcome to the session. Being the highest level entity after your
[server](#server). Regardless of whether you're starting tmux fresh
or attaching an already created one, your interaction with tmux will
have to have at least one session running.

A session will hold one or more [windows](#windows). Your tmux status bar,
found at the bottom, will include a list of windows.

![Session](images/info/session.png)

The window you have selected currently may have a special color or a `*` symbol
next to it.

![The first window, ID 1, titled "manuscript" is active. The second window, ID 2, titled zsh.](images/05-session/active-window.png)

## Switching sessions within tmux

I've seen some people acquire a habit of detaching their tmux client, and
trying to reattach via `tmux att -t session_name`. Thankfully, you have the
ability to switch to session from within tmux!

### Keystroke

| Short cut        | Action
|------------------|----------------------------------------------------|
|`s`               | Select a new session for the attached client       |
|                  | interactively.                                     |
|`(`               | Switch the attached client to the previous session.|
|`)`               | Switch the attached client to the next session.    |
|`L`               | Switch the attached client back to the last        |
|                  | session.                                           |


`Ctrl-b s` will allow you to switch between sessions within the same tmux
client.

### Command line

{language=shell, line-numbers=off}
    $ tmux switch-client [-Elnpr] [-c target-client] [-t target-session]

## Renaming a tmux session

### Keystroke

You can rename sessions with `Ctrl-b $`.  The status bar will be temporarily
altered into a text field to allow altering the session name.

### Command line

{language=shell, line-numbers=off}
    $ tmux rename-session [-t target-session] new-name
