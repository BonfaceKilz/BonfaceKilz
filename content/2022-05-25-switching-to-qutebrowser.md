+++
title = "Switching to QuteBrowser"
description = "Tidbits on my experience switching to QuteBrowser"
date = 2022-05-25T16:02:00+03:00

draft = false

[taxonomies]
tags = ["technology"]
+++

Recently, I switched from Firefox to [qutebrowser](https://www.qutebrowser.org/)
for my daily web-surfing needs. This move has been
mainly driven by the need to adopt a keyboard
driven minimal browser that I can also use during
web development. Prior to this switch, I had tried
[Nyxt](https://nyxt.atlas.engineer/), another keyboard driven browser. My
experience with Nyxt has mostly been positive, but
the deal-breaker for me was un-reproducible random
crashes that made the browser-experience
inconvenient/uncomfortable.

That said, using qutebrowser has not always been
smooth sailing: At the onset, I noticed that in
some web pages---in my qutebrowser install---text
was not visible. Here's an example of browsing
GitHub:

![Example browsing GitHub in qutebrowser---bug with QtWebEngine](/img/blank-qutebrowser-1.png)

As outlined [here](https://github.com/qutebrowser/qutebrowser/issues/6942), this was an [issue](https://bugs.chromium.org/p/chromium/issues/detail?id=1164975) with
Chromium. Unfortunately for me, at the time of
this writing, the [upstream fix](https://codereview.qt-project.org/c/qt/qtwebengine-chromium/+/374232) in QtWebEngine that
addresses this issue has not been applied in GNU
Guix upstream. To fix this issue, I had to add
this to my `~/.config/qutebrowser/config.py`:

```txt
c.qt.args = ['disable-seccomp-filter-sandbox']
```

That said, after working around the aforementioned
bug with QtWebEngine, my browsing experience with
qutebrowser has been _suave_: I'm always discovering
new hacks for doing new things with a keyboard
that I thought difficult. Needless to say, this
has been an exciting experience and besides GNU
Emacs, qutebrowser is growing to be one of those
tools that keeps "fanning the flame" of: _the joy
of computing_.
