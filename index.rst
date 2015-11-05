.. The Tao of Tmux documentation master file, created by
   sphinx-quickstart on Tue Nov  3 22:08:49 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

The Tao of Tmux
===============

Contents:

.. toctree::
   :maxdepth: 2

   basic_usage
   configuration
   shortcuts
   server
   session
   window
   pane
   plugins
   changes
   internals

.. figure:: _static/tao-tmux-screenshot.png
    :scale: 60%
    :align: center

    BSD-licensed terminal multiplexer.

tmux is geared for developers and admins who interact regularly with
CLI (text-only interfaces)

In the world of computers, there are 2 realms:

1. The text realm
2. The graphical realm

Tmux resides in the text realm. This is about fixed-width fonts and that
old fashioned black terminal.

tmux is to the console what a desktop is to gui apps. It's a world inside
the text dimension. Inside tmux you can:

- multitask inside the terminal, run multiple applications.
- have multiple command lines (pane) in the same window
- have multiple windows (window) in the workspace (session)
- switch between multiple workspaces, like virtual desktops

=============
Thinking Tmux
=============

Text-based window manager
-------------------------

=================== ====================== ===============================
**tmux**            **"Desktop"-Speak**    **Plain English**
------------------- ---------------------- -------------------------------
Multiplexer         Multi-tasking          Multiple applications
                                           simulataneously.
Session             Desktop                Applications are visible here
Window              Virtual Desktop or     A desktop that stores it own
                    applications           screen
Pane                Application            Performs operations
=================== ====================== ===============================

.. aafig::
    :textual:

    +----------------------------------------------------------------+
    |  +--------+--------+ +-----------------+ +-----------------+   |
    |  | pane   | pane   | | pane            | | pane            |   |
    |  |        |        | |                 | |                 |   |
    |  |        |        | |                 | |                 |   |
    |  +--------+--------+ |                 | +-----------------+   |
    |  | pane   | pane   | |                 | | pane            |   |
    |  |        |        | |                 | |                 |   |
    |  |        |        | |                 | |                 |   |
    |  +--------+--------+ +-----------------+ +-----------------+   |
    |  | window          | | window          | | window          |   |
    |  \--------+--------/ \-----------------/ \-----------------/   |
    +----------------------------------------------------------------+
    | session                                                        |
    \----------------------------------------------------------------/

- 1 :term:`Server`.

  - has 1 or more :term:`Session`.

    - has 1 or more :term:`Window`.

      - has 1 or more :term:`Pane`.

.. seealso:: :ref:`glossary` has a dictionary of tmux words.

CLI Power Tool
--------------

Multiple applications or terminals to run on the same screen by splitting
up 1 terminal into multiple.

One screen can be used to edit a file, and another may be used to
``$ tail -F`` a logfile.

.. aafig::

   +--------+--------+
   | $ bash | $ bash |
   |        |        |
   |        |        |
   |        |        |
   |        |        |
   |        |        |
   |        |        |
   +--------+--------+

.. aafig::

   +--------+--------+
   | $ bash | $ bash |
   |        |        |
   |        |        |
   +--------+--------+
   | $ vim  | $ bash |
   |        |        |
   |        |        |
   +--------+--------+

tmux supports as manys terminals as you want.


.. aafig::
   :textual:

   +---------+---------+
   | $ bash  | $ bash  |
   |         |         |
   |         |         |     /-----------------\
   +---------+---------+ --> |'switch-window 2'|
   | $ vim   | $ bash  |     \-----------------/
   |         |         |              |
   |         |         |              |
   +---------+---------+              |
   | '1:sys*  2:vim'   |              |
   +-------------------+              |
             /------------------------/
             |
             v
   +---------+---------+
   | $ bash  | $ bash  |
   |         |         |
   |         |         |
   +---------+---------+
   | $ vim   | $ bash  |
   |         |         |
   |         |         |
   +---------+---------+
   | '1:sys*  2:vim'   |
   +-------------------+

You can switch between the windows you create.

.. _resume:

Resume everything later
-----------------------

You can leave tmux and all applications running (detach), log out, make a
sandwich, and re-(attach), all applications are still running!

.. aafig::
   :textual:

   +--------+--------+
   | $ bash | $ bash |
   |        |        |
   |        |        |     /------------\ 
   +--------+--------+ --> |   detach   | 
   | $ vim  | $ bash |     | 'Ctrl-b b' |     
   |        |        |     \------------/     
   |        |        |            |
   +--------+--------+            |
               /------------------/
               |
               v
   +-----------------------+
   | $ [screen detached]   |
   |                       |
   |                       |
   |                       |
   |                       |
   |                       |
   |                       |
   +-----------------------+
              v
              |
              v
   +-----------------------+
   | $ [screen detached]   |
   | $ tmux attach         |
   |                       |     /------------\
   |                       | --> | attaching  |
   |                       |     \------------/
   |                       |            |
   |                       |            |
   +-----------------------+            |
                                        |
            /---------------------------/
            |
            v
   +--------+--------+
   | $ bash | $ bash |
   |        |        |
   |        |        |
   +--------+--------+
   | $ vim  | $ bash |
   |        |        |
   |        |        |
   +--------+--------+

Manage workflow
---------------

- System administrators monitor logs and services.
- Programmers like to have an editor open with a CLI nearby.

Applications running on a remote server can be launched inside of a tmux
session, detached, and reattached next timeyour `"train of thought"`_ and
work.

Multitasking. Preserving the thinking you have. 

.. _"train of thought": http://en.wikipedia.org/wiki/Train_of_thought

===============
Installing tmux
===============

Tmux is packaged on most Linux and BSD systems.

For the freshest results on how to get tmux installed on your system,
"How to install tmux on <my distro>" will do, as directions change and are
slightly different between distributions.

This documentation is written for version **1.8**. It's important that
you have the latest stable release of tmux. The latest stable version is
viewable on the `tmux homepage`_.

**Mac OS X** users may install that latest stable version of tmux through
`MacPorts`_, `fink`_ or `Homebrew`_ (aka brew).

If **compiling from source**, the dependencies are `libevent`_ and
`ncurses`_.

.. _tmux homepage: http://tmux.sourceforge.net/
.. _libevent: http://www.monkey.org/~provos/libevent/
.. _ncurses: http://invisible-island.net/ncurses/
.. _MacPorts: http://www.macports.org/
.. _Fink: http://fink.thetis.ig42.org/
.. _Homebrew: http://www.brew.sh

=======
License
=======

Copyright 2013-2015, Tony Narlock. All rights reserved.

This page is licensed `Creative Commons BY-NC-ND 3.0 US`_.

.. _Creative Commons BY-NC-ND 3.0 US: http://creativecommons.org/licenses/by-nc-nd/3.0/us/


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
