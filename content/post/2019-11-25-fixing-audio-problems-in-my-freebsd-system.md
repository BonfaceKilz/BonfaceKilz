+++
title = "Fixing Audio Problems in my freeBSD system"
description = "How I fixed audio problems in FireFox in my FreeBSD system"
date = 2019-11-25T16:55:00+03:00
draft = false
+++

> **Each new user of a system uncovers a new class of bugs.**
>
> -- Brian Kernighan

Ever since I rejected my previous job's contract offer(more on that in another post), I've been spending a lot of time in my FreeBSD system(_FreeBSD 12.0-RELEASE-p12_) which I'm proud of. It runs [exwm](https://github.com/ch11ng/exwm) and uses [xdm](https://www.freebsd.org/doc/handbook/x-xdm.html) as the [display manager](https://wiki.archlinux.org/index.php/Display%5Fmanager).

Whilst in the BSD universe, I encountered a bunch of problems, biggest among them is playing audio in my system. Initially, I thought it was a driver problem; perhaps I did not set up some audio driver properly. This however did not make any sense because I followed the [sound card setup](https://www.freebsd.org/doc/handbook/sound-setup.html) instructions from the FreeBSD kernel faithfully. Also, I could see that my sound card drivers were properly loaded by running: `# cat /dev/sndstat` whose output was:

```text
pcm0: <Intel Haswell (HDMI/DP 8ch)> (play)
pcm1: <Intel Haswell (HDMI/DP 8ch)> (play)
pcm2: <Intel Haswell (HDMI/DP 8ch)> (play)
pcm3: <Realtek ALC292 (Analog 2.0+HP/2.0)> (play/rec) default
pcm4: <Realtek ALC292 (Analog)> (play/rec)
No devices installed from userspace.
```

What to do? The first thing I did was to reproduce the problem. I like doing this because it prevents me from doing unnecessary guesswork. I tried to find out if this problem affected apps only(in this case firefox v70) or if it was a system wide thing. The quickest way to do this was to play a normal mp4 video, both from the browser and the system using [VLC](https://www.videolan.org/vlc/download-freebsd.html) and to compare the sound quality.

The results were encouraging: The audio was only broken in Firefox(FF). To debug the firefox audio problem, I checked the post-installation notes about audio from the maintainers by running: `pkg info -xD firefox`. Fortunately, there was something in there that was useful:

```text
## Audio backend

To select non-default audio backend open `about:config` page and
create `media.cubeb.backend` preference. Supported values are: `alsa`,
`jack`, `pulse`, `pulse-rust`, `sndio`. Currently used backend can be
inspected on `about:support` page.
```

Turns out that FF discontinued ALSA somewhere along their release chain. On FreeBSD, you have to set a different audio backend to use. I followed the above steps, and reconfigured my FF to use `pulse` as my preferred audio backend and this fixed all my audio woes :)
