# Configuration {#config}

Most tmux users break away from the defaults by creating their own customized
configurations. These configurations vary from the trivial, such as adding
keybindings, and adjusting the prefix key, to complex things, such as decking
out the [status bar](#status-bar) with system stats and fancy glyphs via
powerlines.

Configuration of tmux is managed through `.tmux.conf` in your `$HOME` directory. 
The paths `~/.tmux.conf` and `$HOME/.tmux.conf` should work on OS X, Linux, and
BSD.

Configuration is done via the file being run upon initially starting tmux, when
the server is started. tmux is configured using the same commands as tmux does via
shell. For instance, `$ tmux set-window-option -g automatic-rename` in a shell
is the same as `set-window-option -g automatic-rename` in your config.

Configuration can be updated later via `source-file`, which is discussed in
this chapter.

For a sample config, I maintain a pretty decked out one at
<https://github.com/tony/tmux-config>. It's permissively licensed, and you're
free to copy and paste from it as you wish.

I> **Custom Configs**
I>
I> You can specify your config via the `-f` command. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf
I>
I> Note: If a tmux server is running in the background and you want 
I> to test a fresh config, you must either shut down the rest of the
I> tmux sessions or use a different socket name. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf -Ltesting_tmux
I>
I> And you can treat everything like normal; just keep passing `-Ltesting_tmux`
I> (or whatever socket name you feel like testing configs with) for reuse.
I>
I> {language=shell, line-numbers=off}
I>     $ tmux -Ltesting_tmux attach

## Reloading configuration {#reload-config}

You can apply config files in live tmux sessions. Compare this to `source` or
["dot"](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#dot)
in the POSIX standard.

`Prefix` + `:` will open the tmux prompt, then type:

`:source /path/to/config.conf`

And hit return.

`$ tmux source-file /path/to/config.conf` can also achieve the same result via
command line.

I> **Easy reloadin'**
I>
I> Even better, often, you will keep your default tmux config stored in
I> `$HOME/.tmux.conf`. So, what can you do? You can `bind-key` to
I> `source-file ~/.tmux.conf`:
I>
I> `bind r source ~/.tmux.conf`
I> 
I> You can also have it give you a confirmation afterwards:
I> 
I> `bind r source ~/.tmux.conf\; display "~/.tmux.conf sourced!"`
I>
I> Now, you can type `Prefix` + `r` to get the config to reload.

## How configs work

The tmux configuration is processed just like [run commands](https://en.wikipedia.org/wiki/Run_commands)
in a `~/.zshrc` or `~/.bashrc` file. `bind r source ~/.tmux.conf` in the tmux
configuration is the same as `$ tmux bind r source ~/.tmux.conf`.

You could always create a shell script prefixing `tmux` in front of commands
and run it on fresh servers. The result is the same. Same goes if you manually
type in `$ tmux set-option` and `$ tmux bind-key` commands into any terminal (in
or outside tmux).

This in `.tmux.conf`:

{language=shell, line-numbers=off}
    bind-key a send-prefix

Is the same as having no `.tmux.conf` (or `$ tmux -f/dev/null`) and typing:

{language=shell, line-numbers=off}
    $ tmux bind-key a send-prefix

in a newly started tmux server.

The important thing to internalize is that a tmux configuration consists of
setting server options (`set-option -s`), global session (`set-option -g`), and
window options (`set-window-option -g`).

The rest of this chapter is going to proceed cookbook-style. You can pick out
these tweaks and add them to your `.tmux.conf` and [reload](#reload-config).

## Server options

Server options are set with `set-option -s option value`.

### Tweak timing between key sequences

{line-numbers=off}
    set -s escape-time 0

### Terminal coloring

If you're having an issue with color detail in tmux, it may help to set
`default-terminal` to `screen-256color`.

{line-numbers=off}
    set -g default-terminal "screen-256color"

This sets the `TERM` variable in new panes.

## Session options

Aside from the [status bar](#status-bar), covered in the next chapter, most
user configuration will be custom keybindings. This section covers the few
generic options, and the next section goes into snippets involving keybindings.

### Base index

Set the starting number (base index) for windows:

{line-numbers=off}
    set -g base-index 1

Setting `base-index` assures newly created windows start at 1 and count upwards.

## Window options

Window options are set via `set-option -w` or `set-window-option`. They are the
same thing.

### Automatic window naming

Windows can be automatically renamed via setting `automatic-rename`:

{line-numbers=off}
    set-window-option -g automatic-rename

## Keybindings

### Prefix key

The default [prefix key](#prefix-key) in tmux is `<Ctrl-b>`. You can customize
it by setting a new prefix and unsetting the default. To set the prefix to
`<Ctrl-a>`, like GNU Screen, try this:

{line-numbers=off}
    set-option -g prefix C-a
    unbind-key C-b
    bind-key a send-prefix

### New window w/ prompt

Prompt for window name upon creating a new window, `Prefix` + `C` (capital C):

{line-numbers=off}
    bind-key C command-prompt -p "Name of new window: " "new-window -n '%%'"

### Vi copy-paste keys

This is comprised of two-parts: Setting the `mode-keys` window option to vi and
setting the `vi-copy` bindings to use `v` to begin selection and `y` to yank.

{line-numbers=off}
    # Vi copypaste mode
    set-window-option -g mode-keys vi
    bind-key -t vi-copy 'v' begin-selection
    bind-key -t vi-copy 'y' copy-selection

### hjkl / vi-like pane traversal

Another one for vi fans, this keeps your right hand on the home row when moving
directionally across panes in a window.

{line-numbers=off}
    bind h select-pane -L
    bind j select-pane -D
    bind k select-pane -U
    bind l select-pane -R

### Further inspiration

For more ideas, I have a `.tmux.conf` you can copy-paste from on the internet at
<https://github.com/tony/tmux-config/blob/master/.tmux.conf>.

In the next chapter, we will go into configuring the [status line](#status-bar).
