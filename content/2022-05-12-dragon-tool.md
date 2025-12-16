+++
title = "Terminal/Emacs Driven Drag and Drop"
description = "Using drag-and-drop from the Terminal/Emacs"
date = 2022-05-12T17:39:00+03:00
tags = ["terminal", "productivity", "emacs"]
draft = false
+++

File Managers, and many web/desktop
applications---such as WhatsApp, DropBox, GDrive
etc.---have a drag and drop feature: You click on
some UI element, say a folder/file and drag it to
a dedicated spot in the app. For terminal users,
this can be an annoying feature, particularly if
you hate using UIs. To work around that, enter:
[dragon](https://github.com/mwh/dragon); a lightweight drag-and-drop source for
X. Using dragon you can easily run it against any
file from your terminal, and it will pop up a
window with just that file in. From this window,
you can drag your file to a target. This is as
simple as:

```txt
dragon myfile
```

Note that the above command will not close the window once it completes. To close the window once you are done:

```txt
dragon myfile --and-exit
```

Personally, I use "dired-dragon", an emacs wrapper
around this tool. My configs are:

```el
(use-package dired-dragon
  :straight (:host github
             :repo "jeetelongname/dired-dragon")
  :after dired

  ;; if you use use-package for bindings
  :bind (:map dired-mode-map
         ("C-d d" . dired-dragon)
         ("C-d s" . dired-dragon-stay)
         ("C-d i" . dired-dragon-individual)))
```

[dragon](https://github.com/mwh/dragon) is a useful tool that doesn't get in my
way. I'd strongly recommend it; if not for it's
utility, then for it's novelty and simplicity.
