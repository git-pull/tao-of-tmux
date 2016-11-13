# Technical Stuff

![Server w/ laptop](images/info/server-with-laptop.png)

There's how you use it in practice, and the hard technical reality of how something
operates under the hood.

The point of an application that's built for you to use is it elegantly hides that
complexity of how it operates underneath. Though, tmux actually has really great
code underneath, down to the point its a joy to read it. You really have to thank
Nicolas Mariott, Thomas Adam and Tiago Cunha for that.

Did you know that when you start tmux, you're automatically creating a server in the background?

The innards of tmux is powered by [libevent](http://libevent.org/), a cross-platform event
notification library. libevent is an abstraction layer on top of OS-specific event notifiers.

## Targets

## Formats
