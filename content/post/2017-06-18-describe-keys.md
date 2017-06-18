+++
categories = ["Emacs"]
date = "2017-06-18T19:31:56+03:00"
description = "The describe system in GNU Emacs"
tags = ["emacs", "productivity"]
title = "Useful Describe Keys in Emacs"

+++

> What captures the beauty of Emac's self-documenting nature is
> the describe system of commands. If you know what you're looking
> for, then describe will explain what it is
>
> -- Mastering Emacs

Many a times in GNU Emacs you get stuck trying to figure out what some key strokes do. Sometimes, you get someone's config(emacs.d/init.el) file and you wonder what those goddamn minor/ major modes do. Well, Emacs inbuilt describe system makes work easier as it helps you, the user, know what stuff does. Below, I list some of the most important key bindings in GNU Emacs which you'll probably (maybe) use in your daily interaction with GNU Emacs:

1. `C-h m`/ `M-x describe-mode`: Running this command will display the major mode and any minor modes enabled in the current buffer along with any key-bindings introduced by said modes
2. `C-h k`/ `M-x describe-key`: Describe key-binding.
3. `C-h v`/ `M-x describe-variable`: Describes a variable.
4. `C-h f`/ `M-x describe-function`: Describes a function and any other relevant details pertaining that function. Here's an example of what is displayed by running `M-x describe-function` followed by `list-packages`:

```
list-packages is an interactive autoloaded compiled Lisp function in
‘package.el’.

(list-packages &optional NO-FETCH)

:around advice: fullframe-command-on-advice

Display a list of packages.
This first fetches the updated list of packages before
displaying, unless a prefix argument NO-FETCH is specified.
The list is displayed in a buffer named ‘*Packages*’.

[back]
```

**References:**
<br/>1. *Mastering Emacs* by Mickey Petersen
