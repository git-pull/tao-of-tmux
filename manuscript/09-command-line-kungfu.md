# Command Line Kung fu {#cli-kung-fu}

The command line in tmux is one of those areas often uncharted.

## Shorthands

tmux commands and arguments may all be accessed via [`fnmatch(3)`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fnmatch.html)
patterns.

For instance, you don't need to type `$ tmux attach` every time. `$ tmux attac`,
`$ tmux att`, `$ tmux at` and `$ tmux a` work just as well.

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

So sessions are represented by dollar signs ($), because those are where you keep
your projects (*ostensibly* where you make money, or help someone else do it).

Windows are represented by the [at sign](https://en.wikipedia.org/wiki/At_sign)
(@). So windows are kind of like referencing / messaging a user on a social
networking website.

Panes are the fun one, represented by the percent sign (%). Just like the
default prompt for [csh](https://en.wikipedia.org/wiki/C_shell) and
[tcsh](https://en.wikipedia.org/wiki/Tcsh). Hey, makes sense, since panes are
your pseudoterminals.

To give you an idea of the possibilities of where you can use targets, here are
the commands with you can use targets:

- `$ tmux attach-session [-t target-session]`
- `$ tmux detach-client [-s target-session] [-t target-client]`
- `$ tmux has-session [-t target-session]`
- `$ tmux kill-session [-t target-session]`
- `$ tmux list-clients [-t target-session]`
- `$ tmux lock-client [-t target-client]`
- `$ tmux lock-session [-t target-session]`
- `$ tmux new-session [-t target-session]`
- `$ tmux refresh-client [-t target-client]`
- `$ tmux rename-session [-t target-session]`
- `$ tmux show-messages [-t target-client]`
- `$ tmux suspend-client [-t target-client]`
- `$ tmux switch-client [-c target-client] [-t target-session]`

## Formats {#formats}

tmux provides a minimal template language and set of variables you can use to
access information about your tmux environment.

Formats are often specified via `-F` flag.

You know how template engines such as
[mustache](https://mustache.github.io/), [handlebars](http://handlebarsjs.com/)
[ERB](http://ruby-doc.org/stdlib-2.3.3/libdoc/erb/rdoc/ERB.html) in ruby,
[jinja2](http://jinja.pocoo.org/docs/dev/) in python,
[twig](http://twig.sensiolabs.org/) in PHP and
[JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) in Java allow template
variables? Formats are a similar concept.

The amount of `FORMATS` (variables) made available by tmux has expanded greatly
since version 1.8. As of tmux 2.3, the available formats are:

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| alternate_on          |        |If pane is in alternate screen            |
| alternate_saved_x     |        |Saved cursor X in alternate screen        |
| alternate_saved_y     |        |Saved cursor Y in alternate screen        |
| buffer_name           |        |Name of buffer                            |
| buffer_sample         |        |Sample of start of buffer                 |
| buffer_size           |        |Size of the specified buffer in bytes     |

### Client

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| client_activity       |        |Integer time client last had activity     |
| client_created        |        |Integer time client created               |
| client_control_mode   |        |1 if client is in control mode            |
| client_height         |        |Height of client                          |
| client_key_table      |        |Current key table                         |
| client_last_session   |        |Name of the client's last session         |
| client_pid            |        |PID of client process                     |
| client_prefix         |        |1 if prefix key has been pressed          |
| client_readonly       |        |1 if client is readonly                   |
| client_session        |        |Name of the client's session              |
| client_termname       |        |Terminal name of client                   |
| client_tty            |        |Pseudo terminal of client                 |
| client_utf8           |        |1 if client supports utf8                 |
| client_width          |        |Width of client                           |
| command_hooked        |        |Name of command hooked, if any            |
| command_name          |        |Name of command in use, if any            |
| command_list_name     |        |Command name if listing commands          |
| command_list_alias    |        |Command alias if listing commands         |
| command_list_usage    |        |Command usage if listing commands         |
| history_bytes         |        |Number of bytes in window history         |
| history_limit         |        |Maximum window history lines              |
| history_size          |        |Size of history in bytes                  |
| host                  |#H      |Hostname of local host                    |
| host_short            |#h      |Hostname of local host (no domain name)   |
| line                  |        |Line number in the list                   |

### Pane

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| cursor_flag           |        |Pane cursor flag                          |
| cursor_x              |        |Cursor X position in pane                 |
| cursor_y              |        |Cursor Y position in pane                 |
| insert_flag           |        |Pane insert flag                          |
| keypad_cursor_flag    |        |Pane keypad cursor flag                   |
| keypad_flag           |        |Pane keypad flag                          |
| mouse_any_flag        |        |Pane mouse any flag                       |
| mouse_button_flag     |        |Pane mouse button flag                    |
| mouse_standard_flag   |        |Pane mouse standard flag                  |
| pane_active           |        |1 if active pane                          |
| pane_bottom           |        |Bottom of pane                            |
| pane_current_command  |        |Current command if available              |
| pane_current_path     |        |Current path if available                 |
| pane_dead             |        |1 if pane is dead                         |
| pane_dead_status      |        |Exit status of process in dead pane       |
| pane_height           |        |Height of pane                            |
| pane_id               |#D      |Unique pane ID                            |
| pane_in_mode          |        |If pane is in a mode                      |
| pane_input_off        |        |If input to pane is disabled              |
| pane_index            |#P      |Index of pane                             |
| pane_left             |        |Left of pane                              |
| pane_pid              |        |PID of first process in pane              |
| pane_right            |        |Right of pane                             |
| pane_start_command    |        |Command pane started with                 |
| pane_synchronized     |        |If pane is synchronized                   |
| pane_tabs             |        |Pane tab positions                        |
| pane_title            |#T      |Title of pane                             |
| pane_top              |        |Top of pane                               |
| pane_tty              |        |Pseudo terminal of pane                   |
| pane_width            |        |Width of pane                             |
| scroll_region_lower   |        |Bottom of scroll region in pane           |
| scroll_region_upper   |        |Top of scroll region in pane              |
| scroll_position       |        |Scroll position in copy mode              |
| wrap_flag             |        |Pane wrap flag                            |

### Session

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| session_alerts        |        |List of window indexes with alerts        |
| session_attached      |        |Number of clients session is attached to  |
| session_activity      |        |Integer time of session last activity     |
| session_created       |        |Integer time session created              |
| session_last_attached |        |Integer time session last attached        |
| session_group         |        |Number of session group                   |
| session_grouped       |        |1 if session in a group                   |
| session_height        |        |Height of session                         |
| session_id            |        |Unique session ID                         |
| session_many_attached |        |1 if multiple clients attached            |
| session_name          |#S      |Name of session                           |
| session_width         |        |Width of session                          |
| session_windows       |        |Number of windows in session              |

### Window

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| window_activity       |        |Integer time of window last activity      |
| window_activity_flag  |        |1 if window has activity                  |
| window_active         |        |1 if window active                        |
| window_bell_flag      |        |1 if window has bell                      |
| window_find_matches   |        |Matched data from the find-window         |
| window_flags          |#F      |Window flags                              |
| window_height         |        |Height of window                          |
| window_id             |        |Unique window ID                          |
| window_index          |#I      |Index of window                           |
| window_last_flag      |        |1 if window is the last used              |
| window_layout         |        |Window layout description, ignoring zoomed|
|                       |        |window panes                              |
| window_linked         |        |1 if window is linked across sessions     |
| window_name           |#W      |Name of window                            |
| window_panes          |        |Number of panes in window                 |
| window_silence_flag   |        |1 if window has silence alert             |
| window_visible_layout |        |Window layout description, respecting     |
|                       |        |zoomed window panes                       |
| window_width          |        |Width of window                           |
| window_zoomed_flag    |        |1 if window is zoomed                     |


### Server

| Variable name         | Alias  | Description                              |
|-----------------------|--------|------------------------------------------|
| socket_path           |        |Server socket path                        |
| start_time            |        |Server start time                         |
| pid                   |        |Server PID                                |

