
{frontmatter}

# Important

This is a prerelease version of *The Tao of tmux*. The estimated release date is
January 22nd, 2017. [Please submit errata via GitHub or email](#errata). Thank
you!

Also feel free to follow [@TheTaoOfTmux](https://twitter.com/TheTaoOfTmux) for
updates or [share on Twitter](https://twitter.com/intent/tweet?text=I%27m%20reading%20the%20prerelease%20of%20The%20Tao%20of%20tmux%20online%20at&url=https://leanpub.com/the-tao-of-tmux/read&hashtags=tmux&via=TheTaoOfTmux)!

# Foreword 

Pretty much all my friends use tmux. I remember going out at night
for drinks and the 3 of us would take a seat at a round table and take our smart
phones out. This was back when phones still had physical "QWERTY" keyboards.

Despite our home computers being asleep or turned off, our usernames in the IRC channel we frequently visited
persisted in the chatroom list. Our screens were lit by a kaleidoscope of colors
on a black background. We ssh'd with ConnectBot into our cloud servers and
reattached by running [`screen(1)`](https://en.wikipedia.org/wiki/GNU_Screen). Just as it
hit 2AM, our Turkish coffee arrived, the `|away` status indicator trailing our online nicknames disappeared.

It was funny that even though we knew each other by our real names, we sometimes opted to
call each other by our nicks. It's something about how personal
relationships, formed completely online, persist in real life.

It seemed as if it were orchestrated, but each of us fell into the same ebb and
flow of living our lives. No one told us to do it, but inch by inch we
incrementally optimized our lifestyles personally and professionally to arrive
at destinations that felt eerily alike.

Like many things in life, when we act on autopilot, we sometimes arrive at
similar destinations. This is often completely unplanned.

So when I go off and write an educational book about a computer application, I hope
to write it for human beings. I'm not trying to sell you on tmux, not to make you like
it, or hate it, but to tell you what it is, how some people use it. I'll leave the rest
up to you.

## About this book

This book is currently under development. It's available to read for
[free on the web](https://leanpub.com/the-tao-of-tmux/read).

You do not need a book to use or understand tmux. But if there is such a book, let
this be the one.

I don't like to make a slipshod effort. If I'm going to take the time to write a
book, I'm giving it 100%.

tmux to me is a tool I find incredible useful. While I don't attach it to my personal
identity, it's been part of my daily life for years. I've helped thousands of
people learn tmux through my free resource under the name
[The Tao of tmux](https://tmuxp.git-pull.com/en/latest/about_tmux.html),
written a [popular tmux starter configuration](https://github.com/tony/tmux-config),
a [pythonic tmux library](https://github.com/tony/libtmux), and a
[tmux session manager](https://github.com/tony/tmuxp).

I am writing this from vim running in a tmux pane, inside a window, in a session, on
the server, through a client.

It's not that I don't care about accuracy, but
if you want the definitive manual, look at the [manpage for tmux](http://man.openbsd.org/OpenBSD-current/man1/tmux.1).

A word to absolute beginners: don't feel you need to grasp the concepts
of the command line and terminal multiplexing in a single sitting. You have the
choice of picking out concepts of tmux that you like according to your
needs or interests. If you haven't installed tmux yet, please view the
[Installation section](#appendix-installation) in the Appendix of the book.

## Styles

Formatted text `like this` is source code.

Formatted text with a $ in front is a terminal command. `$ echo 'like this'`.
This means you type that text right into the console, without the
dollar character. For more information on the meaning of the "dollar prompt", check out
[*What is the origin of the UNIX $ (dollar)
prompt?*](https://superuser.com/questions/57575/what-is-the-origin-of-the-unix-dollar-prompt)
on Super User.

Shortcuts all require a [prefix key](#prefix-key) be sent before hand. Sections
describing similar keyboard commands typically will appear in a
table. For example:

| Shortcut         | Action                                             |
|------------------|----------------------------------------------------|
|`Prefix` + `s`    | Detach client from session.                        |

## How this book is structured

First, anything involving [installation](http://man.openbsd.org/OpenBSD-current/man1/tmux.1)
and hard technical details are in the Appendix. A lot of
books tend to use installation instructions as filler in the early chapters. For me it's more of not wanting to confuse
complete beginners.

For special circumstances like tmux on Windows 10, I decided that adding screenshots is best
since many readers may be more comfortable with a visual approach.

[*Thinking Tmux*](#thinking-tmux) goes over what
tmux does and how it relates to the GUI desktops already on our
computers.  You'll wrap your brain around what tmux is and how it can
make your life easier.

[*Terminal Fundamentals*](#terminal-fundamentals) shows the text-based
environments you'll be dealing with. It's
great for those new to tmux, but also presents some technical background for
developers who learned the ropes through examples and osmosis. At the end of this
section you'll be more confident and secure using the essential components underpinning
a modern terminal environment.

[*Practical Usage*](#practical-usage) covers common bread and
butter uses for you to start using tmux immediately.

[*Server*](#server) gives life to the unseen workhorse that powers tmux behind
the scenes. You'll think of tmux differently, and may be impressed that
a client-server architecture could be presented so seamlessly to end users.

[*Sessions*](#sessions) are the containers holding your tmux
windows. You'll learn what a session is and how it helps organize your
workspace in the terminal. You'll learn how to manipulate and rename your
session.

[*Windows*](#windows) are what you see when tmux is open in front of you.
You'll learn how to rename and move windows. 

[*Panes*](#panes) are a terminal in a terminal. This is where you get to work and
do your magic! You'll learn how to create, delete, move between, and
copy and paste between panes.

[*Configuration*](#config) discusses customization of tmux via keybindings and
status line behavior. You'll even learn how to show your CPU and
memory usage via the status line.

[Command Line Kung Fu](#cli-kung-fu) goes into command [shorthands](#shorthands),
as well as the advanced and powerful [Targets](#targets) and [Formats](#formats)
concepts.

[*Technical Stuff*](#technical-stuff) is a glimpse at tmux source code and how it
works under the hood. You may learn enough to be able to impress friends who
currently use tmux daily. If you like programming on Unix-like systems, this
one is for you.

[*Tips and Tricks*](#tips-and-tricks) wraps up with a whirlwind of useful
terminal tutorials you can use in conjunction with tmux to improve your day to
day development and administration experience.


## Donations

If you enjoy my learning material or my open source software projects, please
consider donating. Donations go directly to me and my current and future open source
projects and are not squandered. Visit <http://www.git-pull.com/support.html>
for ways to contribute.

## Available Formats

This book is available for sale on [Leanpub](https://leanpub.com/the-tao-of-tmux) and [Amazon Kindle](http://amzn.to/2gPfRhC).

It's also available to read for [free on the web](https://leanpub.com/the-tao-of-tmux/read).

## Errata {#errata}

If you find errors in this book please submit them to me at tao.of.tmux <AT>
nospam git-pull.com.

You can also submit a pull request via <https://github.com/git-pull/tao-of-tmux>.

I will update digital versions of the book with the changes where applicable.

## Book Updates and tmux changes

This book was written for tmux 2.3, released September 2016.

tmux does intermittently receive updates. I've accommodated many of them over
the past 5 or so years on my personal configurations as well as software
libraries.

Refer to tmux's [`CHANGES`](https://github.com/tmux/tmux/blob/master/CHANGES)
file for updates on what changes and when.

As of November 2016, it's pretty trivial for me to push out minor changes to this book on
Leanpub and Amazon. So don't worry about having to pay unless tmux
radically changes.
