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

Matching targets will fail if a pattern matches more than one item. If 2
sessions existed, named `mysession` and `mysession2`, the above command would
fail. To target either session, the complete target name must be specified.

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

When scripting tmux, the symbols help denote the type of object, but also serve
as a way to target something deeply, like the pane, *directly*, without needing
to know or specify the window or its session.

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
output occurs in this version of tmux, it's undefined behavior, it's advised to
keep use of `-F` scoped to the objects being listing, when scripting, to avoid
breakage. For instance, if you want the active pane, use `#{pane_active}` via
`$ tmux list-panes -F "#{pane_active}"`.

By default, `list-panes` will only show panes in a window. Unless you specificy
`-a` to output all on a server, or `-s [-t session-name]` for all panes in a
session:

{language=shell, line-numbers=off}
    $ tmux list-panes -s -t mysession
    > 1.0: [176x29] [history 87/2000, 21033 bytes] %0
      1.1: [87x6] [history 1814/2000, 408479 bytes] %1 (active)
      1.2: [88x6] [history 1916/2000, 464932 bytes] %2
      2.0: [176x24] [history 9/2000, 2262 bytes] %13
      2.1: [55x11] [history 55/2000, 7395 bytes] %14

And the `-t` flag lists all panes in a window:

{language=shell, line-numbers=off}
    $ tmux list-panes -t @0
    > 0: [176x29] [history 87/2000, 21033 bytes] %0
      1: [176x36] [history 1790/2000, 407807 bytes] %1 (active)
      2: [88x6] [history 1916/2000, 464932 bytes] %2

Same concept applies to `list-windows`. By default, The `-a` flag will list all
windows on a server, `-t` lists windows within a session, omitting `-t` will
only list windows within the current session inside tmux.

{language=shell, line-numbers=off}
    $ tmux list-windows
    > 1: zsh* (3 panes) [176x36] [layout f9a4,176x36,0,0[176x29,0,0,0,176x6,0,30{87x6,0,30,1,88x6,88,30,2}]] @0 (active)
      2: zsh- (5 panes) [176x36] [layout 55ef,176x36,0,0[176x24,0,0,13,176x11,0,25{55x11,0,25,14,58x11,56,25[58x7,56,25,16,58x3,56,33,17],61x11,115,25,15}]] @6

## Controlling tmux

tmux allows sending keys, including Ctrl via `C-`, `^` and alt (meta) via `M-`,
as well as special key names, from the tmux manual:

> Up, Down, Left, Right, BSpace, BTab, DC (Delete), End, Enter, Escape, F1 to
> F12, Home, IC (Insert), NPage/PageDown/PgDn, PPage/PageUp/PgUp, Space,
> and Tab.

If special keys are not matched, the defined behavior is to send it as a string
to the pane, character by character.

For this example, we will use `send-keys` through tmux prompt, because omitting
target (`-t`) will direct the command to the current pane, but the keys sent will 
sometimes print before the prompt.

Open tmux command prompt via `Prefix` + `:` and type this after the `:`:

`send-keys echo 'hi'`

Hit enter. This just inserted *hi* into the current active pane. You can also
use targets to specific which pane to send it to. 

Let's now try to send keys to a another pane in our current window. Create a
second pane via splitting the window if one doesn't exist. You can also do this
exercise outside of tmux or inside a scripting file and running it.

Grab a pane ID from the output of `list-panes`:

{language=shell, line-numbers=off}
    $ tmux list-panes
    > 0: [180x57] [history 87/2000, 21033 bytes] %0
      1: [89x14] [history 1884/2000, 509864 bytes] %1 (active)
      2: [90x14] [history 1853/2000, 465297 bytes] %2

`%2` looks good. Replace `%2` with the pane you want to target. This sends `cal`
to the input:

{language=shell, line-numbers=off}
    $ tmux send-keys -t %2 'cal'

Nice, let's cancel that out by sending a [SIGINT](https://en.wikipedia.org/wiki/Unix_signal#SIGINT):

{language=shell, line-numbers=off}
    $ tmux send-keys -t %2 'C-c'

This cancelled the command and brought up a fresh input. This time let's send
an Enter keypress to run `cal(1)`.

{language=shell, line-numbers=off}
    $ tmux send-keys -t %2 'cal' 'Enter'

This outputs in the adjacent pane.

![Top-left: Listing panes, Bottom-left: Sending keys to right pane, Right:
Output of cal(1).](images/10-scripting/send-keys-cal.png)

## Capturing pane content {#capture-pane}

`$ tmux capture-pane` will copy a panes' contents.

By default, the contents will be saved to tmux' internal clipboard; the *paste
buffer*. You can run `capture-pane` within any pane, then navigate to an
editor, paste the contents (don't forget to `:set paste` and go into insert mode
with `i` on vim) and save it to a file. To [paste](#clipbpard), use `Prefix` +
`]` inside the pane you're pasting into.

You can also add the `-p` flag to print it to [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29).
From there you could use [redirection](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_07)
to place the output into a file. Let's do `>>` so we don't accidentically
truncate a file:

{language=shell, line-numbers=off}
    $ tmux capture-pane -p >> ./test

As an alternative to redirection, you can also use `save-buffer`. The `-a` flag
will get you the same behavior as appended output direction.

{language=shell, line-numbers=off}
    $ tmux save-buffer -a ./test

To check what's inside:

{language=shell, line-numbers=off}
    $ cat ./test

Like with `send-keys`, [targets](#targets) can be specified with `-t`. Let's
copy a pane into tmux' clipboard ("paste buffer") and paste it into a text
editor in a third pane:

![Top-left: Listing panes, Bottom-left: Capturing pane output of top-left pane,
Right: Pasting buffer into vim.](images/10-scripting/capture-pane-vim.png)

Remember, you can also copy, paste and send-keys to other windows and sessions
also. Targets are server-wide.

## Summary

tmux has a well-devised and intuitive command system enabling the user to access 
bread and butter functionality, quickly. At the same time, tmux provides a
powerful way of retrieving information on its objects between `list-panes`,
`list-windows` and `list-sessions` and formats. This makes tmux not only
accessible, configurable, but also scriptable.

The ability to explicitly and reliably target information down to the point of
tracking a pane by its ID and collecting its pane contents, even sending in
keys. Used by the skilled programmer, opening up the possiblity of orchestrating
the terminals in ways that were previously unrealistic; anything from niche
shell scripts to monitor and react to behavior on systems to high-level,
intelligent and structured control via object oriented libraries, like
[libtmux](https://libtmux.git-pull.com).

In the next chapter, we go delve into optimizations that showcase the latest
generation of unix tools that build upon old, time-tested concepts like [man pages](https://en.wikipedia.org/wiki/Man_page)
and [piping](https://en.wikipedia.org/wiki/Pipeline_(Unix)), while maintaining
portability across differences in platforms and graceful degradation to ensure
development tooling works on machines missing optional tools. In addition, a
class of powerful, high-level applications that leverage tmux' scripting
capabilities to consistenly build tmux workspace via declarative configurations.
