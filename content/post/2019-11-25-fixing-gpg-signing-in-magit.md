+++
title = "Fixing gpg signing in magit"
description = "Signing commits in magit"
date = 2019-11-25T22:06:00+03:00
publishDate = 2019-11-25T00:00:00+03:00
tags = ["freebsd", "emacs"]
draft = false
+++

Today in the evening, when I wanted to sign my commits in [magit](https://magit.vc/), I came across this error:

```text
    hint: Waiting for your editor to close the file...
    Waiting for Emacs...
    error: gpg failed to sign the data
    fatal: failed to write commit object
```

This log message was not really helpful so I went ahead and tried to sign something in my terminal: `echo "test" | gpg --clearsign`. I got a more useful log:

```text
    -----BEGIN PGP SIGNED MESSAGE-----
    Hash: SHA256

    test
    gpg: signing failed: Invalid IPC response
    gpg: [stdin]: clear-sign failed: Invalid IPC response
```

I went ahead and read the gpg-agent's man agent and I realized that I had not stuck this fella in my init(in my case `.profile`) scripts:

```conf
GPG_TTY=$(tty)
export GPG_TTY
```

This fixed the error I was seeing at my terminal but then I couldn't still sign things from [magit](https://magit.vc/). Running `pkg info pinentry` showed that I was using the tty version of the program (pinentry):

```text
Options        :
        FLTK           : off
        GNOME3         : off
        GTK2           : off
        NCURSES        : off
        QT5            : off
        TTY            : on
```

The downloaded binary you get by using a `pkg install` defaults to using the tty version of pinentry so this means that any time gpg is run, it expects pinentry(the program used to input the password) to be run from the terminal. This is why adding \`GPG\_TTY=$(tty)\` above fixed the gpg error in the terminal. However, when you run emacs from a GUI, it has no access to the terminal hence the weird bug.

To make pinentry work in GNU/ Emacs, I had to remove the installed pinentry binary and compile it(from the ports collection) to use gtk. This way, when signing commits in git, I'll get a floating dialog box from which I'll input my password. This is not my ideal way of doing things, since I know that I can put the darn password within GNU/ Emacs. However, for now it suits my needs just fine :)
