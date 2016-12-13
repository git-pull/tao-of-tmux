# Configuration {#config}

Configuration of tmux is typically done through the `.tmux.conf` file in your
`$HOME` directory.  To those who are uninitiated with the shorthand of how to
pull their home directory up, the paths `~/.tmux.conf` and `$HOME/.tmux.conf`
should work on OS X, Linux and BSD.

You can specify your config via the `-f` command. Like this:

{language=shell, line-numbers=off}
    $ tmux -f path/to/config.conf
