{backmatter}

# Appendix: Installing tmux {#appendix-installation}

## MacOS / OS X

### brew

    $ brew install tmux

### macports

    $ sudo port install tmux

### fink

    $ fink install tmux

## Linux

### Ubuntu / Mint / Debian, etc.

    $ sudo apt-get install tmux

### CentOS / Fedora / Redhat, etc.

    $ sudo yum install tmux

### Arch Linux (pacman)

    $ sudo pacman -S tmux 

### Gentoo (portage)

    $ sudo emerge --ask app-misc/tmux

## BSD

### FreeBSD

#### pkg(1)

    # pkg install tmux

#### pkg_add(1)

    # pkg_add -r tmux

### OpenBSD

As of OpenBSD 4.6, tmux is part of the base system[^openbsd47].

If you are using an earlier version:

    # pkg_add tmux

[^openbsd47]: https://www.openbsd.org/46.html

### NetBSD

    $ make -C /usr/pkgsrc/misc/tmux install

## Windows 10

Check out the [tmux on Windows 10 appendix section](#appendix-windows-bash).
