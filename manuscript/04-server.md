# Server {#server} 

![Server](images/info/server.png) 
Q> ### Wait what, tmux is a server?

Q> Often when "server" is mentioned, what comes to mind for many
Q> may be rackmounted hardware, to others it may be software running
Q> daemonized on a server and managed through a utility like upstart,
Q> supervisor and so on.
Q>
Q> Unlike web or database software, tmux doesn't require specialized
Q> configuration settings or creating a service entry to start things.

tmux uses a client-server model, but the server is forked to the 
background for you.

## Zero config needed

You don't notice it, but when you use tmux normally, what actually happens
is a server is launched and you're really being connected via a client.

It's just that it's streamlined for normal usage. I could continue the book and
not even mention servers. But I'd rather readers a solid understanding that
while tmux feels like magic, it's really utilitarian first and foremost, but
exquisitely executed from a user experience standpoint.

How is it utilitarian? We'll go into it more in future chapters where I dive
into [Formats](#formats), [Targets](#targets) and tools such as [libtmux](https://github.com/tony/libtmux)
which I made that utilize the often unnoticed advanced features under the hood.

It surprises some when I mention it because servers often beget
a setup process. But just because servers are involved doesn't entail
hours of configuration on each machine you run it on. There is no
setup.

When people people think server, they think pain. They visualize time being
spent digging around `/etc/` for configuration files and flipping settings on
and off just to get basic systems online. But not with tmux. It's a server, but
in the good way.

## Stayin' alive

The server part of tmux is how your sessions are able to stay alive even
after your client is detached.

## Servers hold sessions

One server can contain one or multiple [sessions](#sessions).

Recurring usage of tmux after a server already exist will create a new
session inside that server. 

W> ### Advanced: Multiple servers
W>
W> tmux is nimble. if you want to use a separate server, just pass in
W> the `-L` flag to any command.
W>
W> `tmux -L moo` - start a new tmux server + session if non-exists under
W> the socket name "moo"
W>
W> `tmux -L moo attach` try to re-attach to session if one exists

## How servers are "named"

The default name for the server is `default`. It is stored in a socket in
`/tmp`. The default directory for storing this can be overridden via setting
the `TMUX_TMPDIR` environment variable.

So something like:

{language=shell, line-numbers=off}
    $ export TMUX_TMPDIR=$HOME
    $ tmux

Will give you a tmux directory created within your `$HOME` folder. On OS X,
your home folder will probably be something like `/Users/yourusername`, on
other systems, `/home/yourusername` will be most common. If you want to find
out for sure, just type `echo $HOME`.
