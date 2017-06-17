+++
categories = ["sicp", "Emacs"]
date = "2017-06-17T22:28:57+03:00"
description = "Reading SICP in emacs"
tags = ["sicp", "Emacs"]
title = "How to read SICP in Emacs"

+++

Since MIT Press distributed the book Structure and Interpretation of Computer Programs(SICP) in HTML, some very nice people in the interwebs converted the book into texinfo format. This means that you can now view the book in Emacs woOt!

To be able to view the book in Emacs, first clone this github [repository](https://github.com/webframp/sicp-info ). To convert the `.texi` format, simply run:

```
makeinfo --no-split sicp.texi -o sicp.info
```

You however don't need to do this since the file: `sicp.info` is already present in your cloned repository. You can now view the book in emacs using `INFO-MODE`. Happy scheming :)
