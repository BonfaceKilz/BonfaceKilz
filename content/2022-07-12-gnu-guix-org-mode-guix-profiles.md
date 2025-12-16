+++
title = "GNU Guix + Guix Profiles + Org Mode = Python In Org!"
description = "How to hook up Python+PYTHONPATH in org-mode"
date = 2022-07-12T20:15:00+03:00
publishDate = 2022-07-12T00:00:00+03:00

draft = false

[taxonomies]
tags = ["how-to", "Emacs"]
+++

Have you ever wondered how you could point to any version of Python---with the correct PYTHONPATH set correctly---in your org-mode file?
Today, I just successfully hacked on one such way.
Before we go any further, let's look at org-src blocks (wrt Python) basics.
A python org-mode section looks like this:

```txt
#+begin_src python :results output
[...]
#+end_src
```

With the above source block, you can optionally choose the Python binary (with the ":python" header) you want to run:

```txt
#+begin_src python :results output :python /path/to/python/binary
[...]
#+end_src
```

Now here is where things get interesting.
Since you can point org-mode to a binary of your choice, you can also also ideally point it to an executable script that will run your Python interpreter whilst setting the relevant paths.
With the knowledge that you have these powers, you could use Guix to install your python packages in a given profile.
Here's an example of installing `python`, `python-scipy`, and `python-numpy` to the "python-science" profile located in "~/opt":

```txt
guix shell python python-scipy python-numpy -p ~/opt/python-science
```

Now we can point the python binary and "PYTHONPATH" to a script that sets these variables.
In my case, I have this in my "~/bin/,python-science":

```sh
#!/bin/sh

env PYTHONPATH="$HOME/opt/python-science/lib/python3.9/site-packages"\
    $HOME/opt/python-science/bin/python3
```

Now, we can install isolated python binaries with their "PYTHONPATH" and use that within org-mode; and GNU Guix is that "glue" that helps us out.
Of course, although it remains unexplored, you can apply the same with virtual environments.
Now, the end org-mode src-block would look something like this;

```txt
#+begin_src python :results output :python ~/bin/,python-science
import scipy
#+end_src
```
