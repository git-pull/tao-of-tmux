# Status bar and styling {#status-bar}

The status bar, or *status line*, serves as customizable taskbar in the bottom
of tmux. It is comprised of 3 sections. The status fields on either side
of the status line are customizable. The center field is a list of windows.

![](images/09-status-bar/overview.png)

The `status-left` and `status-right` option can be configured to accept 
many variables.

It's [configurable](#config) through the `.tmux.conf` file and modifiable live
through using `$ tmux set-option`.

I> *Finding your current status line settings* 
I>
I> {language=shell, line-numbers=off}
I>     $ tmux show-options -g | grep status

## Window status symbols

This window list is between the left and right status bar regions.

tmux indicates status of a window through symbols. Seen below:

| Symbol | Meaning                                                      |
|--------|--------------------------------------------------------------|
| *      | Denotes the current window.                                  |
| -      | Marks the last window (previously selected).                 |
| #      | Window is monitored and activity has been detected.          |
| !      | A bell has occurred in the window.                           |
| ~      | The window has been silent for the monitor-silence interval. |
| M      | The window contains the marked pane.                         |
| Z      | The window's active pane is zoomed.                          |

Reminder: A pane can be [zoomed](#zoom-pane) via `Prefix` + `z`. To unzoom,
press `Prefix` + `z` or move left / right / up / down panes.

## Date and time

`status-left` and `status-right` accept variables for the date. 

This happens via piping the status templates through [`format_expand_time`](https://github.com/tmux/tmux/blob/2.3/format.c#L868)
in `format.c`, which routes right into [`strftime(3)`](http://pubs.opengroup.org/onlinepubs/9699919799/functions/strftime.html)
from `time.h`.

A full list of variables can be found in the documentation for `strftime(3)`.
This can viewed through `$ man strftime` on Unix-like systems.

## Shell command output

You can also call applications, such as [tmux-mem-cpu-load](https://github.com/thewtex/tmux-mem-cpu-load)
and [conky](https://github.com/brndnmtthws/conky), and [powerline](#powerline).

For this example, we'll use `tmux-mem-cpu-load`. This works on Unix-like systems
like FreeBSD, Linux distributions as well as macOS.

It requires installing [CMake](https://cmake.org) and `git` through your package
managers. As well, you must have a C++ compiler. On macOS, this is done through
installing Xcode CLI Utilities. You can do this by going to Applications ->
Utilities, launching Terminal.app and typing `$ xcode-select --install`. macOS
can use [Homebrew](https://brew.sh/) to install the CMake package. Linux 
distributions allow you to install cmake and clang via package manager.

Also, install `git` via your package manager before this step.

{language=shell, line-numbers=off}
    $ git clone https://github.com/thewtex/tmux-mem-cpu-load.git
    $ cd tmux-mem-cpu-load
    $ mkdir ./build
    $ cd ./build
    $ cmake ..
    $ make
    
    # macOS, no sudo required
    $ make install

    # Linux, BSD will require sudo / root to install
    $ sudo make install

If successful, you should see the output below:

{language=shell, line-numbers=off}
    [100%] Built target tmux-mem-cpu-load
    Install the project...
    -- Install configuration: "MinSizeRel"
    -- Installing: /usr/local/bin/tmux-mem-cpu-load

You can now add `#(tmux-mem-cpu-load)` to your `status-left` or `status-right`
option. In the "[Dressed up](#status-bar-example-dressed-up)" example below, I
use `status-left` and also theme it to be green:

`#[fg=green,bg=default,bright]#(tmux-mem-cpu-load)`

So to apply it to your theme, you need to double check what you already have.
You may have information on there you want to keep.

{language=shell, line-numbers=off}
    $ tmux show-option -g status-right
    status-right " "#{=21:pane_title}" %H:%M %d-%b-%y"

Copy what you had in response (or change, rearrange as you see fit) then add the
`#(tmux-mem-cpu-load)` to it. You can apply the new status line in your current
tmux session via `$ tmux set-option -g status-right`:

{language=shell, line-numbers=off}
    $ tmux set-option -g status-right '"#{=21:pane_title}" #(tmux-mem-cpu-load) %H:%M %d-%b-%y'

Also, note how I switched out the double quotes on either side of the option
with single quotes. This is recommended, since there are double quotes inside.

You can do this with anything, for instance, try adding [`uptime`](https://linux.die.net/man/1/uptime).
This could be done by adding `#(uptime)` to your status line. Typically the
output is pretty long, so trim it down by doing something like this:

`#(uptime | cut -f 4-5 -d " " | cut -f 1 -d ",")``

In the next section, we go into how you can style (color) tmux.

## Styling

The *colors* available to tmux are:

- `black`, `red`, `green`, `yellow`, `blue`, `magenta`, `cyan`, `white`.
- bright colors such as `brightred`, `brightgreen`, `brightyellow`,
  `brightblue`, `brightmagenta`, `brightcyan`.
- `colour0` through `colour255` from the 256-color set.
- `default`
- hexadecimal RGB code like `#000000`, `#FFFFFF`, similar to HTML colors.

### Status line

You can use `[bg=color]` and `[fg=color]` to adjust the text color and
background within for status line text. This works on `status-left` and
`status-right`.

Let's say you want to style the background:

Command: `$ tmux set-option status-style fg=white,bg=black`

In config: `status-style fg=white,bg=black`

In the examples at the end of the chapter, you will see complete examples of how
colors can be used, also.

### Clock styling

You can style the color of the tmux clock via:

{lang="text", line-numbers=off}
    set-option -g clock-mode-colour white

Reminder: Clock mode can be opened with `$ tmux clock-mode` or `Prefix` + `t`.
Pressing any key will exit clock mode.

### Prompt colors

The benefit of wrapping your brain around this styling is you will see
it `message-command-style`, `message style` and so on.

Let's try this:

{lang="shell", line-numbers=off}
    $ tmux set-option -ag message-style fg=yellow,blink\; set-option -ag message-style bg=black

![Top: default scheme for prompt. Bottom: newly-styled.](images/09-status-bar/prompt.png)

## Styling while using tmux

So, you want to customize your tmux status line before you write the changes to
your [config](#config) file.

Start by grabbing your current status line section you want to edit, for
instance:

{lang="text", line-numbers=off}
    $ tmux show-options -g status-left
    > status-left "[#S] "
    $ tmux show-options -g status-right
    > status-right " "#{=21:pane_title}" %H:%M %d-%b-%y"

Also, you can try to snip off the variable with `| cut -d' ' -f2-`:

{lang="text", line-numbers=off}
    $ tmux show-options -g status-left | cut -d' ' -f2-
    > "[#S] "
    $ tmux show-options -g status-right | cut -d' ' -f2-
    > " "#{=21:pane_title}" %H:%M %d-%b-%y"

Then, add the options to your [configuration](#config).

To be sure your configuration fully works, you can start it in a different
server via `tmux -Lrandom`, verify the settings, and close it. This is helpful
to make sure your config file isn't missing any styling info.

## Toggling status line 

The tmux status line can be hidden, as well. Turn it off:

{language=shell, line-numbers=off}
    $ tmux set-option status off

And, turn it on:

{language=shell, line-numbers=off}
    $ tmux set-option status on

The above is best for scripting, but if you're binding it to a keyboard
shortcut, *toggling*, or reversing the current option, can be done via omitting
the on/off value:

{language=shell, line-numbers=off}
    $ tmux set-option status

Bind toggling status line to `Prefix` + `q`:

{language=shell, line-numbers=off}
    $ tmux bind-key q set-option status

## Example: Default config

![](images/09-status-bar/default.png)

This is an example of the default config, you see if your tmux
configuration has no status styling.

{line-numbers=off}
    status on
    status-interval 15
    status-justify left
    status-keys vi
    status-left "[#S] "
    status-left-length 10
    status-left-style default
    status-position bottom
    status-right " "#{=21:pane_title}" %H:%M %d-%b-%y"
    status-right-length 40
    status-right-style default
    status-style fg=black,bg=green

## Example: Dressed up {#status-bar-example-dressed-up}

![](images/09-status-bar/dressed up.png)

{line-numbers=off}
    status on
    status-interval 1
    status-justify centre
    status-keys vi
    status-left "#[fg=green]#H #[fg=black]• #[fg=green,bright]#(uname -r | cut -c 1-6)#[default]"
    status-left-length 20
    status-left-style default
    status-position bottom
    status-right "#[fg=green,bg=default,bright]#(tmux-mem-cpu-load) #[fg=red,dim,bg=default]#(uptime | cut -f 4-5 -d " " | cut -f 1 -d ",") #[fg=white,bg=default]%a%l:%M:%S %p#[default] #[fg=blue]%Y-%m-%d"
    status-right-length 140
    status-right-style default
    status-style fg=colour136,bg=colour235

    # default window title colors
    set-window-option -g window-status-fg colour244  # base0
    set-window-option -g window-status-bg default

    # active window title colors
    set-window-option -g window-status-current-fg colour166  # orange
    set-window-option -g window-status-current-bg default

Configs can print the output of an application. In this example,
[tmux-mem-cpu-load](https://github.com/thewtex/tmux-mem-cpu-load) is providing
system statistics in the right-side section of the status line.

To build tmux-mem-cpu-load, you have to install [CMake](https://cmake.org/)
and have a C++ compiler, like [clang](http://clang.llvm.org/) or [GCC](https://gcc.gnu.org/).

On Ubuntu, Debian, and Mint machines, you can do this via `$ sudo apt-get
install cmake build-essential`. On macOS w/ [brew](http://brew.sh/) via `$ brew
install cmake`.

Source: <https://github.com/tony/tmux-config>

## Example: Powerline

![](images/09-status-bar/powerline.png)

The most full-featured solution available for tmux status lines is
[powerline](https://github.com/powerline/powerline/), which heavily utilizes the
shell command outputs, not only to give direct system statistics, but also to
generate graphical-like styling.

To get the styling to work correctly, special fonts must be installed. The
easiest way to use this is to install [powerline fonts](https://github.com/powerline/fonts),
a collection of fixed width coder fonts patched to support [Wingdings](https://en.wikipedia.org/wiki/Wingdings)-like
symbols.

[Installation instructions](https://powerline.readthedocs.io/en/latest/installation.html)
are on Read the Docs. For a better idea:

{language=shell, line-numbers=off}
    $ pip install --user powerline-status psutil

[psutil](https://github.com/giampaolo/psutil), a required dependency of
powerline, is a cross-platform tool to gather system information.

Assure you [properly configured python with your PATHs](#troubleshoot-site-paths) and try this:

{line-numbers=off}
    set -g status-interval 2
    set -g status-right '#(powerline tmux right)'

## Summary

Configuring the status line is optional. It can use the the output of programs
installed on your system to give you specialized information such as CPU, ram
and I/O usage. By default, you'll at least have a window list and a clock.

In addition, you can customize the colors of the status line, clock and prompt.
By default, it's only a green bar with dark text, so take some time to customize
yours if you want and save it to your [configuration](#config).

In the next chapter, we will go into the command line and scripting features of
tmux.
