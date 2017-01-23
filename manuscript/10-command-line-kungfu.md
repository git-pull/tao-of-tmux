# Scripting tmux {#scripting-tmux}

The command line in tmux is one of those areas often uncharted.

I will use some tables in this chapter. Never get a feeling that you have to
commit a table to memory immediately. Not my intention, but every person's way
of using tmux is slightly different, I want to be able to cover points most
likely to benefit people's flows. Full tables are in the
[cheatsheets](#appendix-cheatsheets).

## Aliases {#aliases}

tmux supports a variety of alias commands. So don't feel you always have to type
`tmux attach`. *Aliases*, alongside [fnmatch-style pattern commands](#fnmatch)
make it very intuitive to type those commands in a pinch.

Most of these aliases come to mind via intuition and are a lot friendlier than
typing the full hyphenated commands.

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

If you already know the full name of the command, if you were to chop the hyphen
(-) from the command and add the first letter of the last word, you'd get the
shortcut. e.g. **swap**-**w**indow is swapw, **split**-**w**indow is splitw.

## Pattern matching {#fnmatch}

tmux commands and arguments may all be accessed via [`fnmatch(3)`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fnmatch.html)
patterns.

For instance, you don't need to type `$ tmux attach-session` every time. First
there's the [alias](#aliases) of `$ tmux attach`, but *in addition* to that, you
can pattern match `$ tmux attac`, `$ tmux att`, `$ tmux at` and `$ tmux a` work
as well.

Every tmux command has shorthands, let's try this for `$ tmux new-session`:

{language=shell, line-numbers=off}
    $ tmux new-session

    $ tmux new-sessio

    # ...

    $ tmux new-s

and so on, until:

{language=shell, line-numbers=off}
    $ tmux new-
    ambiguous command: new-, could be: new-session, new-window

The limitation, as seen above, is command matches can collide. There are
multiple commands which begin with `new-`. So, if you wanted to use matches,
`$ tmux new-s` for a new session, or `$ tmux new-w` for a new window would be
the most efficient way. But the alias of `$ tmux new` for new session and
`$ tmux neww` for new windows is even better than the matching in that case.

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

So sessions are represented by dollar signs ($) because they hold your projects
(*ostensibly* where you make money, or help someone else do it).

Windows are represented by the [at sign](https://en.wikipedia.org/wiki/At_sign)
(@). So windows are kind of like referencing / messaging a user on a social
networking website.

Panes are the fun one, represented by the percent sign (%), like the
default prompt for [csh](https://en.wikipedia.org/wiki/C_shell) and
[tcsh](https://en.wikipedia.org/wiki/Tcsh). Hey, makes sense, since panes are
pseudoterminals!

To give you an idea of the possibilities of where you can use targets, here are
the commands with you can use targets:

`$ tmux attach-session [-t target-session]`

`$ tmux detach-client [-s target-session] [-t target-client]`

`$ tmux has-session [-t target-session]`

`$ tmux kill-session [-t target-session]`

`$ tmux list-clients [-t target-session]`

`$ tmux lock-client [-t target-client]`

`$ tmux lock-session [-t target-session]`

`$ tmux new-session [-t target-session]`

`$ tmux refresh-client [-t target-client]`

`$ tmux rename-session [-t target-session]`

`$ tmux show-messages [-t target-client]`

`$ tmux suspend-client [-t target-client]`

`$ tmux switch-client [-c target-client] [-t target-session]`

## Formats {#formats}

tmux provides a minimal template language and set of variables you can use to
access information about your tmux environment.

Formats are specified via the `-F` flag.

You know how template engines such as
[mustache](https://mustache.github.io/), [handlebars](http://handlebarsjs.com/)
[ERB](http://ruby-doc.org/stdlib-2.3.3/libdoc/erb/rdoc/ERB.html) in ruby,
[jinja2](http://jinja.pocoo.org/docs/dev/) in python,
[twig](http://twig.sensiolabs.org/) in PHP and
[JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) in Java allow template
variables? Formats are a similar concept.

The amount of `FORMATS` (variables) made available by tmux has expanded greatly
since version 1.8. Some of the most commonly used formats as of tmux 2.3 are
listed below. See the [appendix section on formats](#appendix-formats) for a
complete list.

Let's try to output it:

{language=shell, line-numbers=off}
    $ tmux list-windows -F "#{window_id} #{window_name}"
    > @0 zsh

Here's a cool trick, list all panes with the x and y coordinates of the cursor
position:

{language=shell, line-numbers=off}
    $ tmux list-panes -F "#{pane_id} #{pane_current_command} \
      #{pane_current_path} #{cursor_x},#{cursor_y}"
    > %0 vim /Users/me/work/tao-of-tmux/manuscript 0,34
      %1 tmux /Users/me/work/tao-of-tmux/manuscript 0,17
      %2 man /Users/me/work/tao-of-tmux/manuscript 0,0

### Panes

{width="wide"}
| Variable name         | Description                              |
|-----------------------|------------------------------------------|
| cursor_x              |Cursor X position in pane                 |
| cursor_y              |Cursor Y position in pane                 |
| pane_active           |1 if active pane                          |
| pane_current_command  |Current command if available              |
| pane_current_path     |Current path if available                 |
| pane_dead             |1 if pane is dead                         |
| pane_dead_status      |Exit status of process in dead pane       |
| pane_height           |Height of pane                            |
| pane_id               |Unique pane ID (Alias: #D)                |
| pane_in_mode          |If pane is in a mode                      |
| pane_index            |Index of pane (Alias: #P)                 |
| pane_pid              |PID of first process in pane              |
| pane_start_command    |Command pane started with                 |
| pane_title            |Title of pane (Alias: #T)                 |
| pane_tty              |Pseudo terminal of pane                   |
| pane_width            |Width of pane                             |

### Sessions

{width="wide"}
| Variable name         | Description                              |
|-----------------------|------------------------------------------|
| session_attached      |Number of clients session is attached to  |
| session_activity      |Integer time of session last activity     |
| session_created       |Integer time session created              |
| session_last_attached |Integer time session last attached        |
| session_group         |Number of session group                   |
| session_grouped       |1 if session in a group                   |
| session_height        |Height of session                         |
| session_id            |Unique session ID                         |
| session_many_attached |1 if multiple clients attached            |
| session_name          |Name of session (Alias: #S)               |
| session_width         |Width of session                          |
| session_windows       |Number of windows in session              |

### Windows

{width="wide"}
| Variable name         | Description                              |
|-----------------------|------------------------------------------|
| window_activity       |Integer time of window last activity      |
| window_activity_flag  |1 if window has activity                  |
| window_active         |1 if window active                        |
| window_bell_flag      |1 if window has bell                      |
| window_flags          |Window flags (Alias: #F)                  |
| window_height         |Height of window                          |
| window_id             |Unique window ID                          |
| window_index          |Index of window (Alias: #I)               |
| window_layout         |Window layout description, ignoring zoomed|
|                       |window panes                              |
| window_linked         |1 if window is linked across sessions     |
| window_name           |Name of window (Alias: #W)                |
| window_panes          |Number of panes in window                 |
|                       |zoomed window panes                       |
| window_width          |Width of window                           |
| window_zoomed_flag    |1 if window is zoomed                     |

### Servers

{width="wide"}
| Variable name         | Description                              |
|-----------------------|------------------------------------------|
| host                  |Hostname of local host (alias: #H)        |
| host_short            |Hostname of local host (no domain name)   |
|                       |(alias: #h)                               |
| socket_path           |Server socket path                        |
| start_time            |Server start time                         |
| pid                   |Server PID                                |
