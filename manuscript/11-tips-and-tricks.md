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

So to get this working, you need to set your `PAGER` [environmental variable](https://en.wikipedia.org/wiki/Environment_variable)
to point to the MOST binary. You can test is like this:

{language=shell, line-numbers=off}
    $ export PAGER=more man ls

If you found that you like `most`, you will probably want it to be the manual
page filter for anything you look up. You will want to add it to the "rc" ([Run
Commands](https://en.wikipedia.org/wiki/Run_commands) for your shell. Depending
on your shell (you can use `$ echo $SHELL` to find it on most shells, you will
want to keep this in `~/.bashrc` or `~/.zshrc`:

{language=shell, line-numbers=off}
    export PAGER="most"

In my configuratiosn, I often reuse configs and some machines may not have
`most` installed, so I will have my scripting only set `PAGER` if `most` is
found:

{language=shell, line-numbers=off}
    #!/bin/sh

    if command -v most > /dev/null 2>&1; then
        export PAGER="most"
    fi

## Log tailing

Not tmux specific, but powerful when used in tandem with it. You can run a
follow (`-f`) using [`tail(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/tail.html).
More modern versions of tail have the `-F` (capitalized) which checks for file
renames and rotation. 

On OS X, you can do:

{language=shell, line-numbers=off}
    $ tail -F /var/log/system.log

and keep that open in a pane. It's kind of like a Facebook newsfeed, except for
programmers and system adminstrators.

## File watching

In my never ending conquest for file watchers, I've become the unofficial
taste-tester of them.

What this kind of application does is wait for a file to be updated, then
executes a custom command, like restarting a server, rebuilding an application,
running tests, linters and so on. It gives you as a developer instant feedback
in the terminal and is one of those things that can really trick out a tmux
workspace into an IDE-like environment.

I eventually settled toward [`entr(1)`](http://entrproject.org/), which
works superbly across Linux distros, BSD's and OS X / MacOS.

The trick to make entr work is to [pipe](https://en.wikipedia.org/wiki/Pipeline_(Unix))
a list of files into it to watch.

Let's search for all go files in a directory and run tests on file change:

{language=shell, line-numbers=off}
    $ ls -d *.go | entr -c go test ./...

Sometimes we may want to see recursive files, and we need to do that in a
cross-platform way. We can't depend on `**` existing to grab files recursively.
So something more POSIX friendly would be `find . -print | grep -i '.*[.]go'`:

{language=shell, line-numbers=off}
    $ find . -print | grep -i '.*[.]go' | entr -c go test ./...

Only run file watcher if entr is installed, let's wrap in a conditional
[`command -v`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/command.html)
test:

{language=shell, line-numbers=off}
    $ if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; else go test ./...; fi

Show a notice message to user to install entr if not installed ons system:

{language=shell, line-numbers=off}
    $ if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; else go test ./...; echo "\nInstall entr(1) to automatically rebuild documentation when files change. \nSee http://entrproject.org/"; fi

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

So in tmuxp, we'll hollow out a tmuxp config directory with `$ mkdir ~/.tmuxp`
then create a YAML file at `~/.tmuxp/test.yaml`:

{language=yaml, line-numbers=off}
    session_name: 4-pane-split
    windows:
    - window_name: dev window
      layout: tiled
      shell_command_before:
        - cd ~/                    # run as a first command in all panes
      panes:
        - shell_command:           # pane no. 1
            - cd /var/log          # run multiple commands in this pane
            - ls -al | grep \.log
        - echo second pane         # pane no. 2
        - echo third pane          # pane no. 3
        - echo forth pane          # pane no. 4

gives a session titled *4-pane-split*, with one window titled *dev window* that
has 4 panes in it. 3 of them are in the home directory, the other is in
`/var/log` and is listed all files ending with `.log`.

To launch it, install tmuxp and load the configuration:

{language=shell, line-numbers=off}
    $ pip install --user tmuxp
    $ tmuxp -V   # verify tmuxp is installed, if not you to fix your `PATH`
    $ tmuxp load ~/.tmuxp/test.yaml
