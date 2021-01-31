+++
title = "How to persist a particular layout when hotplugging a USB keyboard"
description = "How to persist a keyboard layout after USB hotplugging the keyboard"
date = 2021-01-31T12:43:00+03:00
tags = ["howto", "linux"]
draft = false
+++

I use the [dvorakp](https://www.dvorak-keyboard.com/) keyboard layout, and the other day, I got a manual
KVM switch which allows me to share a keyboard, mouse, and monitor
with another workstation. The other workstation runs Windows 10 and
uses the normal QWERTY layout. The problem I faced with this set up,
is that every time I switched back to my GNU/ Linux workstation, the
layout kept resetting to QWERTY.

To keep my keyboard layout persistent, I had to play around with udev
rules to get the targettable identity of my keyboard:

```text
sudo lsusb | grep board
```

This yielded:

```text
Bus 001 Device 003: ID 258a:0016 BY Tech Usb Gaming Keyboard
```

"258a" is the idVendor; and "0016" is the idProduct of my particular
keyboard. Now to add an udev rules in
"/etc/udev/rules.d/gaming\_keyboard.rules":

```text
ACTION=="add", ATTRS{idVendor}=="258a", ATTRS{idProduct}=="0016", ENV{XKBMODEL}="pc104", ENV{XKBLAYOUT}="us", ENV{XKBVARIANT}="dvp", ENV{XKBOPTIONS}="ctrl:nocaps"
```

After that, I had to restart udev rules by running:

```text
sudo udevadm control --reload
```

Now everytime I hotplug my USB keyboard, it will use the right
keyboard layout.
