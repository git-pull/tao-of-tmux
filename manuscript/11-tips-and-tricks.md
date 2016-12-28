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
Commands](https://en.wikipedia.org/wiki/Run_commands)) for your shell. Depending
on your shell (you can use `$ echo $SHELL` to find it on most shells), you will
want to keep this in `~/.bashrc` or `~/.zshrc`:

{language=shell, line-numbers=off}
    export PAGER="most"

In my configurations, I often reuse configs and some machines may not have
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
programmers and system administrators.

You could also bring in a tool like [multitail](https://vanheusden.com/multitail/).
You'd be in for an [*Inception*](http://www.imdb.com/title/tt1375666/) moment,
because you'd be using a log multiplexer in a terminal multiplexer.

## File watching

In my never ending conquest to get software projects working in symphony with
code changes, I've come to taste test many file watching applications and
patterns to get 'instant feedback' upon file changes, I've become the
internet's unofficial connoisseur on them.

What this kind of application does is wait for a file to be updated, then
executes a custom command, like restarting a server, rebuilding an application,
running tests, linters and so on. It gives you as a developer instant feedback
in the terminal and is one of those things that can really trick out a tmux
workspace into an IDE-like environment.

I eventually settled on [`entr(1)`](http://entrproject.org/), which works
superbly across Linux distros, BSD's and OS X / MacOS.

The trick to make entr work is to [pipe](https://en.wikipedia.org/wiki/Pipeline_(Unix))
a list of files into it to watch.

Let's search for all [`.go`](https://en.wikipedia.org/wiki/Go_(programming_language))
files in a directory and [run tests](https://golang.org/cmd/go/#hdr-Test_packages)
on file change:

{language=shell, line-numbers=off}
    $ ls -d *.go | entr -c go test ./...

Sometimes we may want to watch files recursively, and we need to do that in a
cross-platform way. We can't depend on `**` existing to grab files recursively.
So something more POSIX friendly would be `find . -print | grep -i '.*[.]go'`:

{language=shell, line-numbers=off}
    $ find . -print | grep -i '.*[.]go' | entr -c go test ./...

Only run file watcher if entr is installed, let's wrap in a conditional
[`command -v`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/command.html)
test:

{language=shell, line-numbers=off}
    $ if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; fi

And have it fallback to `go test` in the event `entr` isn't installed (you'll
thank me when you end up scripting this command in a [session manager](#session-manager):

{language=shell, line-numbers=off}
    $ if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; else go test ./...; fi

Show a notice message to user to install entr if not installed ons system:

{language=shell, line-numbers=off}
    $ if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; else go test ./...; echo "\nInstall entr(1) to automatically rebuild documentation when files change. \nSee http://entrproject.org/"; fi

Here's why you want patterns like that, you can put it into a [`Makefile`](https://en.wikipedia.org/wiki/Makefile)
and commit it to your project's [VCS](https://en.wikipedia.org/wiki/Version_control)
so you and other developers can have access to this reusable command across
different UNIX-like systems, with and without that certain program installed.

Note: You may have to convert the indentation within the `Makefile`s from spaces to tabs.

So let's go ahead see what a `Makefile` with this looks like:

{language=makefile, line-numbers=off}
    watch_test:
        if command -v entr > /dev/null; then find . -print | grep -i '.*[.]go' | entr -c go test ./...; else go test ./...; echo "\nInstall entr(1) to automatically rebuild documentation when files change. \nSee http://entrproject.org/"; fi

To run this, do `$ make watch_test` in the same directory as the `Makefile`.

But that was a tad bloated and hard to read. We have a couple tricks at our
disposal. One would be to add continuation to the next line with a trailing
backlash (`\`):

{language=makefile, line-numbers=off}
    watch_test:
        if command -v entr > /dev/null; then find . -print | \
        grep -i '.*[.]go' | entr -c go test ./...; \
        else go test ./...; \
        echo "\nInstall entr(1) to automatically rebuild documentation when files change. \nSee http://entrproject.org/"; fi

Another would be to break the command up into variables and `make` subcommands.
So let's try that:

{language=makefile, line-numbers=off}
    WATCH_FILES= find . -type f -not -path '*/\.*' | \
    grep -i '.*[.]go$$' 2> /dev/null

    test:
            go test $(test) ./...

    entr_warn:
            @echo "----------------------------------------------------------"
            @echo "     ! File watching functionality non-operational !      "
            @echo "                                                          "
            @echo "Install entr(1) to automatically run tasks on file change."
            @echo "See http://entrproject.org/                               "
            @echo "----------------------------------------------------------"

    watch_test:
            if command -v entr > /dev/null; then ${WATCH_FILES} | \
            entr -c $(MAKE) test; else $(MAKE) test entr_warn; fi

`$(MAKE)` is helpful for portability because those are recursive command calls
back into `make`. On BSD systems, I may try invoking `make` via `gmake` (to call
[GNU Make](https://www.gnu.org/software/make/) specifically). This ended
up happening to me personally building PDF's for the book [AlgoXY](https://github.com/liuxinyu95/AlgoXY/).
I've since [wrote a patch](https://github.com/liuxinyu95/AlgoXY/pull/16) to
property use `$(MAKE)` for recursive calls.

The `$(test)` after `go test` allows passing in a shell variable with arguments
in it. So you could do `make watch_test test='-i'`. For examples of a similar
`Makefile` in action see [the one in my tmuxp project](https://github.com/tony/tmuxp/blob/master/Makefile).
The project is licensed BSD (permissive), so you can grab code and use it
in compliant with the [LICENSE](https://github.com/tony/tmuxp/blob/master/LICENSE).

One more thing, let's say you're running a server like
[Gin](https://github.com/gin-gonic/gin), [Iris](https://github.com/kataras/iris)
or [Echo](https://github.com/labstack/echo). `entr -c` likely won't be
restarting the server for you. Try entering the `-r` flag to send a
[`SIGTERM`](https://en.wikipedia.org/wiki/Unix_signal) to the process before
restarting it. Combining the current `-c` flag with the new `-r` will give you
`entr -rc`:

{language=makefile, line-numbers=off}
    run:
            go run main.go

    watch_run:
            if command -v entr > /dev/null; then ${WATCH_FILES} | \
            entr -c $(MAKE) run; else $(MAKE) run entr_warn; fi

## Session Managers {#session-manager}

For those who use tmux regularly to perform repetitive tasks, such as opening
the same software project, view the same logs, etc. there are applications that
store your layouts declaratively in a YAML or JSON file and help you boot up
your session fast.

[Teamocil](https://github.com/remiprev/teamocil) and
[Tmuxinator](https://github.com/tmuxinator/tmuxinator) are the first ones I
tried. By far the most popular one is tmuxinator. They are both programmed in
Ruby. There is also [tmuxomatic](https://github.com/oxidane/tmuxomatic), which
allows you to "draw" your tmux sessions in text and have tmuxomatic build the
layout.

I sort of have a home team advantage here, as I'm author of [tmuxp](https://github.com/tony/tmuxp).
I written it already having used teamocil and tmuxinator but with many more
features. For one, it builds on top of [libtmux](https://github.com/tony/libtmux),
a library which abstracts tmux [server](#server), [sessions](#sessions),
[windows](#windows) and [panes](#panes) to actively build the state of tmux
sessions. In addition it has a naive form of session freezing, support for JSON,
more flexible configuration options, and it will even offer to attach sessions
that already exist instead of redundantly running script commands against the
session if it already is running.

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
                 # to point to your python bin folder. More help below.
    $ tmuxp load ~/.tmuxp/test.yaml

### Troubleshooting `tmuxp: command not found`

This is due to your site package bin path (where application entry points are
installed to) not being in your paths. To find your user site packages base directory:

{language=shell, line-numbers=off}
    `$ python -m site --user-base`

This will get you something like `/Users/me/Library/Python/2.7` on MacOS with
Python 2.7 or `/home/me/.local` on Linux/BSD boxes.

The applications are in the `bin/` folder insite that. So you need to
concatenate the two and add them to your [`PATH`](https://en.wikipedia.org/wiki/PATH_(variable)).
Try adding one of these in your `~/.bashrc` or `~/.zshrc`:

{language=shell, line-numbers=off}
    export PATH=/Users/me/Library/Python/2.7/bin:$PATH     # MacOS w/ python 2.7
    export PATH=$HOME/.local/bin:$PATH                     # Linux/BSD
    export PATH="`python -m site --user-base`/bin":$PATH   # May work all-around

Then open a new terminal, or `. ~/.zshrc` / `. ~/.bashrc` in your current one.
Then you can run `tmuxp -V` and `tmuxp load` commands.

## tmux-plugins and tpm

[tmux-plugins](https://github.com/tmux-plugins) and [tmux package
manager](https://github.com/tmux-plugins/tpm) are a suite of tools dedicated
toward enhancing the experience of tmux users.

- [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect): Persists
  tmux environment across system restarts.
- [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum): Continuous
  saving of tmux environment. Automatic restore when tmux is started. Automatic
  tmux start when computer is turned on.
- [tmux-yank](https://github.com/tmux-plugins/tmux-yank): Tmux plugin for
  copying to system clipboard. Works on OSX, Linux and Cygwin.
- [tmux-battery](https://github.com/tmux-plugins/tmux-battery): Plug and play
  battery percentage and icon indicator for Tmux.
