
{frontmatter}

# Forward 

Pretty much all my friends swear to using tmux. I remember going out at night
for drinks and the 3 of us would take a seat at a round table and take our smart
phones out. It was the days back when phones still had mechanical keyboards. All
3 of us, by happenstance, drawn our phones from our pockets. We just planned 2
hours earlier on IRC to use Oleg's car to pick us up and drive us into the city.

Despite our home computers sleeping or being off, our username's in the channel
persisted in the chatroom list. Our screens were lit by a kaleidoscope of colors
on a black background. We ssh'd with ConnectBot into our cloud servers and
reattached [`screen(1)`](https://en.wikipedia.org/wiki/GNU_Screen). Just as it
hit 2AM, our Turkish coffee arrived, the `|away` trailing our online nicknames
one by one fell off.

Funnily, even though we knew each other by our real names, we sometimes opted to
call each other by our nicks. It's something about how the personal
relationships, formed completely through text, persist in real life.

It seemed as if it were orchestrated, but each of us fell into the same ebb and
flow of operating our lives. No one told us to do it, but inch by inch we
incrementally optimized our lifestyles personally and professionally to arrive
at destinations that felt eerily alike.

Like many things in life, when we act on autopilot, we sometimes arrive at
similar destinations. This is often completely unplanned.

So when I go off and write a learning book on a computer application, I hope
to write it for human beings. Not to sell you on tmux, not to make you like
it, or hate it, but to tell you what it is, how some use it and leave the rest
up to you.

## About this book

This book is currently under development. It's available to read for
[free on the web](https://leanpub.com/the-tao-of-tmux/read).

You do not need a book to use or understand tmux. But if there is a book, let
this be the one.

I don't like to give a slipshod effort. If I'm going to take the time to write a
book, I'm giving it 100% of my effort.

tmux to me is a tool I find incredible use with, while I don't attach it to my
identity, it's been part of my daily life for years. I've helped thousands of
people learn tmux through my free resource under the same name
[The Tao of tmux](https://tmuxp.readthedocs.io/en/latest/about_tmux.html),
written a [popular tmux starter configuration](https://github.com/tony/tmux-config),
a [pythonic tmux library](https://github.com/tony/libtmux) and a
[tmux session manager](https://github.com/tony/tmuxp). You'd think I'm trying
to build this big thing around tmux, in reality, it's just that useful.

I am writing this from vim in a tmux pane, inside a window, in a session, on
the server, through a client.  It's not that I don't care about accuracy, but
if you want a technical manual, the manpage for tmux is quite sufficient in
this regard.

A word to absolute beginners, do not feel like you need to grasp the concepts
of command line and terminal multiplexing in a single sitting. You have the
choice of picking out the concepts of tmux that you like according to your
needs or curiosities. If you do not have it installed, please view the
[Installation section](#appendix-installation) in the Appendix of the book.

## How this book is structured

First, anything involving installation and hard technical details are in the
appendix (back of the book). A lot of books tend to use this as filler. For me
it's more of not wanting to leave complete beginners behind.

For special circumstances like Windows 10, I opted that going so far as adding
screenshots since a fair share may be more comfortable by a visual approach.

The first Chapter, [*Thinking Tmux*](#chapter-01), goes over a breakdown of what
tmux does and how it relates to the GUI desktops we already use on our
computers.  You will get to wrap your brain around what tmux is and how it can
make your life easier.

The second Chapter, [*Terminal Fundamentals*](#chapter-02), gives a run through of the common
systems you'll be dealing with in the realm of the text-based console. It's
great for those new to tmux, but also to put some technical backing for
developers who learned the ropes through examples and osmosis. You'll be more
confident and secure in the fundamental underpinnings of using multiplexers
and shells.

In chapter three, [*Practical Usage*](#chapter-03), covers common bread and
butter use cases for you to start using tmux daily, starting now.

Chapter Four, [*Technical Stuff*](#chapter-04) is intensive, "nice to know"
stuff about the internals of tmux. You may learn enough to be able to 
impress friends who currently use tmux daily. If you like programming on
POSIX-like systems, this one is for you.

[*Server*](#chapter-05) gives life to unseen workhorse that powers tmux behind
the scenes. You'll think of tmux in a different way, and may be impressed to see
a client-server architecture could be implemented so seamlessly to end users.

[*Session*](#chapter-06) drops you into the world launching tmux places you into.
You'll learn what a session is and how it helps you organize your workspace
in the terminal. You'll learn how you can manipulate and rename your session,
which leaves you an an excellent transition to our next destination.

[*Window*](#chapter-07) is what you see when tmux is open right in front
of you. You'll learn to rename and move windows, to create, delete, move between
and copy and paste been panes.

[*Panes*](#chapter-08) - A terminal in a terminal. This is where we leave you to
do your magic and get to work!

[*Configuration*](#chapter-09) discusses customization of tmux, via keybindings,
status line and behavior. You'll even know how to show your CPU usage and
memory via the status line.

[*Recipes*](#chapter-10) wraps it up with a whirlwind of a customized tmux
configuration, a yaml file to launch tmux sessions using
[tmuxp](https://github.com/tony/tmuxp). In addition, we'll cover a Python API
for tmux called [libtmux](https://github.com/tony/libtmux). You'll get to see
some tricked out tmux examples.

## Donations

I do offer my learning material for free on the internet, as well as maintain
several open source projects. If you'd like to support my day-to-day open
source participation please check out <http://www.git-pull.com/support.html>
for ways to contribute.

## Available Formats

This book is available for sale on [Leanpub](https://leanpub.com/the-tao-of-tmux), [Amazon Kindle](https://www.amazon.com/gp/product/B01MG342KU/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B01MG342KU&linkCode=as2&tag=gitpull-20&linkId=e6d3f08ad92bfea1cf62d735b6a90bdf) and [Apple iBooks](https://geo.itunes.apple.com/us/book/the-tao-of-tmux/id1168912720?mt=11&at=1001lrwP).

It's also available for free to [free on the web](https://leanpub.com/the-tao-of-tmux/read).

## Errata

If you find errors in this book please submit them to me at tao.of.tmux <AT>
nospam git-pull.com. I will update digital versions of the book with the 
changes where applicable.
