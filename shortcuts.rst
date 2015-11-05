.. _shortcuts:
.. _keybindings:
   
=========
Shortcuts
=========

.. tip::

    :ref:`Prefix key` is pressed before a short cut!

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``C-b``               Send the prefix key (C-b) through to the
                      application.
``C-o``               Rotate the panes in the current window forwards.
``C-z``               Suspend the tmux client.
``!``                 Break the current pane out of the window.
``"``                 Split the current pane into two, top and bottom.
``#``                 List all paste buffers.
``$``                 Rename the current session.
``%``                 Split the current pane into two, left and right.
``&``                 Kill the current window.
``'``                 Prompt for a window index to select.
``,``                 Rename the current window.
``-``                 Delete the most recently copied buffer of text.
``.``                 Prompt for an index to move the current window.
``0 to 9``            Select windows 0 to 9.
``:``                 Enter the tmux command prompt.
``;``                 Move to the previously active pane.
``=``                 Choose which buffer to paste interactively from a
                      list.
``?``                 List all key bindings.
``D``                 Choose a client to detach.
``[``                 Enter copy mode to copy text or view the history.
``]``                 Paste the most recently copied buffer of text.
``c``                 Create a new window.
``d``                 Detach the current client.
``f``                 Prompt to search for text in open windows.
``i``                 Display some information about the current window.
``l``                 Move to the previously selected window.
``n``                 Change to the next window.
``o``                 Select the next pane in the current window.
``p``                 Change to the previous window.
``q``                 Briefly display pane indexes.
``r``                 Force redraw of the attached client.
``s``                 Select a new session for the attached client
                      interactively.
``L``                 Switch the attached client back to the last session.
``t``                 Show the time.
``w``                 Choose the current window interactively.
``x``                 Kill the current pane.
``{``                 Swap the current pane with the previous pane.
``}``                 Swap the current pane with the next pane.
``~``                 Show previous messages from tmux, if any.
``Page Up``           Enter copy mode and scroll one page up.
``Up, Down``          Change to the pane above, below, to the left, or to
``Left, Right``       the right of the current pane.
``M-1 to M-5``        Arrange panes in one of the five preset layouts:
                      even-horizontal, even-vertical, main-horizontal,
                      main-vertical, or tiled.
``M-n``               Move to the next window with a bell or activity
                      marker.
``M-o``               Rotate the panes in the current window backwards.
``M-p``               Move to the previous window with a bell or activity
                      marker.
``C-Up, C-Down``      Resize the current pane in steps of one cell. 
``C-Left, C-Right``
``M-Up, M-Down``      Resize the current pane in steps of five cells.
``M-Left, M-Right``
===================   ====================================================

Source: tmux manpage [1]_.

To get the text documentation of a ``.1`` manual file:

.. code-block:: bash

    $ nroff -mdoc tmux.1|less

.. [1] http://sourceforge.net/p/tmux/tmux-code/ci/master/tree/tmux.1

