# Configuration {#config}

Configuration of tmux managed through `.tmux.conf` in your `$HOME` directory. 
The paths `~/.tmux.conf` and `$HOME/.tmux.conf` should work on OS X, Linux and
BSD.

For a sample config, I maintain a pretty decked out one at
<https://github.com/tony/tmux-config>.

I> **Custom Configs**
I>
I> You can specify your config via the `-f` command. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf
I>
I> Note that if a tmux server is already running in the background and you want 
I> to test a fresh config, you must either shut down the rest of the
I> tmux sessions or use a different socket name. Like this:
I> 
I> {language=shell, line-numbers=off}
I>     $ tmux -f path/to/config.conf -Ltesting_tmux
I>
I> And you can treat everything like normal, just keep passing `-Ltesting_tmux`
I> (or whatever socket name you feel like testing configs with) for reuse.
I>
I> {language=shell, line-numbers=off}
I>     $ tmux -Ltesting_tmux attach

## Updating configs in current sessions

You can apply config files in live tmux sessions. Compare this to `source` or
["dot"](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#dot)
in the POSIX standard.

`prefix` + `:` will open up the tmux prompt, then type:

`:source /path/to/config.conf`

And hit return.

`$ tmux source-file /path/to/config.conf` can also achieve the same result via
command line.

I> **Easy reloadin'**
I>
I> Even better, often you will keep your default tmux config stored in
I> `$HOME/.tmux.conf`. So what can you do? You can `bind-key` to
I> `source-file ~/.tmux.conf`:
I>
I> `bind r source ~/.tmux.conf`
I> 
I> You can also have it give you a confirmation afterwards:
I> 
I> `bind r source ~/.tmux.conf\; display "~/.tmux.conf sourced!"`
I>
I> Now you can type `prefix` + `r` to get the config to reload.
