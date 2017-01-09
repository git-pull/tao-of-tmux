{backmatter}

# Appendix: Installing tmux {#appendix-installation}

## macOS / OS X

### brew

{language=shell, line-numbers=off}
    $ brew install tmux

### macports

{language=shell, line-numbers=off}
    $ sudo port install tmux

### fink

{language=shell, line-numbers=off}
    $ fink install tmux

## Linux

### Ubuntu / Mint / Debian, etc.

{language=shell, line-numbers=off}
    $ sudo apt-get install tmux

### CentOS / Fedora / Redhat, etc.

{language=shell, line-numbers=off}
    $ sudo yum install tmux

### Arch Linux (pacman)

{language=shell, line-numbers=off}
    $ sudo pacman -S tmux 

### Gentoo (portage)

{language=shell, line-numbers=off}
    $ sudo emerge --ask app-misc/tmux

## BSD

### FreeBSD

#### pkg(1)

{line-numbers=off}
    # pkg install tmux

#### pkg_add(1)

{line-numbers=off}
    # pkg_add -r tmux

### OpenBSD

As of OpenBSD 4.6, [tmux is part of the base system](https://www.openbsd.org/46.html).

If you are using an earlier version:

{line-numbers=off}
    # pkg_add tmux

### NetBSD

{language=shell, line-numbers=off}
    $ make -C /usr/pkgsrc/misc/tmux install

## Windows 10

Check out the [tmux on Windows 10 appendix section](#appendix-windows-bash).
