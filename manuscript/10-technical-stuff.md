# Technical Stuff {#technical-stuff}

Since you've read this far, you already know there is a [server](#server)
automatically started and stopped for you when you use tmux. So let's go a bit
into the innards and how tmux works.

![Server w/ laptop](images/info/server-with-laptop.png)

## Under the hood

There's how you use it in practice, and the hard technical reality of how something
operates under the hood.

The point of an application that's built for you to use is it elegantly hides that
complexity of how it operates underneath. Though, tmux actually has really great
code underneath, down to the point its a joy to read it. You really have to thank
Nicholas Marriott, Thomas Adam and Tiago Cunha for that.

## Project basics

tmux is programmed in [C](https://en.wikipedia.org/wiki/C_(programming_language)).

tmux is cross-platform. In order to allow the code base to build across a
variety of unix-like systems, [autotools](https://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html)
and some cool C tricks are used.

The files that make up the project build system are in [`configure.ac`](https://github.com/tmux/tmux/blob/master/configure.ac),
[`Makefile.am`](https://github.com/tmux/tmux/blob/master/Makefile.am), and the
[preprocessor directives](https://en.wikipedia.org/wiki/C_preprocessor#Conditional_compilation)
in [`compat.h`](https://github.com/tmux/tmux/blob/master/compat.h).

`compat.h` works in tandem with autotools to route header definitions to system
headers, installed libraries or the `compat/` folder if they're not present on
the system.

## Event passing

The innards of tmux is powered by [libevent](http://libevent.org/), a cross-platform event
notification library. libevent is an abstraction layer on top of OS-specific event notifiers.
