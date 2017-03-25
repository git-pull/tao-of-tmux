# Scripting tmux {#scripting-tmux}

The command line shortcuts and options in tmux is an area often uncharted.

I will use tables in this chapter. Never get a feeling you have to commit a
table to memory immediately. Not my intention, but every person's way of using
tmux is slightly different. I want to cover points most likely to benefit
people's flows. Full tables are in the [cheatsheets](#appendix-cheatsheets).

## Aliases {#aliases}

tmux supports a variety of alias commands. So, don't feel you always have to
type `tmux attach`. *Aliases*, alongside [fnmatch-style pattern commands](#fnmatch),
make it intuitive to type those commands in a pinch.

Most aliases come to mind via intuition and are a lot friendlier than typing the
full hyphenated commands.

{width="narrow"}
| Command             | Alias     |
|---------------------|-----------|
| attach-session      | attach    |
| break-pane          | breakp    |
| capture-pane        | capturep  |
| display-panes       | displayp  |
| find-window         | findw     |
| join-pane           | joinp     |
| kill-pane           | killp     |
| kill-window         | killw     |
| last-pane           | lastp     |
| last-window         | last      |
| link-window         | linkw     |
| list-panes          | lsp       |
| list-windows        | lsw       |
| move-pane           | movep     |
| move-window         | movew     |
| new-session         | new       |
| new-window          | neww      |
| next-layout         | nextl     |
| next-window         | next      |
| pipe-pane           | pipep     |
| previous-layout     | prevl     |
| previous-window     | prev      |
| rename-window       | renamew   |
| resize-pane         | resizep   |
| respawn-pane        | respawnp  |
| respawn-window      | respawnw  |
| rotate-window       | rotatew   |
| select-layout       | selectl   |
| select-pane         | selectp   |
| set-option          | set       |
| set-window-option   | setw      |
| show-options        | show      |
| show-window-options | showw     |
| split-window        | splitw    |
| swap-pane           | swapp     |
| swap-window         | swapw     |
| unlink-window       | unlinkw   |

If you know the full name of the command, if you were to chopped the hyphen
(-) from the command and add the first letter of the last word, you'd get the
shortcut, e.g., **swap**-**w**indow is swapw, **split**-**w**indow is splitw.

## Pattern matching {#fnmatch}

tmux commands and arguments may all be accessed via [`fnmatch(3)`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fnmatch.html)
patterns.

For instance, you need not type `$ tmux attach-session` every time. First,
there's the [alias](#aliases) of `$ tmux attach`, but additionally, more
concise commands can be used if they partially match the name of the command or
the target. tmux' pattern matching allows `$ tmux attac`, `$ tmux att`, `$ tmux at`
and `$ tmux a` to reach `$ tmux attach`.

Every tmux command has shorthands; let's try this for `$ tmux new-session`:

{language=shell, line-numbers=off}
    $ tmux new-session

    $ tmux new-sessio

    # ...

    $ tmux new-s

and so on, until:

{language=shell, line-numbers=off}
    $ tmux new-
    ambiguous command: new-, could be: new-session, new-window

The limitation, as seen above, is command matches can collide. Multiple commands
begin with `new-`. So, if you wanted to use matches, `$ tmux new-s` for a new
session or `$ tmux new-w` for a new window would be the most efficient way. But,
the alias of `$ tmux new` for new session and `$ tmux neww` for new windows is
even more concise than matching, since the special alias exists.

Patterns can also match [targets](#targets) with window and session names. For
instance, a session named `mysession` can be matched via `mys`:

{language=shell, line-numbers=off}
    $ tmux attach -t mys

Collisions to patterns also have a limitation, if there is a `mysession` and
`mysession2` session, means `mys` would match both. To target either session,
the full target name must be specific.

## Targets {#targets}

If a command allows target specification, it's usually done through `-t`.

Think of targets as tmux's way of specifying a [unique key](https://en.wikipedia.org/wiki/Unique_key)
in a relational database.

| Entity    | Prefix | Example                               |
|-----------|--------|---------------------------------------|
| server    | n/a    | n/a, uses socket-name and socket-path |
| client    | n/a    | n/a, uses /dev/tty{p,s}[000-9999]     |
| session   | $      | $13                                   |
| window    | @      | @2313                                 |
| pane      | %      | %5432                                 |

What I use to help me remember:

So, sessions are represented by dollar signs ($) because they hold your projects
(*ostensibly* where you make money or help someone else do it).

Windows are represented by the [at sign](https://en.wikipedia.org/wiki/At_sign)
(@). So, windows are like referencing / messaging a user on a social
networking website.

Panes are the fun one, represented by the percent sign (%), like the
default prompt for [csh](https://en.wikipedia.org/wiki/C_shell) and
[tcsh](https://en.wikipedia.org/wiki/Tcsh). Hey, makes sense, since panes are
pseudoterminals!

Here are some examples of targets, assuming one session named `mysession` and a
client at `/dev/ttys004`:

`$ tmux attach-session [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux attach-session -t mysession

`$ tmux detach-client [-s target-session] [-t target-client]`

{language=shell, line-numbers=off}
    $ tmux detach-client -s mysession -t /dev/ttys004

    # If within client, -t is assumed to be current client
    $ tmux detach-client -s mysession

`$ tmux has-session [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux has-session -t mysession

    # Pattern matching session name
    $ tmux has-session -t mys

`$ tmux kill-session [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux kill-session -t mysession

`$ tmux list-clients [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux list-clients -t mysession

`$ tmux lock-client [-t target-client]`

{language=shell, line-numbers=off}
    $ tmux lock-clients -t /dev/ttys004

`$ tmux lock-session [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux lock-session -t mysession

`$ tmux new-session [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux new-session -t newsession

    # Create new-session in the background
    $ tmux new-session -t newsession -d

`$ tmux refresh-client [-t target-client]`

{language=shell, line-numbers=off}
    $ tmux refresh-client -t /dev/ttys004

`$ tmux rename-session [-t target-session]` session-name

{language=shell, line-numbers=off}
    $ tmux rename-session -t mysession renamedsession

    # If within attached session, -t is assumed
    $ tmux rename-session renamedsession

`$ tmux show-messages [-t target-client]`

{language=shell, line-numbers=off}
    $ tmux show-messages -t /dev/ttys004

`$ tmux suspend-client [-t target-client]`

{language=shell, line-numbers=off}
    $ tmux suspend-client -t /dev/ttys004

    # If already in client
    $ tmux suspend-client

    # bring client back to the foreground
    $ fg

`$ tmux switch-client [-c target-client] [-t target-session]`

{language=shell, line-numbers=off}
    $ tmux suspend-client -c /dev/ttys004 -t othersession

    # Within current client, -c is assumed
    $ tmux suspend-client -t othersession 

## Formats {#formats}

tmux provides a minimal template language and set of variables to access
information about your tmux environment.

Formats are specified via the `-F` flag.

You know how template engines, such as
[mustache](https://mustache.github.io/), [handlebars](http://handlebarsjs.com/)
[ERB](http://ruby-doc.org/stdlib-2.3.3/libdoc/erb/rdoc/ERB.html) in ruby,
[jinja2](http://jinja.pocoo.org/docs/dev/) in python,
[twig](http://twig.sensiolabs.org/) in PHP, and
[JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) in Java, allow template
variables? Formats are a similar concept.

The `FORMATS` (variables) provided by tmux have expanded greatly
since version 1.8. Some of the most commonly used formats as of tmux 2.3 are
listed below. See the [appendix section on formats](#appendix-formats) for a
complete list.

Let's try to output it:

{language=shell, line-numbers=off}
    $ tmux list-windows -F "#{window_id} #{window_name}"
    > @0 zsh

Here's a cool trick; list all panes with the x and y coordinates of the cursor
position:

{language=shell, line-numbers=off}
    $ tmux list-panes -F "#{pane_id} #{pane_current_command} \
      #{pane_current_path} #{cursor_x},#{cursor_y}"
    > %0 vim /Users/me/work/tao-of-tmux/manuscript 0,34
      %1 tmux /Users/me/work/tao-of-tmux/manuscript 0,17
      %2 man /Users/me/work/tao-of-tmux/manuscript 0,0

Variables are specific to the objects being listed. For instance:

Server-wide variables: `host`, `host_short` (no domain name), `socket_path`,
`start_time` and `pid`.

Session-wide variables: `session_attached`, `session_activity`,
`session_created`, `session_height`, `session_id`, `session_name`,
`session_width`, `session_windows` and all server-wide variables.

Window variables: `window_activity`, `window_active`, `window_height`,
`window_id`, `window_index`, `window_layout`, `window_name`, `window_panes`,
`window_width` and all session and server variables.

Pane variables: `cursor_x`, `cursor_y`, `pane_active`, `pane_current_command`,
`pane_current_path`, `pane_height`, `pane_id`, `pane_index`, `pane_width`,
`pane_pid` and all window, session and server variables.

This book gives a great focus to seperating the concept of server, session,
window and panes, a separation existing in user experience, and now also in
tmux' printing attributes. If you `list-panes`, all variables up the ladder,
including window, session and server variables are available for the panes being
listed. Try this:

{language=shell, line-numbers=off}
    $ tmux list-panes -F "pane: #{pane_id}, window: #{window_id}, \
      session: #{session_id}, server: #{socket_path}"
    > pane: %35, window: @13, session: $6, server: /private/tmp/tmux-501/default
      pane: %38, window: @13, session: $6, server: /private/tmp/tmux-501/default
      pane: %36, window: @13, session: $6, server: /private/tmp/tmux-501/default

Listing windows isn't designed to display variables for pane-specific propreties.
Since a window is a collection of panes, it can have 1 or more panes open at any
time.

{language=shell, line-numbers=off}
    $ tmux list-windows -F "window: #{window_id}, panes: #{window_panes} \
      pane_id: #{pane_id}"
    > window: @15, panes: 1 pane_id: %40
      window: @13, panes: 3 pane_id: %36
      window: @25, panes: 1 pane_id: %50

This will show the window ID, which is prefixed by an `@` symbol, as well as the
number of panes inside the window.

Surprisingly, `pane_id` shows up via `list-windows`, as of tmux 2.3. While this
behavior happens now, it's advised to keep use of `-F` scoped to the objects
being listing, when scripting, to avoid breakage. For instance, if you want the
active pane, use `#{pane_active}` via `$ tmux list-panes -F "#{pane_active}"`.
