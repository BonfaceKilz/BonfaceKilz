+++
title = "Monoids and Semigroups"
description = """
  What are Monoids and Semigroups? This blog post outlines my understanding of
  what they are in the context of Haskell.
  """
date = 2018-12-23T22:19:00+03:00
tags = ["haskell", "programming"]
categories = ["programming"]
draft = false
+++

Before talking about Monoids and Semigroups, you first have to understand what
"an algebra"(in the context of Functional Programming) is. From Mathematics,
Algebra is a tool used to manipulate symbols. We really don't care what those
symbols contain; instead, what we care about is some of the laws you have to
follow. In the Functional Programming universe, an algebra is an operation and
the set it can operate on. Both a Monoid and Semigroup are algebras.

A Monoid is an operation which meets the following properties:

-   It has an _identity_. An identity function always returns the same value used
    as its argument. The id of the sum operation is 0 and the id of the product
    is 1. A Monoid has both the left and right identity.
-   It is _associative_. Associativity means that an operation can be grouped in
    any order e.g. : _(a + b) + c == a + (b + c)_
-   It is a _binary_ operator. A binary operator only takes 2 arguments.

<br />
A Semigroup is similar to the Monoid; the only difference being that it does not
have to meet the _identity_ requirement. A Monoid can be considered a subset of
the Semigroup set.

In Haskell, the Monoid is defined in its own typeclass as:

```haskell
class Monoid m where
  mempty  :: m
  mappend :: m -> m -> m

  mconcat :: [m] -> m
  mconcat = foldr mappend mempty
```

When a specific type implements the Monoid typeclass, it will automatically be
_reduce-able_. You can also be able to use the infix operator \`<>\` which behaves
in a similar way to \`mappend\`. In Haskell, the most common case of a type that
has an instance of the Monoid typeclass is the List.

```haskell
mappend [1, 2, 3] [4, 5, 6]
[1, 2, 3] <> [4, 5, 6]
[1, 2, 3] ++ [4, 5, 6]

-- They all print the same thing:
-- [1, 2, 3, 4, 5, 6]
```
