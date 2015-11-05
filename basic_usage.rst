.. _basic_usage:
   
===========
Basic usage
===========

Start a new session
-------------------

.. code-block:: bash

    $ tmux

That's all it takes to launch yourself into a tmux session.

.. tip:: Common pitfall

    Running ``$ tmux list-sessions`` or any other command for listing tmux
    entities (such as ``$ tmux list-windows`` or ``$ tmux list-panes``).
    This can generate the error "failed to connect to server".
    
    This could be because:

        - tmux server has killed its' last session, killing the server.
        - tmux server has encountered a crash. (tmux is highly stable,
          this will rarely happen)
        - tmux has not be launched yet at all.

.. _Prefix key:

The prefix key
--------------

Tmux hot keys have to be pressed in a special way. **Read this
carefully**, then try it yourself.

First, you press the *prefix* key. This is ``C-b`` by default.

Release. Then pause. For less than second. Then type what's next.

``C-b o`` means: Press ``Ctrl`` and ``b`` at the same time. Release,
Then press ``o``.

**Remember, prefix + short cut!** ``C`` is ``Ctrl`` key.

Session Name
------------

Sessions can be *named upon creation*.

.. code-block:: bash

    $ tmux new-session [-s session-name]

Sessions can be *renamed after creation*.

=============== =========================================================
Command         .. code-block:: bash

                    $ tmux rename-session <sesion-name>

Short cut       ``Prefix`` + ``$``
=============== =========================================================

Window Name
-----------

Windows can be *named upon creation*.

.. code-block:: bash

    $ tmuxp new-window [-n window-name]

Windows can be *renamed after creation*.

=============== ==========================================================
Command         .. code-block:: bash

                    $ tmux rename-window <new-name>

Short cut       ``Prefix`` + ``,``
=============== ==========================================================

Creating new windows
--------------------

=============== =========================================================
Command         .. code-block:: bash

                    $ tmux new-window [-n window-name]

Short cut       ``Prefix`` + ``c``

                You may then rename window.
=============== =========================================================

Traverse windows
----------------

By number

.. code-block:: bash

    $ tmux select-window

Next

.. code-block:: bash

    $ tmux next-window

Previous

.. code-block:: bash

    $ tmux previous-window

Last-window

.. code-block:: bash

    $ tmux last-window

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``n``                 Change to the next window.
``p``                 Change to the previous window.
``w``                 Choose the current window interactively.
``0 to 9``            Select windows 0 to 9.

``M-n``               Move to the next window with a bell or activity
                      marker.
``M-p``               Move to the previous window with a bell or activity
                      marker.

===================   ====================================================

Move windows
------------

Move window

.. code-block:: bash

    $ tmux move-window [-t dst-window]

Swap the window

.. code-block:: bash

    $ tmux swap-window [-t dst-window]

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``.``                 Prompt for an index to move the current window.
===================   ====================================================


Move panes
----------

.. code-block:: bash

    $ tmux move-pane [-t dst-pane]

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``C-o``               Rotate the panes in the current window forwards.
``{``                 Swap the current pane with the previous pane.
``}``                 Swap the current pane with the next pane.
===================   ====================================================


Traverse panes
--------------

Shortcut to move between panes.

.. code-block:: bash

    $ tmux last-window

.. code-block:: bash

    $ tmux next-window

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``Up, Down``          Change to the pane above, below, to the left, or to
``Left, Right``       the right of the current pane.
===================   ====================================================


Recipe: tmux conf to ``hjkl`` commands, add this to your
``~/.tmux.conf``::

    # hjkl pane traversal
    bind h select-pane -L
    bind j select-pane -D
    bind k select-pane -U
    bind l select-pane -R

Kill window
-----------

.. code-block:: bash

    $ tmux kill-window

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``&``                 Kill the current window.
===================   ====================================================


Kill pane
---------

.. code-block:: bash

    $ tmux kill-pane [-t target-pane]

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``x``                 Kill the current pane.
===================   ====================================================

Kill window
-----------

.. code-block:: bash

    $ tmux kill-window [-t target-window]

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``&``                 Kill the current window.
===================   ====================================================

Splitting windows into panes
----------------------------

.. code-block:: bash

    $ tmux split-window [-c start-directory] <shell-command>

Tmux windows can be split into multiple panes.

===================   ====================================================
Short cut             Action
-------------------   ----------------------------------------------------
``%``                 Split the current pane into two, left and right.
``"``                 Split the current pane into two, top and bottom.
===================   ====================================================


