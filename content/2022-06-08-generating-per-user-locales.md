+++
title = "Generating Per-User Locales"
description = """
  How to generate per-user locales to fix jumbled
  terminal characters
  """
date = 2022-06-08T11:47:00+03:00

draft = false

[taxonomies]
tags = ["terminal", "linux", "guix"]
+++

For a while now---in the terminal(kitty)---your
author has been putting up with: characters in the
command line displayed with an offset; and more
annoyingly, characters being randomly jumbled up
during auto-completions. After some fiddling, the
root cause was un-earthed: your author's prompt
contains non-ASCII characters, and zsh and his
terminal have a different idea of how wide they
are. This is because there is a mismatch between
the encoding in the terminal and the one declared
by the shell; and these 2 encodings result in
different widths for certain byte sequences. This
happened for your author since he has 2 different
encodings: one declared by my base-system: Arch
Linux; and the other defined by GNU Guix.

To remedy this conundrum, your author resorted to
generating his own locales and setting them in
"$HOME/.zshenv" as follows:

```zsh
mkdir -p $HOME/.locale
I18NPATH=$HOME/.guix-profiles/share/i18n/locales localedef -f UTF-8 -i en_US $HOME/.locale/en_US.UTF-8
LOCPATH=$HOME/.locale LC_ALL=en_US.UTF-8 date
echo "export LOCPATH=\$HOME/.locale" >> $HOME/.zshenv
echo "export LANG=en_US.UTF-8" >> $HOME/.zshenv
```

This is a common issue that faces many people
running GNU Guix in a foreign distro; and as such
your author hopes that this article is relevant to
people with a similar issue. To read more on
alternative reasons/solutions, check out this
[StackOverflow answer](https://unix.stackexchange.com/a/90876).
