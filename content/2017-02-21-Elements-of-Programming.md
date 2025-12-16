+++
date = "2017-02-21T18:20:44+03:00"
title = "Elements of Programming"
categories = ["SICP"]
tags = [
    "fundamentals", 
    "programming", 
    "sicp",
    ]
description = "A summary of SICP section 1.1"

+++

The three things that a powerful computer language should have is:  
1. **Primitive expresssions**: The simplest entities the language is concerned with.  
2. **Means of combination**: How compound components can be made from smaller ones.  
3. **Means of abstraction**: Creating new units that can be used in more complex structures.  
In this text, I am using MIT-Scheme[a lisp variant] which is in-built in emacs. Scheme has a small set of primitives such as: +, /, * and so on.You can use these primitives to form primitive expressions like so:  
```
(+ 74 23)
```  
You can also use the key word **define** to form new abstractions. If you come from other programming languages, it can help to think of **define** as a way to create variables or make procedures[functions]. Here's an example:  
```
(define (cube x) (* x x x))
```  
The general form of a procedure definition is:  
```
(define (<name> <formal parameters>) <body>)
```  
In scheme, there are other primitive expressions which help us to make conditional statements. They are **if** and **cond**. Here's an example of their use:  
```
(define (abs x)
	(cond ((< x 0) (- x))
		((= x 0) 0)
		((> x 0) x)))
```  
This function can also be re-written using **if** as follows:  
```
(define (abs x)
	(if (< x 0) (- x)
		x))
```  
Here's a summary of how they work:  
```
(define (<name> <formal parameters>)
	(cond ((<condition1>)) (<execute if condition1 is met)
	(cond ((<condition2>)) (<execute if condition2 is met)
	)))
(define (<name> <formal parameters>)
	(if (condition1) (<execute if condition1 is met)
		<else execute this section>))
```  
## The substitution model ##
An interpreter needs a way to evaluate a combination whose operator names a compound procedure. This is where the substitution model comes in. It helps us think about procedure application[and not to provide the inner workings of the interpreter]. You can go further and classify this model into 2 types: **Applicative Order** and **Normal Order**.  

### Applicative Order ###
These steps are followed:  
1. Evaluate the body of the compound procedure  
2. Evaluate the corresponding arguments  
Let's take an example here. Assume a function **f**, **sum-of-squares** and **square** are defined as:  
```
(define (f x)(sum-of-squares (+ x 1) (* x 2)) )
(define (sum-of-squares x y) (+ (square x) (square y)))
(define (square x) (* x x))  
```
The compound procedure `(f 5)` is evaluated as follows:  
```
(sum-of-squares (+ 5 1) (* 5 2))
(+ (square 6) (square 10))
(+ (* 6 6) (* 10 10))
(+ 36  100)
136
```  
You can think of the _applicative order_ as **Evaluate the arguments adn then apply**   

### Normal Order ###
In this model, the operands are not evaluated until the substitution process evaluates all the procedure bodies to the primitive operations. In other words, _Full expand then reduce_ . Here's an example using `(f 5)` which was defined above:  
```
(f 5)
(sum-of-squares (+ 5 1) (* 5 2))
(+ (square (+ 5 1)) (square (* 5 2)))
(+ (* (+ 5 1) (+ 5 1)) (* (* 5 2) (* 5 2)))
(+ (* 6 6) (* 10 10))
(+ 36 100)
```
