+++
title = "Comparing floating point numbers"
description = "How to compare floating point numbers"
date = 2021-10-21T21:27:00+03:00
publishDate = 2021-10-21T00:00:00+03:00
tags = ["programming"]
draft = false
+++

Floating point numbers are a chore to work with. And how computers
work with them can be more complex. As an example take this example in
Python:

```python
print(0.3 * 3 + 0.1)
```

We get:

```text
0.9999999999999999
```

This is caused by rounding errors during calculations. Instead of
getting a simple "1", we get: "0.9999999999999999". Thus, when
programming, it's dangerous to directly compare floating numbers, like
say:

```python
print((0.3 * 3 + 0.1) == 1)
```

Which outputs:

```text
False
```

Instead, a more plausible way of checking for equality with 2 floating
point numbers would be to assume that the 2 floating point numbers are
equal if the difference between them is less than some number, like
say ϵ.

```python
ϵ = 1e-9
print(abs((0.3 * 3 + 0.1) - 1) < ϵ)
```

which now correctly outputs

```text
True
```

Also, a bit off-topic, but it's worth pointing out that symbols like
θ, β, ζ etc are valid names for variables.