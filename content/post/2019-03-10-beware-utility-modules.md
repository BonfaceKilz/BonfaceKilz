+++
title = "Beware utility modules/ classes"
description = """
  Utility modules(or classes) can be a potential sign of code smell. This
  article describes why.
  """
date = 2019-03-10T21:13:00+03:00
tags = ["programming", "software"]
categories = ["programming"]
draft = false
+++

> **We build our computer systems the way we build our cities;**
> **over time, without a plan, on top of ruins**
>
> -- Ellen Ullman

If you have been writing software for a while, there's a high likelihood that
you have encountered modules or classes that contain utility functions. Utility/
helper functions, as the name suggests, contain useful functions used elsewhere
in a project. Here's an example: [util.py](https://github.com/kennethreitz/requests/blob/master/requests/utils.py)

Utility modules grow out of a need to abstract away a set of functions used
several times in different places within a project. They form some sort of
Swiss Army knife in the project. At the onset of a project, this is not bad
because normally, the priority is to get things working.

The problem with utility modules is that they have a nasty tendency to be hard
to maintain. As a project grows, utility modules become a dumping ground for
functions that do not fit well in other modules. Also, as a team grows, people
can misuse utility functions to dump some 'quick-fixy' functions that they need
somewhere else, and this can lead to code duplication. Also, as they grow,
utility modules can be really hard to read because they contain a bunch of
unrelated functions.

Avoid utility modules or keep them as slim as possible. They should flagged
during code reviews. They are a sign that you should rethink how you
encapsulate your functions in a module(or a class).
