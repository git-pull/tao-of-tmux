.. _configuration:

=============
Configuration
=============

Tmux can be configured via a configuration at ``~/.tmux.conf``.

Depending on your tmux version, there is different options available.

Vi-style copy and paste
-----------------------

.. code-block:: ini

    # Vi copypaste mode
    set-window-option -g mode-keys vi
    bind-key -t vi-copy 'v' begin-selection
    bind-key -t vi-copy 'y' copy-selection

Aggressive resizing for clients
-------------------------------

.. code-block:: ini

    setw -g aggressive-resize on

Reload config
-------------

``<Prefix>`` + ``r``.

.. code-block:: ini

    bind r source-file ~/.tmux.conf \; display-message "Config reloaded."
