# Recipes {#recipes}

## Read the tmux manual in style

`$ man tmux` is the command to load up the "[man page](https://en.wikipedia.org/wiki/Man_page)" for tmux. You can do the same to find instructions for just about any comment, here's a couple of fun ones:

{language=shell, line-numbers=off}
    $ man less
    $ man man

[most(1)](http://www.jedsoft.org/most/) is a solid
[`PAGER`](http://pubs.opengroup.org/onlinepubs/9699919799//utilities/man.html)
that drastically improves readability of manual pages by acting as a syntax
highlighter for manual pages.

![left: man, version 1.6c on MacOS Sierra. right: MOST v5.0.0](images/11-recipes/most.png)
