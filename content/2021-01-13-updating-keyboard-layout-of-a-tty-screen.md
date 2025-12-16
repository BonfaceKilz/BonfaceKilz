+++
title = "Updating The Keyboard Layout of a TTY screen"
description = "How to update the keyboard layout of a TTY screen"
date = 2022-01-13T12:58:00+03:00
tags = ["linux"]
draft = false
+++

I normally use the [dvorak programmer keyboard layout](https://www.kaufmann.no/roland/dvorak/); but that is only
configured for my xorg sessions.  In my `.xinitrc` file, I have the following snip:

```txt
setxkbmap -layout us -variant dvp -option ctrl:nocaps
```

Outside Xorg sessions, the layout is the normal QWERTY set-up which I don't use.  Today, I got around to setting up `dvorak-programmer` as my layout of choice for my tty screens.  To do that in a persistent way[0], run the following command with admin privileges:

```txt
# localectl set-keymap --no-convert dvorak-programmer
```

Now when you `cat /etc/vconsole.conf`, you can see:

```txt
KEYMAP=dvorak-programmer
```

And voila!  There you have it: a tty with `dvorak-programmer`.

[0] Linux console/Keyboard configuration. Jan 13, 2021. URL:
<https://wiki.archlinux.org/title/Linux%5Fconsole/Keyboard%5Fconfiguration>