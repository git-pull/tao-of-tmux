
{frontmatter}
 
# Foreword 

The terminal is a direct link to your system. It's characterized by high
contrast, fixed width text, raw input and output, flexibility, yet stringent.
Precise by nature - it acts upon what we say, not what we mean.

It's ignorant of your intentions. It's developers designed it for utility, and it
happens in a setting where happiness and convenience is tied legacy implementations
on terminal displays, the UNIX / DOS legacy, and an ever growing set of new
developers using terminals despite having graphical options.

Terminals are mainstream. They're not going away.

Microsoft and Windows Terminal. The Rust community and its writing of shell and
CLI utilities that are defying expectations. Version managers that handle
python, node, rust, PHP, and ruby versioning. Continual improvement on systems
such as ZSH, Bash, Fish, and other systems. There's just too many to mention,
and if I kept going, it'd be out of date in a month.

There is still mystery to the terminal for me. When text turns into garbage,
cells corrupt recall an NES cartridge that decides to corrupt with a life of its
own. I launch a new terminal or pane, wave it off and keep going. What I mean to
say is:

1. We're human.

   We aren't computers, we're thinking, and often have more than just our terminal open.

   We may have handbook or documentation open alongside a window manager.
   We may be interfacing with other human being outside of the computer.
   Pair coding. 
   Watching YouTube or a Podcast.
2. It's not feasible to know everything.

   Terminals are a way to get from point A to point B. We're using it for value, but
   we won't upend our work, we'll probably procrastinate, and not understand
   many of the systems underneath the hood.

   Some of us may eventually.

   Programming and IT rely more and more on a huge dependency tree
   of software. We're on working with, and on top of, yet so far away from unix
   parts. In the same way we have hearts and aren't cargiologists, have brains
   and aren't neurologists, don't take it open yourself to stunt your own
   learning by feeling you need to learn everything.

## About this book

