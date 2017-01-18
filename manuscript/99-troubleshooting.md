# Troubleshooting {#appendix-troubleshooting}

## `E353: Nothing in register *` when pasting on vim

If you are using macOS / OS X with vim inside tmux, you may get the error
`E353: Nothing in register *` when trying to paste.

Try installing [`reattach-to-user-namespace`](https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard)
via [brew](http://brew.sh).

{language=shell, line-numbers=off}
    $ brew install reattach-to-user-namespace

## `tmuxp: command not found` and `powerline: command not found` {#troubleshoot-site-paths}

This is due to your site package bin path (where application entry points are
installed to) not being in your paths. To find your user site packages base directory:

{language=shell, line-numbers=off}
    $ python -m site --user-base

This will get you something like `/Users/me/Library/Python/2.7` on macOS with
Python 2.7 or `/home/me/.local` on Linux/BSD boxes.

The applications are in the `bin/` folder inside that. So you need to
concatenate the two and add them to your [`PATH`](https://en.wikipedia.org/wiki/PATH_(variable)).
Try adding one of these in your `~/.bashrc` or `~/.zshrc`:

{language=shell, line-numbers=off}
    export PATH=/Users/me/Library/Python/2.7/bin:$PATH     # macOS w/ python 2.7
    export PATH=$HOME/.local/bin:$PATH                     # Linux/BSD
    export PATH="`python -m site --user-base`/bin":$PATH   # May work all-around

Then open a new terminal, or `. ~/.zshrc` / `. ~/.bashrc` in your current one.
Then you can run `$ tmuxp -V`, `$ tmuxp load` and `$ powerline tmux right`
commands.
