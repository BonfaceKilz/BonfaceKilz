+++
title = "Fixing a Display Bug in Protégé"
description = """
  Protege does not start---blank window in
  EXWM (Running on Arch Linux with GNU Guix as the
  primary package manager)
  """
date = 2022-06-07T13:59:00+03:00

draft = false

[taxonomies]
tags = ["howto"]
+++

Your dear author is learning how to create an
[ontology](http://www-ksl.stanford.edu/kst/what-is-an-ontology.html) for a sub-set of [GeneNetwork](https://genenetwork.org) data. To
make his work easier, he searched for a
GPL-compliant tool that can: 1) Generate a graph;
and 2) export the ontology to different
formats. This adventurous journey led him to
stumble upon: [Protégé](https://github.com/protegeproject/protege). This desktop application
tool hasn't been packaged yet in GNU Guix
upstream---something to do with how notoriously
difficult it is to package Java projects---but is
however provided in the official Arch Linux
repositories.

Installing the tool in Arch Linux was easy:

```txt
sudo pacman -S protege
```

After installation, your beloved author ran into
an annoying issue where the program started off
with a blank window:

![Protege Blank Screen](/img/2022-06-07-134547_1920x1080_scrot.png)

Luckily for your author, this is a well known
[issue](https://github.com/protegeproject/protege/issues/641) with a straight-forward solution; simply run
"protege" with some special flag like so:

```txt
_JAVA_AWT_WM_NONREPARENTING=1 protege
```

Should you face a similar problem, you can stick
this flag in one of your start-up dotfiles.

Your author will be reporting on his experience
with creating ontologies; hopefully relevant
material to you!