I've helped thousands learn tmux through my free resource under the name
[The Tao of tmux](https://tmuxp.git-pull.com/en/latest/about_tmux.html), which I
kept as part of the documentation for the [tmuxp session manager](https://github.com/tony/tmuxp).
And now, it's been expanded into a full-blown book with refined graphics,
examples, and much more.

You do not need a book to use or understand tmux. If you want a technical
manual, look at the [manpage for tmux](http://man.openbsd.org/OpenBSD-current/man1/tmux.1).
Manpages, however, are rarely sufficient to wrap your brain around
abstract concepts; they're there for reference. This learning book is the
culmination of years of explaining tmux to others online and in person.

In this book, we will break down tmux by its objects, from servers
down to panes. It also includes a rehash of terminal facilities we use every day
to keep us autodidacts up to speed with what is what. I've included numerous
examples of projects, permissively licensed source code, and workflows designed
for efficiency in the world of the terminal.

tmux is a tool I find useful. While I don't attach it to my personal identity,
it's been part of my daily life for years. Besides the original resource,
I've written a [popular tmux starter configuration](https://github.com/tony/tmux-config),
a [pythonic tmux library](https://libtmux.git-pull.com), and a
[tmux session manager](https://tmuxp.git-pull.com).

I am writing this from vim running in a tmux pane, inside a window, in a session
running on a tmux server, through a client.

A word to absolute beginners: Don't feel you need to grasp the concepts
of the command line and terminal multiplexing in a single sitting. You have the
choice of picking out concepts of tmux you like, according to your
needs or interests. If you haven't installed tmux yet, please view the
[Installation section](#appendix-installation) in the Appendix of the book.

Follow [@TheTaoOfTmux](https://twitter.com/TheTaoOfTmux) for
updates or [share on Twitter](https://twitter.com/intent/tweet?text=I%27m%20reading%20The%20Tao%20of%20tmux%20online%20at&url=https://leanpub.com/the-tao-of-tmux/read&hashtags=tmux&via=TheTaoOfTmux)!

## Styles

Formatted text `like this` is source code.

Formatted text with a $ in front is a terminal command. `$ echo 'like this'`.
The text can be typed into the console, without the dollar character. For more
information on the meaning of the "dollar prompt", check out [*What is the
origin of the UNIX $ (dollar) prompt?*](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)
on Super User.

In tmux, shortcuts require a [prefix key](#prefix-key) to be sent beforehand.
For instance, `Prefix` + `d` will detach a tmux client from its session. This
prefix, by default, is `<Ctrl-b>`, but users can override it. This is discussed in
greater detail in *the prefix key* section and [*configuration*](#config).

## How this book is structured

First, anything involving [installation](http://man.openbsd.org/OpenBSD-current/man1/tmux.1)
and hard technical details are in the Appendix. A lot of books use installation
instructions as filler in the early chapters. For me, it's more of not wanting
to confuse beginners.

For special circumstances, like [tmux on Windows 10](#appendix-windows-bash), I
decided adding screenshots is best, since many readers may be more comfortable
with a visual approach.

[*Thinking in tmux*](#thinking-tmux) goes over what tmux does and how it relates to
the GUI desktops on our computers.  You'll understand the big picture of
what tmux is and how it can make your life easier.

[*Terminal Fundamentals*](#terminal-fundamentals) shows the text-based
environments you'll be dealing with. It's great for those new to tmux, but also
presents technical background for developers, who learned the ropes through
examples and osmosis. At the end of this section, you'll be more confident and
secure using the essential components underpinning a modern terminal
environment.

[*Practical usage*](#practical-usage) covers common bread-and-butter uses for
you to use tmux immediately.

[*Server*](#server) gives life to the unseen workhorse behind the scenes
powering tmux. You'll think of tmux differently and may be impressed a
client-server architecture could be presented to end users so seamlessly.

[*Sessions*](#sessions) are the containers holding windows. You'll learn what
sessions are and how they help organize your workspace in the terminal. You'll
learn how to manipulate and rename and traverse sessions.

[*Windows*](#windows) are what you see when tmux is open in front of you.
You'll learn how to rename and move windows. 

[*Panes*](#panes) are a terminal in a terminal. This is where you get to work and
do your magic! You'll learn how to create, delete, move between, and resize
panes.

[*Configuration*](#config) discusses customization of tmux and sets the
foundation for how to think about `.tmux.conf` so you can customize your own.

[*Status bar and styling*](#status-bar) is devoted to the customization
of the status line and colors in tmux. As a bonus, you'll even learn how to
display system information like CPU and memory usage via the status line.

[*Scripting tmux*](#scripting-tmux) goes into command [aliases](#aliases)
and the advanced and powerful [Targets](#targets) and [Formats](#formats)
concepts.

[*Technical stuff*](#technical-stuff) is a glimpse at tmux source code and how it
works under the hood. You may learn enough to impress colleagues who already use
tmux. If you like programming on Unix-like systems, this one is for you.

[*Tips and tricks*](#tips-and-tricks) wraps up with a whirlwind of useful
terminal tutorials you can use with tmux to improve day to day development and
administration experience.

[*Cheatsheets*](#appendix-cheatsheets) are organized tables of commands,
shortcuts, and formats grouped by section.

## Donations

If you enjoy my learning material or my open source software projects, please
consider donating. Donations go directly to me and my current and future open source
projects and are not squandered. Visit <http://www.git-pull.com/support.html>
for ways to contribute.

## Formats

This book is available for sale on [Leanpub](https://leanpub.com/the-tao-of-tmux) and [Amazon Kindle](http://amzn.to/2gPfRhC).

It's also available to read for [free on the web](https://leanpub.com/the-tao-of-tmux/read).

## Errata {#errata}

This is my first book. I am human and make mistakes.

If you find errors in this book, please submit them to me at tao.of.tmux <AT>
nospam git-pull.com.

You can also submit a pull request via <https://github.com/git-pull/tao-of-tmux>.

I will update digital versions of the book with the changes where applicable.

## Thanks

Thanks to the [contributors](https://github.com/git-pull/tao-of-tmux/graphs/contributors)
for spotting errors in this book and submitting errata through GitHub. In
addition, readers like Graziano Misuraca, who looked through the book closely,
providing valuable feedback.

Some copy, particularly in [cheatsheets](#appendix-cheatsheets), comes straight out
of the manual of tmux, which is [ISC-licensed](https://github.com/tmux/tmux/blob/master/COPYING).

## Book Updates and tmux changes

This book was written for tmux 2.3, released September 2016.

As of January 2017, it's trivial to push out minor changes to
Leanpub. Kindle is harder.

tmux does intermittently receive updates. I've accommodated many over the past 5
years on my personal configurations and software libraries set with [continuous integration tests against multiple tmux versions](https://github.com/tony/libtmux/blob/master/.travis.yml).
Sometimes, publishers overplay version numbers to make it seem as if it's worth
striking a new edition of a book over it. It's effective for them, but I'd
rather be honest to my readership.

If you're considering keeping up to date with new features and adjustments to tmux,
the [`CHANGES`](https://github.com/tmux/tmux/blob/master/CHANGES) file in the
project source serves as a way to see what's updated between official releases.
