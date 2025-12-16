+++
title = "How To Install WinBugs in ArchLinux using Wine"
description = "How to use Wine to install WinBugs"
date = 2022-12-06T13:17:00+03:00
publishDate = 2022-12-06T00:00:00+03:00

draft = false

[taxonomies]
tags = ["linux", "how-to"]
+++

WinBugs is a statistical software tool that's built to explicitly run on Windows.  As such, to be able to run it on a \*Nix system, you have to run it under a compability layer that's able to run Microsoft Windows applications.  In this case, that layer is WINE.  This post outlines how to install WINE, and finally, WinBugs


## Installing Wine {#installing-wine}

To install WINE in ArchLinux, first enable the [multilib](https://wiki.archlinux.org/title/Multilib) repository and thereafter install WINE by running:

```txt
sudo pacman -S wine
```

Next install all the necessary Windows fonts:

```txt
yay -S ttf-ms-win1{0,1}-auto
```

Since I have a high-dpi screen, I had to to adjust the font-size in wine by typing, `wine regedit`, then navigating to "HKEY_CURRENT_CONFIG" &gt; "Software" &gt; "Fonts" and adjusting "LogPixels" to "120."

To be able to run windows programs directly as if you had typed: `wine ./myprogram.exe`:

```txt
sudo systemctl start systemd-binfmt.service
```


## Installing WinBugs {#installing-winbugs}

To install WinBugs:

```sh
# Download the winbugs package.  I usually install my user software in ~/opt.
cd ~/opt/
wget https://www.mrc-bsu.cam.ac.uk/wp-content/uploads/2018/11/winbugs143_unrestricted.zip

# unzip the package and make winbugs executable
unzip winbugs143_unrestricted.zip && cd winbugs14_full_patched/WinBUGS14
chmod +x ~/opt/WinBUGS14/WinBUGS14.exe


# Make winbugs executable!
'#!/usr/bin/bash\n\n$HOME/opt/WinBUGS14/WinBUGS14.exe' >
$HOME/bin/,winbugs chmod +x $HOME/bin/,winbugs
```


### References {#references}

-   [[ArchWiki] Wine](https://wiki.archlinux.org/title/Wine)
-   [[ArchWiki] Multilib](https://wiki.archlinux.org/title/Official_repositories#multilib)
-   [The Bugs Project](https://www.mrc-bsu.cam.ac.uk/software/bugs/the-bugs-project-winbugs/)
-   [Bugs installing in Linux](https://www.atsanchez.es/tutorials/winbugs.html) (Do not install WinBugs with Sudo Permissions!)
