# Troubleshooting {#appendix-troubleshooting}

## `E353: Nothing in register *` when pasting on vim

If you are using macOS / OS X with vim inside tmux, you may get the error
`E353: Nothing in register *` when trying to paste.

Try installing [`reattach-to-user-namespace`](https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard)
via [brew](http://brew.sh).

{language=shell, line-numbers=off}
    $ brew install reattach-to-user-namespace
