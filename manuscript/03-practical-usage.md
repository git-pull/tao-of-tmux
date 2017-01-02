# Practical Usage {#practical-usage}

This is the easiest part, open up your terminal and type `tmux`, hit enter.

{language=shell, line-numbers=off}
    $ tmux

You're in tmux.

## The prefix key {#prefix-key}

The *prefix* is how we send commands into tmux. With this, we can split windows,
move windows, switch windows, switch sessions, send in custom commands, you name
it.

And it's a hump we have to get over.

It's kind of like [Street Fighter](https://en.wikipedia.org/wiki/Street_Fighter).
In this game the player inputs a combination of buttons in sequence to
perform flying spinning kicks and shoot fireballs; sweet. As the player grew
more accustomed with the combos, they'd begin to repeat moves by intuition
since they've committed to muscle memory.

That's kind of what the prefix key in tmux is like. Without understanding how to
send *command sequences* to tmux via the prefix key, you'll pretty much be
dead in the water.

Key sequences will also come up in later if you use Vim or Emacs and other TUI
(Terminal User Interface) applications. If you haven't internalized the
concept let's do it now. If you already have done similar command sequences
before in TUI/GUI applications, that'll come in handy.

When you memorize a key combo it's one less time you'll be moving your hand
away from the keyboard to grab your mouse. You can focus your short term memory
on getting stuff done, that means less mistakes.

Q> ### Coming from ``GNU Screen``?
Q>
Q> Your tmux prefix key can be set via your tmux configuration later on!  In
Q> your `~/.tmux.conf` file, set the `prefix` option:
Q>
Q>      set-option -g prefix C-a
Q>
Q> This will set the prefix key to `screen(1)`'s (another terminal
Q> multiplexer's) prefix key.

The default leader prefix is `<Ctrl-b>`. That's holding down the
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
X> You've just sent tmux your first command! And you're back at the plain old
X> terminal now!

You've just detached the tmux session you were in.

## Session persistence and the server model

If you're familiar with Linux, you may have heard of [Job Control](https://en.wikipedia.org/wiki/Job_control_(Unix)),
such as [`fg(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/fg.html), [`jobs(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/jobs.html).

This is a similar concept, it feels like you just ran `<ctrl-z>` and sent
except technically you were in a "job" all along, you were just using a client
to view it.

A better way of putting it: `<Ctrl-b> d` closed the client connection, therefore
'detached' from the session.

Your tmux client disconnected from the server instance. The session however is
still running in the background.

## It's all just commands

Configs and Commands - [Configs](#config) are the same as automatically running
commands via `$ tmux command`.

Keybindings and Commands - Keyboard shortcuts in tmux are just shorthands for
commands you can do via `$ tmux command`.

Even if you look at the [source code](#technical-stuff) there are files prefixed
`cmd-`. The essence of what you're doing in tmux is easier and more transparent
than it seems.
