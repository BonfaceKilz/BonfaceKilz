+++
title = "Haskell- Elegances in Functional Programming"
description = "Short musings on FP with Haskell"
tags = ["programming", "functional programming"]
categories = ["programming", "functional programming"]
date = "2018-08-07"
+++

In this past few months, I've delved deep into Functional Programming(FP). FP is a functional paradigm whereby functions are the basic building blocks of various abstractions. In FP, we build more abstractions by composing small functions together. One great motivation for this is my desire build robust, terse and correct programs that are easy to test. At work, I've been tasked with maintaining and adding new features to a system that runs on unsupported [php] framework; which barely has any code coverage. My frustrations working in such an environment have greatly inspired me to look for ways to hone my deving craft- hence FP.

As an example of terseness, I'll write a small program that sums the first *n* fibonacci numbers. A fibonacci number consists of the sum of the previous number before it i.e *fib(n) = fib(n-1) + fib(n-2)*. The initial conditions would be that: *fib(0) = 1* and *fib(1) = 1*. From this definition, it can be seen that the solution is recursive. In Python, a naive implementation of this would be using tree recursion as follows:

```
def fib(n):
	if n == 0:
		return 0
	if n == 1:
		return 1
	return fib(n-1) + fib(n-2)
	
def sumFib(n):
	sum = sum([fib(x) | x for x in range(n)])
	return sum
```
The above alogorithm is quite slow because it uses tree recursion which takes up *O(n)* time to execute. A more efficient way to do this would be to use iterative recursion as follows:

```
def fibIter(n):
	a, b = 0, 1
	for i in range(0, n):
		a, b = b, a+b
	return a

def sumFib(n):
	sum = sum ([fibIter(x) | x for x in range(n)])
```

A more efficient way of writing the above would be:

```
def fibSumIter(n):
	a, b = 0,1
	result = 0
	for i in range(0, n):
		result = result + a
		a, b = b, a + b
	return result
```

In Haskell we could solve the recursion problem by first generating an infinite list of fibonacci numbers. We do not have to worry about this because, we have lazy evaluation which is built into the language itself. This means we only evaluate something, in the case of infinite lists, when it is required. We generate this list using Haskell's list comprehension as follows:

```
fibs = [0, 1] ++ [fibs !! (i-1) + fibs !! (i-2) | i <- [2..]]
```

If we want to find the sum of the first *n* fibonacci numbers, we would simply apply a *sum* function over the first *n* numbers as follows:

```
fibSum n = sum $ take n fibs
```

Personally, I find this shorter, and more terse compared to the Python version. One disadvantage of this though is that the Haskell version appears to be more obfuscated than the Python version. Well, that's it for this tiny Haskell musing. If you want to find out more about FP in general, join this [mailing list](https://groups.google.com/forum/#!forum/nairobi-functional-programming-community).
