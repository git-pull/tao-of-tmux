# Terminal fundamentals {#terminal-fundamentals}

Before getting into tmux, there are a few fundamentals of the command line to
run over. Often, we're so used to using these out of street smarts and muscle
memory a great deal of us never see the relation of where these tools stand
next to each other.

Seasoned developers are familiar with zsh, bash, iterm2, konsole, /dev/tty,
shell scripting, and so on. If you use tmux, you'll be around these all the
time, regardless of whether you're in a GUI on your local machine or ssh'ing
into a remote server.

If you ever wanted to dive into how processes and TTY's work at the kernel level
(data structures and all) the book *The Design and Implementation of the FreeBSD
Operating System (2nd Edition)* by Marshall Kirk McKusick is nice. In particular,
Chapter 4, *Process Management* and Section 8.6, *Terminal Handling*. [*The TTY
demystified*](http://www.linusakesson.net/programming/tty/index.php) by Linus
Åkesson (available online) dives into the TTY and is a good read as well.

There is also a lot to glean off the history of Unix, 4.2 BSD, etc. It is
interesting and I probably could have a coffee / tea with you discussing it for
hours. You could look at it from multiple perpsectives (The C Language, anything
from the Unix/BSD lineage, etc.) and some clever fellow would likely chime in
mentioning Linux, GNU and so on. It's like *Game of Thrones*, there's multiple
story arcs you can follow, some of which intersect. A few good resources would
be [A Narrative History of BSD](https://www.youtube.com/watch?v=bVSXXeiFLgk)
by Marshall Kirk McKusick (Video), [The UNIX Operating System](https://www.youtube.com/watch?v=tc4ROCJYbm0)
by AT&T (Video), [Early days of Unix and design of sh](https://www.youtube.com/watch?v=FI_bZhV7wpI)
(Video) by Stephen R. Bourne.

## POSIX stuff

Operating systems like MacOS (formerly OS X), Linux and the BSD's all follow
something similar to the POSIX specification in terms of how they square away
various responsibilities and interfaces of the operating system. They're
categorized as ["Mostly POSIX-compliant"](https://en.wikipedia.org/wiki/POSIX#Mostly_POSIX-compliant).

In daily life we often break compatibility with POSIX standards for reasons of
sheer practicality. Operating systems like MacOS will drop you right into Bash.
[`make(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/make.html),
which is also a POSIX standard, is in actuality [GNU Make](https://www.gnu.org/software/make/)
on MacOS by default.  Did you know that as of September 2016 POSIX Make has no
conditionals?

I'm not saying this to take a run at purists, as someone who tries to remain
as compatible as possible in my scripting, it gets very hard to do simple
things after a while. On FreeBSD, the default Make
[(PMake)](https://www.freebsd.org/doc/en_US.ISO8859-1/books/pmake/) uses dots
between conditionals:

    .IF

    .ENDIF

But on most Linux systems and MacOS, GNU Make is the default so they get to do:

    IF

    ENDIF

In addition to that tiny little thing there are hundreds of trivialities that
run across operating systems, their userlands, their binary / library /  include
paths and adherence / interpretation of the [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
or whether they follow their own.

I> **Find your path**
I>
I> Most operating systems inspired by Unix (BSD's, MacOS, Linux) will allow you
I> to get the info of your systems' filesystem hierarchy via [`hier(7)`](https://www.freebsd.org/cgi/man.cgi?hier(7)).
I>
I> {language=shell, line-numbers=off}
I>     $ man hier

These inconsistencies add up so much, a good deal of software infrastructure out
there exists solely to abstract the differences across them. For example, CMake,
Autotools, SFML, SDL2, interpreted programming languages and their standard
libraries are dedicated to normalizing the banal differences across
BSD-derivatives and Linux distributions. Many, many `#ifdef` preprocessor
directives in your C and C++ applications. You want open source, you get choice,
but be aware there's a lot of upkeep cost in keeping these upstream projects
(and even your personal ones) compatible. But I digress, back to terminal stuff.

Why does it matter, why  bring it up? You'll see this kind of stuff everywhere.
So let's separate the common suspects into their respective categories.

## Terminal interface

The terminal interface can be best introduced by stating that there is an
official specification laying out its technical properties, interfaces and
responsibilities in its [POSIX specification](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap11.html).

That's your TTY's, what you see when you move between them, on Linux / BSD
systems, this you can switch between sessions via `<ctrl-alt-F1>` through
`<ctrl-alt-F12>`.

## Terminal emulation

GUI Terminals: Terminal.app, iterm, iterm2, konsole, lxterm, xfce4-terminal,
rxvt-unicode, xterm, roxterm, gnome terminal, cmd.exe + bash.exe

## Shell languages {#shell-languages}

Shell languages *are* programming languages.

Sure you may not compile the code into binaries with [`gcc`](https://gcc.gnu.org/)
or [`clang`](http://clang.llvm.org/). And there may not be a shiny [npm](https://www.npmjs.com/)
for them. But a language is a language.

Each shell interpreter has its own language features. Like with shells
themselves, many will resemble the [POSIX shell language](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_01)
and strive to be compatible with it. ZSH and Bash should be able to understand
POSIX shell script you write, but not the other way around (we will cover that
in [shell interpreters](#shells)).


The top of `.sh` files [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))
statement which can invoke shellscripts in different dialects.

ZSH scripts are implemented by the ZSH shell interpreter, Bash scripts by Bash.
But the languages are not as closely regulated and standardized as say, [C++'s
standards committee](http://www.open-std.org/jtc1/sc22/wg21/) workgroups or
[python's PEPs](https://www.python.org/dev/peps/). Bash and ZSH take features
from Korn and C Shell's languages, but without all the ceremony and bureaucracy
that other languages entail.

## Shell interpreters (Shells) {#shells}

Examples: POSIX sh, Bash, ZSH, csh, tcsh, ksh, fish

Shell interpreters *implement* the shell language. They are a layer on top of
the kernel and are what allow you to, interactively, run commands and
applications inside them.

As of October 2016 the [latest POSIX specification](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/sh.html)
covers in technical detail the responsibilities of the shell.

When it comes to shells and operating systems: each distro or group does their
own darn thing. On most Linux distributions and MacOS, you'll typically be
dropped into Bash. That's because it's what Apple decided to use as a *default
shell* for users.

On BSD you may be placed into use plain vanilla `sh` unless you specify
otherwise during the installation process. In Ubuntu, `/bin/sh` used to be
`bash` ([Bourne Shell](https://en.wikipedia.org/wiki/Bourne_shell)) but was
[replaced with `dash`](https://wiki.ubuntu.com/DashAsBinSh)
([Debian Almquist Shell](https://en.wikipedia.org/wiki/Almquist_shell)). So here
you are thinking "hmm, `/bin/sh`, probably just a plain old POSIX shell",
however, system startup scripts on Ubuntu used to allow non-POSIX scripting
via bash. This is because specialty [shell languages](#shell-languages) like
Bash, ZSH and so on can add a lot of cool and very practical features, but
they're not portable unfortunately!

Recent versions of MacOS include ZSH by default. Linux distributions
typically require you to install it via package manager and installs it to
`/usr/bin/zsh`. BSD systems build it via the port system, [`pkg(8)`](https://www.freebsd.org/cgi/man.cgi?query=pkg&apropos=0&sektion=0&manpath=FreeBSD+10.3-RELEASE+and+Ports&arch=default&format=html)
on FreeBSD or [`pkg_add(1)`](http://man.openbsd.org/pkg_add.1) on OpenBSD
and it will install to `/usr/local/bin/zsh`.

It's fun to experiment with different shells. On many systems you can use
[`chsh -s`](https://en.wikipedia.org/wiki/Chsh) to update the default shell for
a user.

The other thing to mention is that in order for `chsh -s` to work  you
typically need to have it added to [`/etc/shells`](https://bash.cyberciti.biz/guide//etc/shells).
