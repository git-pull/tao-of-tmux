# Configuration {#config}

Configuration of tmux is typically done through the `.tmux.conf` file in your
`$HOME` directory.  To those who are uninitiated with the shorthand of how to
pull their home directory up, the paths `~/.tmux.conf` and `$HOME/.tmux.conf`
should work on OS X, Linux and BSD.

I> **Custom Configs**
I>
I> You can specify your config via the `-f` command. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf
I>
I> Note that if a tmux server is already running in the background, you may not
I> and you want to test a fresh config, you should shut down the rest of the
I> tmux sessions or use a different socket name. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf -Ltesting_tmux
I>
I> And you can treat everything like normal, just keep passing `-Ltesting_tmux`
I> (or whatever socket name you feel like) for reuse.
I>
I> {language=shell, line-numbers=off}
I>     $ tmux -Ltesting_tmux attach
