# Appendix: Installing tmux

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

Usage requires enabling **Developer mode** via the "For Developers" tab in the "Update & security" settings.

After you enable that, you open up "Windows Features", you can find it by searching for "Turn Windows features on or off".  Then check "Windows Subsystem for Linux (Beta)".

You may be asked to restart.

Then open up Command Prompt as you normally would (Run cli.exe). Then type

    C:\Users\tony> bash.exe

It will prompt you to agree to terms, create a user. In my build, tmux was already installed! But if it's not, type `sudo apt-get install tmux`.

![Prompt to agree to terms and install Ubuntu on Windows](images/windows_bash/.png)

For more a more detailed instruction with screenshots, check out the [Windows 10 tmux installation](#appendix-windows-bash)

[^win10bashbuild]: https://blogs.msdn.microsoft.com/commandline/2016/06/08/tmux-support-arrives-for-bash-on-ubuntu-on-windows/
