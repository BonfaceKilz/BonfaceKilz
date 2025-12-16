+++
title = "Inserting Control Characters in GNU Emacs' Minibuffer"
description = """
  This post outlines how to insert control
  characters in GNU Emacs' minibuffer
  """
date = 2022-05-24T20:56:00+03:00
publishDate = 2022-05-24T00:00:00+03:00
tags = ["emacs"]
draft = false
+++

Most commands in GNU Emacs are entered in a
special buffer called the _minibuffer_. Usually, it
appears at the bottom of a frame (Read and learn
more about the minibuffer [here](https://www.emacswiki.org/emacs/MiniBuffer) and [here](https://www.gnu.org/software/emacs/manual/html_node/elisp/Intro-to-Minibuffers.html)).

Sometimes, when using the minibuffer, you may want
to enter [control characters](https://en.wikipedia.org/wiki/Control_character). An example of a
use-case where you may want to use control
characters is when you have configured your editor
to visually see [linefeed](https://en.wiktionary.org/wiki/line_feed) characters---"^M"---and
you want to use a facility like GNU Emacs' [isearch](https://www.gnu.org/software/emacs/manual/html_node/emacs/Basic-Isearch.html)
to manually replace that character with something
else. To do so, use the in-built function:
`(quoted-insert ARG)` which is normally bound to
"C-q". This reads the next input character and
inserts it---a useful thing when inserting control
characters. Here's an example how to insert a
newline control sequence:

```txt
C-q C-j
```

For what's it worth, you can use octal digits to
specify a character code too!  Note that while
inputting characters, non-digit characters
terminate the sequence.

In summary, the important thing to note is that
you can use `quoted-insert` (usually bound to "C-q")
to insert any control character anywhere you want,
and that includes the minibuffer.
