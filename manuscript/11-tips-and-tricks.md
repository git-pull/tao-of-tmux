# Tips and Tricks {#tips-and-tricks}

## Read the tmux manual in style

`$ man tmux` is the command to load up the "[man page](https://en.wikipedia.org/wiki/Man_page)" for tmux. You can do the same to find instructions for just about any comment, here's a couple of fun ones:

{language=shell, line-numbers=off}
    $ man less
    $ man man

[most(1)](http://www.jedsoft.org/most/) is a solid
[`PAGER`](http://pubs.opengroup.org/onlinepubs/9699919799//utilities/man.html)
that drastically improves readability of manual pages by acting as a syntax
highlighter for manual pages.

![left: man, version 1.6c on MacOS Sierra. right: MOST v5.0.0](images/11-recipes/most.png)

## Session Managers

For those who use tmux regularly to perform repetitive tasks, such as open the
same software project, view the same logs, etc. there are applications that
store your layouts declaratively in a YAML or JSON file and help you boot up
your session fast.

[Teamocil](https://github.com/remiprev/teamocil) and
[Tmuxinator](https://github.com/tmuxinator/tmuxinator) are the first ones I
tried. By far the most popular one is tmuxinator. They are both programmed in
Ruby. There is also [tmuxomatic](https://github.com/oxidane/tmuxomatic), which
allows you to "draw" your tmux sessions in text and have tmuxomatic build the
layout.

Of course, I sort of have hometeam advantage here, [tmuxp](https://github.com/tony/tmuxp)
is better. I written it already having used teamocil and tmuxinator but with
many more features. For one, it builds on top of
[libtmux](https://github.com/tony/libtmux), a library which abstracts tmux
[server](#server), [sessions](#sessions), [windows](#windows) and
[panes](#panes) to actively build the state of tmux sessions. In addition it
has a naive form of session freezing, support for JSON, more flexible
configuration options, and it will even offer to attach sessions that already
exist instead of redundantly running script commands against the session if it
already is running.
