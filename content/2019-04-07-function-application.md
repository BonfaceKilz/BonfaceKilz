+++
title = "Functional Application (Notes)"
description = "Some short notes on function application in Haskell"
date = 2019-04-07T00:00:00+03:00
tags = ["haskell", "functional-programming"]
draft = false
+++

In Haskell, functional application associates to the left in expressions and also has the highest binding power. What does this mean?

Well, this is what it means:

If you have a function: `f x y z` left associativity implies: `(((f x) y) z)`. The highest binding power means that `f x + y` will be parsed as `(f x) + y`.

Another counter-intuitive example to demonstrate the 'highest binding power of left associativity' is: `f sin 3`. This will not pass the result of `sin 3` to `f`. Instead, it will pass the `sin` and `3` as arguments to `f`.
