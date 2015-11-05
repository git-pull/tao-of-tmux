.. _plugins:

=======
Plugins
=======

There are a plethora of plugins available for tmux

Status lines
------------

Tmux allows configuring a status line that displays system information,
window list, and even pipe in the ``stdout`` of an application.

You can use `tmux-mem-cpu-load`_ to get stats (requires compilation) and
`basic-cpu-and-memory.tmux`_. You can pipe in a bash command to a tmux
status line like:

.. code-block:: ini

    $(shell-command)

So if ``/usr/local/bin/tmux-mem-cpu-load`` outputs stats to
``stdout``, then ``$(tmux-mem-cpu-load)`` is going to output the first
line to the status line.  The interval is determined by the
``status-interval``::

    set -g status-interval 1

.. _tmux-mem-cpu-load: https://github.com/thewtex/tmux-mem-cpu-load
.. _basic-cpu-and-memory.tmux: https://github.com/zaiste/tmuxified/blob/master/scripts/basic-cpu-and-memory.tmux

Examples
--------

- https://github.com/tony/tmux-config - works with tmux 1.5+. Supports
  screen's ``ctrl-a`` :ref:`Prefix key`. Support for system cpu, memory,
  uptime stats.
- Add yours, edit this page on github.

