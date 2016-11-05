# Server

Q> ### Wait what, tmux is a server?
Q>
Q> Often when web servers are mentioned, what comes to mind for many
Q> may be rackmounted hardware, to others it may be software running
Q> daemonized on a server and managed through a utility like upstart,
Q> supervisor and so on.
Q>
Q> Unlike web or database software, tmux doesn't require sqecialized
Q> configuration settings or creating a service entry to start things.

tmux uses a client-server model, but the server is forked to the 
background for you.

It surprises some when I mention it because servers often beget
a setup process. But just because server's are involved doesn't entail
hours of configuration on each machine you run it on. There is no
setup.

You don't notice it, but when you use tmux normally, what actually happens
is a server is launched and you're really being connected via a client.

It's just that's streamlined. People think, server, they think pain. They
think time being spent. But not with tmux. Its server, but in the good way.

The server part of tmux is how your sessions are able to stay alive even
when you detached your client.
