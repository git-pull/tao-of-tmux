# Practical usage {#practical-usage}

This is the easiest part; open your terminal and type `tmux`, hit enter.

{language=shell, line-numbers=off}
    $ tmux

You're in tmux.

## The prefix key {#prefix-key}

The *prefix* is how we send commands into tmux. With this, we can split windows,
move windows, switch windows, switch sessions, send in custom commands, you name
it.

And it's a hump we have to get over.

It's kind of like [*Street Fighter*](https://en.wikipedia.org/wiki/Street_Fighter).
In this video game, the player inputs a combination of buttons in sequence to
perform flying spinning kicks and shoot fireballs; sweet. As the player grows
more accustomed with the combos, they repeat moves by intuition, since they
develop muscle memory.

Without understanding how to send *command sequences* to tmux via the prefix
key, you'll be dead in the water.

Key sequences will come up later if you use Vim, Emacs, or other TUI (Terminal
User Interface) applications. If you haven't internalized the concept, let's do
it now. Prior experience command sequences in TUI/GUI applications will come in
handy.

When you memorize a key combo, it's one less time you'll be moving your hand
away from the keyboard to grab your mouse. You can focus your short-term memory
on getting stuff done, resulting in fewer mistakes.

Q> ### Coming from ``GNU Screen``?
Q>
Q> Your tmux prefix key can be set via your tmux configuration later!  In
Q> your `~/.tmux.conf` file, set the `prefix` option:
Q>
Q> {language=shell, line-numbers=off}
Q>     set-option -g prefix C-a
Q>
Q> This will set the prefix key to `screen(1)`'s (another terminal
Q> multiplexer's) prefix key.

The default leader prefix is `<Ctrl-b>`. While holding down the `control` key,
press `b`.

X> ### Sending tmux commands
X>
X> Practice:
X>
X> 1. Press `control` key down and *hold it*.
X> 2. Press `b` and hold it.
X> 3. Release both keys at the same time.
X>
X> Try it a few times. It may feel unnatural until you've done it a couple
X> times, which is normal when memorizing shortcuts.
X>
X> Now, let's try something:
X>
X> `<Ctrl-b> d`. So,
X>
X> 1. Press `control` key down and *hold it*.
X> 2. Press `b` and hold it.
X> 3. Release both keys at the same time.
X> 4. Hit `d`!
X>
X> You've sent tmux your first command, and you're now outside of tmux!

You've detached the tmux session you were in. You can reattach via `$ tmux
attach`. 

### Nested tmux sessions

You can also send the prefix key to *nested* tmux sessions. For instance, if
you're inside a tmux client on a *local* machine and you SSH into a *remote* machine
in one of your panes, on the remote machine, you can attach the client via `tmux
attach` as you normally would. To send the prefix key to the machine's tmux
client, not your local one, hit the prefix key again.

So, if your prefix key is the default, `<Ctrl-b>`, do `<Ctrl+b>` + `b` again,
*then* hit the shortcut for what you want to do.

Example: If you wanted to create a window on the remote machine, which would normally
be `<Ctrl-b>` + `c` locally, it'd be `<Ctrl-b>` + `b` + `c`.

Hereinafter, the book will refer to shortcuts by `Prefix`. Instead
of `<Ctrl-B> + d`, you will see `Prefix` + `d`.

## Session persistence and the server model

If you use Linux or a similar system, you've likely brushed through [Job Control](https://en.wikipedia.org/wiki/Job_control_(Unix)),
such as [`fg(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/fg.html), [`jobs(1)`](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/jobs.html).
tmux behavior feels similar, like you ran `<Ctrl-z>` except, technically, you
were in a "job" all along. You were just using a client to view it.

Another way of understanding it: `<Ctrl-b>` + `d` closed the client connection,
therefore, 'detached' from the session.

Your tmux client disconnected from the server instance. The session, however, is
still running in the background.

## It's all commands

Multiple roads can lead you to the same behavior. *Commands* are what tmux uses
to define instructions for setting options, resizing, renaming, traversing,
switching modes, copying and pasting, and so forth.

- [Configs](#config) are the same as automatically running commands via
  `$ tmux command`.
- Internal tmux commands via `Prefix` + `:` prompt.
- Settings defined in your configuration can also set shortcuts, which can
  execute commands via keybindings via `bind-key`.
- Commands called from CLI via `$ tmux cmd`
- To pull it all together, [source code](#technical-stuff) files are prefixed
  `cmd-`.

## Summary

We've established tmux automatically creates a server upon starting it. The
server allows you to detach and later reattach your work. The keyboard
sequences you send to tmux require understanding how to send the prefix key.

Keyboard sequences, configuration, and command line actions all boil down to the
same core commands inside tmux.  In our next chapter, we will cover the server.
