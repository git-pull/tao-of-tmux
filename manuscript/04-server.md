# Server {#server} 

The server holds [sessions](#sessions) and the [windows](#windows) and
[panes](#panes) within them.

When tmux starts, you are connected to a server via a socket connection.
What you see presented in your shell is merely a client connection. In
this chapter, we go into the secret power plant allowing your terminal
applications to persist for months or even years if you want to.

{width=90%}
![](images/info/server.png)

## What? tmux is a server?

Often, when "server" is mentioned, what comes to mind for many
may be rackmounted hardware; to others, it may be software running
daemonized on a server and managed through a utility, like upstart,
supervisor, and so on.

Unlike web or database software, tmux doesn't require specialized
configuration settings or creating a service entry to start things.

tmux uses a client-server model, but the server is forked to the 
background for you.

## Zero config needed

You don't notice it, but when you use tmux normally, a server is launched and
being connected via a client.

tmux is so streamlined, the book could continue to explain usage and not even
mention servers. But, I'd rather you have a true understanding of how it works
on systems. The implementation feels like magic, while still fulfilling the
unix expectations of utilitarianism. One cannot deny it's exquisitely executed
from a user experience standpoint.

How is it utilitarian? We'll go into it more in future chapters, where we dive
into [Formats](#formats), [Targets](#targets), and tools such as [libtmux](https://github.com/tony/libtmux)
I made, which utilize these features.

It surprises some, because servers often beget a setup process. But servers
being involved doesn't entail hours of configuration on each machine you run on.
There's no setup.

When people think server, they think pain. It invokes an image of digging
around `/etc/` for configuration files and flipping settings on and off just to
get basic systems online. But not with tmux. It's a server, but in the good way.

## Stayin' alive

The server part of tmux is how your sessions can stay alive, even after your client
is detached.

You can detach a tmux session from an SSH server and reconnect later.
You can detach a tmux session, stop your X server in Linux/BSD, and reattach
your tmux session in a TTY or new X server.

The tmux server won't go away until all sessions are closed.

## Servers hold sessions

One server can contain one or multiple [sessions](#sessions).

Starting tmux after a server already running will create a new session inside
the existing server. 

W> ### Advanced: Multiple servers
W>
W> tmux is nimble. To use a separate server, pass in the `-L` flag to any
W> command.
W>
W> `tmux -L moo` - connect to server under socket name "moo" and attach
W> a new session. Create server if none already exists for socket.
W>
W> `tmux -L moo attach` will attempt to re-attach a session, if one exists.

## How servers are "named"

The default name for the server is `default`, which is stored as a socket in
`/tmp`. The default directory for storing this can be overridden via setting
the `TMUX_TMPDIR` environment variable.

So, something like:

{language=shell, line-numbers=off}
    $ export TMUX_TMPDIR=$HOME
    $ tmux

Will give you a tmux directory created within your `$HOME` folder. On OS X,
your home folder will probably be something like `/Users/yourusername`. On
other systems, it may be `/home/yourusername`. If you want to find out, type
`echo $HOME`.

## Clients

Servers will have clients (you) connecting to them.

When you connect to a session and see windows and panes, it's a client
connection into tmux.

You can retrieve a list of active client connections via:

{language=shell, line-numbers=off}
    $ tmux list-clients

These commands, and the other `list-` commands, in practice, are rare. But, they
are part of tmux scriptability should you want to get creative. The [scripting tmux](#scripting-tmux)
chapter will cover this in greater detail.

## Clipboard {#clipboard}

tmux clients wield a powerful clipboard feature to copy and paste across
sessions, windows and panes.

Much like vi, tmux handles clipboard as a mode (or a state) in which a pane is
temporarily placed, in while text can be copied.

The default key to enter copy mode is `Prefix` + `[`.

1. From within, use `[space]` to enter copy mode.
2. Use the arrow keys to adjust the text to be selected.
3. Press `[enter]` to copy the selected text.

The default key to paste the text copied is `Prefix` + `]`.

I> *Vi-like copy-paste*
I>
I> In your [config](#config), put this:
I>
I> {language=shell, line-numbers=off}
I>     # Vi copypaste mode
I>     set-window-option -g mode-keys vi
I>     bind-key -t vi-copy 'v' begin-selection
I>     bind-key -t vi-copy 'y' copy-selection

In addition to the "copy mode", tmux has advanced functionality to
programatically copy and paste. Later in the book, the [Capturing pane content](#capture-pane)
section in the [Scripting tmux](#scripting-tmux) chapter goes into
`$ tmux capture-pane` and how you can use [targets](#targets) to copy pane
content into your paste buffer or files with `$ tmux save-buffer`.

## Summary

The server is one of the fundamental underpinnings of tmux. Mostly, it is
invisible to the user. 

The server can hold one or more *sessions*. You can copy and paste between
sessions via the clipboard. In the next chapter we will go deeper into the role
sessions play and how they help you organize and control your terminal
workspace.
