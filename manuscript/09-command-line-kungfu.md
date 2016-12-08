# Command Line Kung fu {#cli-kung-fu}

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
