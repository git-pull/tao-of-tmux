# Command Line Kung fu {#cli-kung-fu}

The command line in tmux is one of those areas often uncharted.

## Shorthands

tmux commands and arguments may all be accessed via [`fnmatch(3)`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/fnmatch.html)
patterns.

For instance, you don't need to type `$ tmux attach` every time. `$ tmux attac`,
`$ tmux att`, `$ tmux at`, `$ tmux a` work just as well.

Every tmux command has short-hands, let's try this for `$ tmux new-session`:

{language=shell, line-numbers=off}
    $ tmux new-session

    $ tmux new-sessio

    # ...

    $ tmux new-s

and so on, until:

{language=shell, line-numbers=off}
    $ tmux new-
    ambiguous command: new-, could be: new-session, new-window

## Targets {#targets}

If a command allow target specification, it's usually done through `-t`.

| Thing    | Prefix |
|----------|--------|
| session  | $      |
| window   | @      | 
| pane     | %      |


## Formats {#formats}

tmux provides a minimal template language and set of variables you can use to
access information about your tmux environment.

Formats are often specified via `-F` flag.
