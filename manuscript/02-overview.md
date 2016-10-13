# Thinking in tmux

tmux is geared for developers and admins who interact regularly with
CLI (text-only interfaces)

In the world of computers, there are 2 realms:

1. The text realm
2. The graphical realm

Tmux resides in the text realm. This is about fixed-width fonts and that
old fashioned black terminal.

## So what does tmux help me do in the terminal?

tmux is to the console what a desktop is to gui apps. It's a world inside
the text dimension. Inside tmux you can:

- multitask inside the terminal, run multiple applications.
- have multiple command lines (pane) in the same window
- have multiple windows (window) in the workspace (session)
- switch between multiple workspaces, like virtual desktops

|**tmux**               |**"Desktop"-Speak**       |**Plain English**                 |
|-------------------|----------------------|------------------------------|
|Multiplexer        |Multi-tasking         |Multiple applications         |
|                   |                      |simulataneously.              |
|-------------------|----------------------|------------------------------|
|Session            |Desktop               |Applications are visible here |
|-------------------|----------------------|------------------------------|
|Window             |Virtual Desktop or    |A desktop that stores it own  |
|                   |applications          |screen			  |
|-------------------|----------------------|------------------------------|
|Pane               |Application           |Performs operations           |
