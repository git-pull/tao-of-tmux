
{frontmatter}

# Forward

Pretty much all my friends swear to using tmux. I remember going out at night for drinks and the 3 of us would take a seat at a round table and take our smart phones out. It was the days back when phones still had mechanical keyboards. All 3 of us, by happenstance, drawn our phones from our pockets. We just planned 2 hours earlier on IRC to use Oleg's car to pick us up and drive us into the city.

Despite our home computers sleeping or being off, our username's in the channel persisted in the chatroom list. Our screens were lit by a kaleidoscope of colors on a black background. We ssh'd with ConnectBot into our cloud servers and reattached `screen(1)`[^screen]. Just as it hit 2AM, our Turkish coffee arrived, the `|away` trailing our online nicknames one by one fell off.

Funnily, even though we knew each other by our real names, we sometimes opted to call each other by our nicks. It's something about how the personal relationships, formed completely through text, persist in real life.

It seemed as if it were orchestrated, but each of us fell into the same ebb and flow of operating our lives. No one told us to do it, but inch by inch we incrementally optimized to our lifestyle personally and professionally that felt eerily alike.

Like many things in life, when we act on autopilot, we sometimes arrive at similar destinations. This is often completely unplanned.

So when I go off and write a technical book on a computer application, I hope to write it for human beings. Not to sell you on tmux, not to make you like it, or hate it, but to tell you what it is, how some use it and leave the rest up to you.

## About this book

You do not need a book to use or understand tmux. But if there is a book, let this be the one.

I don't like to give a slipshod effort. if I'm going to take the time to write a book, I'm giving it 100% of my effort.

tmux to me is a tool I find incredible use with, while I don't attach it to my identity, it's been part of my daily life for years. I've helped thousands of people learn tmux through my free resource under the same name [The Tao of tmux](https://tmuxp.readthedocs.io/en/latest/about_tmux.html), written a [popular tmux starter configuration](https://github.com/tony/tmux-config), a [pythonic tmux library](https://github.com/tony/libtmux) and a [tmux session manager](https://github.com/tony/tmuxp). You'd think I'm trying to build this big thing around tmux, in reality, it's just that useful.

I am writing this from vim in a tmux pane, inside a window, in a session, on the server, through a client.  It's not that I don't care about accuracy, but if you want a technical manual, the manpage for tmux is quite sufficient in this regard.

A word to absolute beginners, do not feel like you need to grasps the concepts of command line and terminal multiplexing in a single sitting. You have the choice of picking out the concepts of tmux that you like according to your needs or curiosities. If you do not have it installed, please view the [Installation section](#appendix-installation) in the Appendix of the book.

## How this book is structured

First, anything involving installation and hard technical details are in the appendix.

A lot of books tend to use this as filler. For me it's more of not wanting to leave complete beginners behind.

For special circumstances like Windows 10, I opted that going so far as adding screenshots since a fair share may be more comfortable by a visual approach.

[^screen]: GNU Screen (screen) is a terminal multiplexer that allows detaching (sending applications to the background) and reattaching (returning the background applications to the foreground). It predates tmux. Some still prefer screen to tmux. The official website is at https://www.gnu.org/software/screen/.
