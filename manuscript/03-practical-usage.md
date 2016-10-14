# Practical Usage

This is the easiest part, open up your terminal and type `tmux`, hit enter.

    $ tmux

You're in tmux.

## The leader key / prefix

The leader key is how we send commands into tmux. With this, we can split windows, move windows, switch windows, switch sessions, send in custom commands, you name it.

And its a hump we have to get over. Without you understanding how to send `command sequences` to tmux, you'll pretty much be dead in the water.

So the default leader prefix is `<Ctrl-b>`. So that's holding down the `control` key, then `b`.

Q> ## Customizing your prefix key / Coming from ``GNU Screen``?
Q>
Q> Your tmux prefix key can be set via your tmux configuration later on!  In your
Q> `~/.tmux.conf` file, set the `prefix` option:
Q>     set-option -g prefix C-a
Q>
Q> This will set the prefix key to `screen(1)`'s (another terminal multiplexer's)
Q> prefix key.

Try that.

1. Press `control` key down, and *hold it*.
2. Press `b`, and hold it.
3. Release both keys at the same time.

That's it. Now let's try something:

`<Ctrl-b> d`. So,

1. Press `control` key down, and *hold it*.
2. Press `b`, and hold it.
3. Release both keys at the same time.
4. Hit `d`!

You've just detached the tmux session you were in.

## Detaching a tmux session

When you did `<Ctrl-b> d`, 
