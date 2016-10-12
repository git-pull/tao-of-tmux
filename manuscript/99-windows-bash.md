# Appendix: tmux on Windows 10 {#appendix-windows-bash}

As of Windows 10 build 14361 [^win10bashbuild] you can run tmux via the Linux Subsystem feature.

Usage requires enabling **Developer mode** via the "For Developers" tab in the "Update & security" settings.

After you enable that, you open up "Windows Features", you can find it by searching for "Turn Windows features on or off".  Then check "Windows Subsystem for Linux (Beta)".

You may be asked to restart.

Then open up Command Prompt as you normally would (Run cli.exe). Then type

    C:\Users\tony> bash.exe

It will prompt you to agree to terms, create a user. In my build, tmux was already installed! But if it's not, type `sudo apt-get install tmux`.

{width=50%}
![Find Turn Windows Features on or off](images/99-windows-bash/01-turn-features-onoff.jpg)
{width=50%}
![Check Windows Sybsystem for Linux (Beta)](images/99-windows-bash/02-turn-features-onoff-check.jpg)

{width=50%}
![Windows completed the requested changes. Restart](images/99-windows-bash/03-turn-features-restart.jpg)

{width=50%}
![Use Developer features](images/99-windows-bash/04-developer-mode.jpg)

{width=50%}
![Select Developer mode in Update & Security](images/99-windows-bash/05-developer-mode-check.jpg)

{width=50%}
![Installing Ubuntu from Windows Store](images/99-windows-bash/06-install-ubuntu.jpg)

{width=50%}
![Create Linux user](images/99-windows-bash/07-create-user.jpg)

{width=50%}
![In bash!](images/99-windows-bash/08-bash.jpg)

    yourusername@COMPUTERNAME-ID321FJ:/mnt/c/Users/username$ tmux

{width=50%}
![In tmux!](images/99-windows-bash/09-tmux.jpg)

[^win10bashbuild]: https://blogs.msdn.microsoft.com/commandline/2016/06/08/tmux-support-arrives-for-bash-on-ubuntu-on-windows/
