# Installation and System Requirements

If you're a sysadmin or already have tmux installed on your machine, skip this chapter, as it's intended for absolute beginners.

## System Requirements

tmux is designed to run on Linux, BSD and OS X.

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

Yes, as of Windows 10 build 14361 [^win10bashbuild] you can run tmux via the Linux Subsystem feature.

[^win10bashbuild]: https://blogs.msdn.microsoft.com/commandline/2016/06/08/tmux-support-arrives-for-bash-on-ubuntu-on-windows/
