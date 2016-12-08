# Practical Usage {#practical-usage}

This is the easiest part, open up your terminal and type `tmux`, hit enter.

    $ tmux

You're in tmux.

## The prefix key

The *prefix* is how we send commands into tmux. With this, we can split windows,
move windows, switch windows, switch sessions, send in custom commands, you name
it.

And it's a hump we have to get over.

When I was a kid, there was a video game (depending on your generation you may
know it) called Sonic 3. One of the carnival levels had this ridiculous section
where you could only get passed if you motioned your controller in a special
fashion. Coined the ["Barrel of Doom"](https://gaming.stackexchange.com/questions/10361/i-never-made-it-past-carnival-night-zone),
if you don't get past it, you won't progress to the next stage, game over.

That's kind of what the prefix key in tmux is like. Without you understanding
how to send *command sequences* to tmux via the prefix key, you'll pretty much
be dead in the water.

And the same will also end up coming up in later cases if you use Vim or Emacs
and many TUI (Terminal User Interface) applications. So if you haven't
internalized the concept, let's do it now. If you already have done similar
command sequences before in TUI/GUI applications, that'll come in helpful.

Q> ### Coming from ``GNU Screen``?
Q>
Q> Your tmux prefix key can be set via your tmux configuration later on!  In
Q> you `~/.tmux.conf` file, set the `prefix` option:
Q>
Q>      set-option -g prefix C-a
Q>
Q> This will set the prefix key to `screen(1)`'s (another terminal
Q> multiplexer's) prefix key.

So the default leader prefix is `<Ctrl-b>`. So that's holding down the
`control` key, then `b`.

X> ### Sending tmux commands
X>
X> Try that.
X>
X> 1. Press `control` key down, and *hold it*.
X> 2. Press `b`, and hold it.
X> 3. Release both keys at the same time.
X>
X> That's it. Now let's try something:
X>
X> `<Ctrl-b> d`. So,
X>
X> 1. Press `control` key down, and *hold it*.
X> 2. Press `b`, and hold it.
X> 3. Release both keys at the same time.
X> 4. Hit `d`!
X>
X> You've just send tmux your first command! And you're back at the plain old
X> terminal now!

You've just detached the tmux session you were in. So let's speak about what
just happened.

## Session persistence and the server model

If you're familiar with Linux, you may have heard of [Job Control](https://en.wikipedia.org/wiki/Job_control_(Unix)),
such as [`fg(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/fg.html), [`jobs(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/jobs.html).

This is a similar concept, it feels like you just ran `<ctrl-z>` and sent
except technically you were in a "job" all along, you were just using a client
to view it.

When you did `<Ctrl-b> d`, just detached your session.

Your tmux client disconnected from the server instance. The session however is
still running in the background.
