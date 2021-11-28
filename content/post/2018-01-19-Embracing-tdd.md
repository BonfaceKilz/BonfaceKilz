+++
title= "Embracing TDD- A Sermon"
description= "A short sermon on TDD from a concerned Emacs Evangelist"
tags= [
    "agile",
    "software",
    "fundamentals",
]
categories= [
    "software",
    "fundamentals",
]
date= "2018-01-19T15:50:36+03:00"

+++

It's been a long while since I blogged. I've been busy with tonnes of stuff. For one, I commenced work some time last month as a systems developer for Clinton Health Access Initiative(CHAI). I've been juggling work, and other side projects, with my final year of engineering school, and this has been one tough nut to crack. This is however not a post about time management or schedules, it's one about testing your projects.

TDD(Test Driven Development) is one of those things alot of people talk about but rarely do in practice. People fear doing it in practice because they think that it consumes alot of time and increases development costs. This is far from the truth. I hope this post shows you otherwise.

To prove my point, I will use a simplified model, dividing two numbers, to prove my point.

Alot of people would dive right in and write a function to do the definition like so:

```
function divide(a, b):
    return a/ b;
```

Presto, complete! Simple right?

Let's try out a TDD approach to do this. We first write a simple test test our fictional function. This function should fail. Trying to make a failing funtion, in our case, would make us think of things that aren't really obvious, like division by zero.

```
function testDivide():
    assert(10, 5).toBe(2);
    assert(10, 0).toBeEqualTo('error');
```

We would then write a failing function:

```
function Divide(a, b):
    return a/ b;
```

If we ran our tests against this, we would get a failing test. Time to fix the failing test by refactoring the `Divide` function:

```
function Divide(a, b):
    if(b == 0):
        return 'error';
    return a/ b;
```

And voila, we've fixed a potential bug before it even occured. Writing our tests also makes us think about other things. If our language is strongly typed, we would have to be careful about casting and all that other fancy stuff that comes with a strongly typed language. Writing this test will also give us confidence going forwards with our codebase. *Confidence is important* which has a strong foundation is really important in software.

Using TDD in your work also forces you to write clearer code. Code that is hard to test tends to be unclear.

Functions that are easy to test do one thing well, and do that one thing well. This makes it easier to read code and hence makes maintenace work easier.
