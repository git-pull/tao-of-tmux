
{mainmatter}

# Thinking in tmux {#chapter-01}

tmux is geared for developers and admins who interact regularly with CLI
(text-only interfaces)

In the world of computers, there are 2 realms:

1. The text realm
2. The graphical realm

tmux resides in the text realm. This is about fixed-width fonts and that old
fashioned black terminal.

## Window manager for the terminal

tmux is to the console what a desktop is to gui apps. It's a world inside the
text dimension. Inside tmux you can:

- multitask inside the terminal, run multiple applications
- have multiple command lines (pane) in the same window
- have multiple windows (window) in the workspace (session)
- switch between multiple workspaces, like virtual desktops

|**tmux**           |**"Desktop"-Speak**   |**Plain English**                  |
|-------------------|----------------------|-----------------------------------|
|Multiplexer        |Multi-tasking         |Multiple applications              |
|                   |                      |simulataneously.                   |
|-------------------|----------------------|-----------------------------------|
|Session            |Desktop               |Applications are visible here      |
|-------------------|----------------------|-----------------------------------|
|Window             |Virtual Desktop or    |A desktop that stores it own screen|
|                   |applications          |screen			       |
|-------------------|----------------------|-----------------------------------|
|Pane               |Application           |Performs operations                |

## Multitasking

tmux gives you prime oppurtunity to do many things at once in one screen.

For one you can keep multiple terminals running on the same display.

But you also have the concept of shuffling between multiple "windows" within
that, all within the confines of the tmux session you attached.

Even better, there are facilities to copy and paste, scroll. No requirement
for graphics either, so you have full power even if you're SSH'ing or in a
tty without X.

## Keep your applications running in the background

Sometimes in GUI applications you'll have an option to minimize and application
to a tray ground.  The application is out of the sight, but running in the
background.

In tmux, a similar concept exists where we can "detach" a tmux session.

So here are a few common scenarios:

A system administrator will run a `tail -F /var/log/apache2/error.log` in a
pane to get a live stream of the latest system events.

Running a file watcher like [watchman](https://github.com/facebook/watchman),
[gulp-watch](https://github.com/gulpjs/gulp/blob/master/docs/API.md#gulpwatchglob-opts-tasks),
[grunt-watch](https://github.com/gruntjs/grunt-contrib-watch)
or [entr](http://entrproject.org/).

Keeping a text editor like vim, emacs, pico, nano, etc. open in a main pane,
while leaving two other open for CLI commands and building via `make` or
`ninja`.

{width=50%,float=right}
![Chatting on weechat w/ tmux](images/01-thinking-tmux/weechat.png)

Chatting on [irssi](https://irssi.org/) or [weechat](https://weechat.org/),
one of the "classic combos", along with a [bitlbee](https://www.bitlbee.org)
server to manage AIM, MSN, Google Talk, Jabber, ICQ, even twitter. Then you can
detach your IRC and "idle" in your favorite channels, stay online on instant
messengers, and get back to your messages when you return.

Any general workspace you'd normally use in a terminal for any task, with the
benefit of you being able to persist it

Q> ### Does tmux persist sessions after restarts?
Q>
Q> Unfortunately not. A restart will kill the tmux server.
Q>
Q> Thankfully, the modern server can stay online for a long time. Even for
Q> consumer laptops and PC's with a day or two uptime, having tmux persist
Q> tasks for organizational purposes is satisfactory to run it.
Q>
Q> For tasks you repeat often, you can always use a tool like
Q> [tmuxp](https://github.com/tony/tmuxp), [tmuxinator](https://github.com/tmuxinator/tmuxinator)
Q> or [teamocil](https://github.com/remiprev/teamocil) to resume common
Q> sessions.
Q>
Q> It comes at a disappointment, because some are interested in the idea of
Q> being able to persist a tree of processes after restart. That goes out of
Q> scope of what tmux is meant to do.
