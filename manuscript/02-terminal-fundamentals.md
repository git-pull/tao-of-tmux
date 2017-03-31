# Terminal fundamentals {#terminal-fundamentals}

Before getting into tmux, a few fundamentals of the command line should be 
reviewed. Often, we're so used to using these out of street smarts and muscle
memory, a great deal of us never see the relation of where these tools stand
next to each other.

Seasoned developers are familiar with zsh, Bash, iTerm2, konsole, /dev/tty,
shell scripting, and so on. If you use tmux, you'll be around these all the
time, regardless whether you're in a GUI on a local machine or SSH'ing
into a remote server.

If you want to learn more about how processes and TTY's work at the kernel level
(data structures and all), the book [*The Design and Implementation of the FreeBSD
Operating System (2nd Edition)*](http://amzn.to/2iTmVyv) by Marshall Kirk
McKusick is nice, particularly, Chapter 4, *Process Management* and Section
8.6, *Terminal Handling*. [*The TTY demystified*](http://www.linusakesson.net/programming/tty/index.php)
by Linus Åkesson (available online) dives into the TTY and is a good read.

Much more exists to glean off the history of Unix, 4.2 BSD, etc. I probably
could have a coffee / tea with you discussing it for hours. You could look at it
from multiple perspectives (The C Language, anything from the Unix/BSD lineage,
etc.), and some clever fellow would likely chime in, mentioning Linux, GNU, and
so on. It's like *Game of Thrones*; there's multiple story arcs you can follow,
some of which intersect. A few good video resources would be [*A Narrative History of BSD*](https://www.youtube.com/watch?v=bVSXXeiFLgk)
by Marshall Kirk McKusick, [*The UNIX Operating System*](https://www.youtube.com/watch?v=tc4ROCJYbm0)
by AT&T, [*Early days of Unix and design of sh*](https://www.youtube.com/watch?v=FI_bZhV7wpI)
by Stephen R. Bourne.

## POSIX standards

Operating systems like macOS (formerly OS X), Linux, and the BSDs, follow
something similar to the POSIX specification in terms of how they square away
various responsibilities and interfaces of the operating system. They're
categorized as ["Mostly POSIX-compliant"](https://en.wikipedia.org/wiki/POSIX#Mostly_POSIX-compliant).

In daily life, we often break compatibility with POSIX standards for reasons of
sheer practicality. Operating systems, like macOS, will drop you right into Bash.
[`make(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/make.html),
a POSIX standard, is [GNU Make](https://www.gnu.org/software/make/) on macOS by
default. Did you know, as of September 2016, POSIX Make has no conditionals?

I'm not saying this to take a run at purists. As someone who tries to remain
compatible in my scripting, it gets hard to do simple things after a while. On
FreeBSD, the default Make [(PMake)](https://www.freebsd.org/doc/en_US.ISO8859-1/books/pmake/)
uses dots between conditionals:

{line-numbers=off}
    .IF

    .ENDIF

But on most Linux systems and macOS, GNU Make is the default, so they get to do:

{line-numbers=off}
    IF

    ENDIF

This is one of the many tiny inconsistencies that span operating systems, their
userlands, their binary / library /  include paths, and adherence /
interpretation of the [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
or whether they follow their own.

I> **Find your path**
I>
I> Most operating systems inspired by Unix (BSD's, macOS, Linux) will allow you
I> to get the info of your systems' filesystem hierarchy via [`hier(7)`](https://www.freebsd.org/cgi/man.cgi?hier(7)).
I>
I> {language=shell, line-numbers=off}
I>     $ man hier

These differences add up. A good deal of software infrastructure out
there exists solely to abstract the differences across them. For example: CMake,
Autotools, SFML, SDL2, interpreted programming languages, and their standard
libraries are dedicated to normalizing the banal differences across
BSD-derivatives and Linux distributions. Many, many `#ifdef` preprocessor
directives in your C and C++ applications. You want open source, you get choice,
but be aware; there's a lot of upkeep cost in keeping these upstream projects
(and even your personal ones) compatible. But I digress, back to terminal stuff.

Why does it matter? Why bring it up? You'll see this stuff everywhere.
So, let's separate the usual suspects into their respective categories.

## Terminal interface

The terminal interface can be best introduced by citing official specification,
laying out its technical properties, interfaces, and responsibilities. This can
be viewed in its [POSIX specification](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap11.html).

This includes TTY's, including text terminals and X sessions within them. On
Linux / BSD systems, you can switch between sessions via `<ctrl-alt-F1>`
through `<ctrl-alt-F12>`.

## Terminal emulators

GUI Terminals: Terminal.app, iterm, iterm2, konsole, lxterm, xfce4-terminal,
rxvt-unicode, xterm, roxterm, gnome terminal, cmd.exe + bash.exe

## Shell languages {#shell-languages}

Shell languages *are* programming languages. You may not compile the code
into binaries with [`gcc`](https://gcc.gnu.org/) or [`clang`](http://clang.llvm.org/).
And there may not be a shiny [npm](https://www.npmjs.com/) for them, but a
language is a language.

Each shell interpreter has its own language features. Like with shells, many
will resemble the [POSIX shell language](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_01)
and strive to be compatible with it. Zsh and Bash should be able to understand
POSIX shell scripts you write, but not the other way around (we will cover this
in [shell interpreters](#shells)).

The top of `.sh` files [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))
statement, which points to the interpreter to run the script in.

Zsh scripts are implemented by the Zsh shell interpreter, Bash scripts by Bash.
But the languages are not as closely regulated and standardized as, say, [C++'s
standards committee](http://www.open-std.org/jtc1/sc22/wg21/) workgroups or
[python's PEPs](https://www.python.org/dev/peps/). Bash and Zsh take features
from Korn and C Shell's languages, but without all the ceremony and bureaucracy
other languages espouse.

## Shell interpreters (Shells) {#shells}

Examples: POSIX sh, Bash, Zsh, csh, tcsh, ksh, fish

Shell interpreters *implement* the shell language. They are a layer on top of
the kernel and are what allow you, interactively, to run commands and
applications inside them.

As of October 2016, the [latest POSIX specification](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/sh.html)
covers in technical detail the responsibilities of the shell.

For shells and operating systems: each distro or group does their own darn
thing. On most Linux distributions and macOS, you'll typically be dropped into
Bash.

On FreeBSD, you may default to a plain vanilla `sh` unless you specify
otherwise during the installation process. In Ubuntu, `/bin/sh` used to be
`bash` ([Bourne Again Shell](https://en.wikipedia.org/wiki/Bourne_shell)) but
was [replaced with `dash`](https://wiki.ubuntu.com/DashAsBinSh)
([Debian Almquist Shell](https://en.wikipedia.org/wiki/Almquist_shell)). So,
here, you are thinking "hmm, `/bin/sh`, probably just a plain old POSIX shell";
however, system startup scripts on Ubuntu used to allow non-POSIX scripting
via Bash. This is because specialty [shell languages](#shell-languages), such as
Bash and Zsh, add a lot of helpful and practical that features may work on one
interpreter but not another. For instance, you would need to install the Zsh
interpreter across all your systems if you rely on Zsh-specialized
scripting. If you conformed with POSIX shell scripting, your scripting would
have the highest level of compatibility at the cost of being more verbose.

Recent versions of macOS include Zsh by default. Linux distributions
typically require you to install it via package manager and install it to
`/usr/bin/zsh`. BSD systems build it via the port system, [`pkg(8)`](https://www.freebsd.org/cgi/man.cgi?query=pkg&apropos=0&sektion=0&manpath=FreeBSD+10.3-RELEASE+and+Ports&arch=default&format=html)
on FreeBSD, or [`pkg_add(1)`](http://man.openbsd.org/pkg_add.1) on OpenBSD,
and it will install to `/usr/local/bin/zsh`.

It's fun to experiment with different shells. On many systems, you can use
[`chsh -s`](https://en.wikipedia.org/wiki/Chsh) to update the default shell for
a user.

The other thing to mention is, for `chsh -s` to work, you typically need to have
it added to [`/etc/shells`](https://bash.cyberciti.biz/guide//etc/shells).

## Summary

To wrap it up, you will hear people talking about shells all the time.
Context is key. It could be:

- A generic way to refer to any terminal you have open. "Type `$ top` into your
  shell and see what happens." (Press q to quit.)
- A server they have to log into. Before the era of the cloud, it would be
  popular for small hosts to sell "C Shells" with root access.
- A shell within a tmux [pane](#panes).
- If scripting is mentioned, it is likely either the script file, an issue
  related to the scripts' behavior, or something about the shell language.

But overall, once you get out of this chapter, go back to doing what you're
doing. If shell is what people say and they understand it, use it. The backing
you have here should make you more confident in yourself. It's an ongoing
battle, these days, to keep street smarts we pick up with book smarts.

In the next chapter, we will touch some terminal basics before diving
deeper into tmux.
