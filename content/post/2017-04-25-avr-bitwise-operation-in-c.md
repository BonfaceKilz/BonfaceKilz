+++
categories = ["electronics"]
date = "2017-04-25T11:07:58+03:00"
description = "Some fundamental basics in AVR programming. Working with bits."
tags = ["avr", "electronics"]
title = "Bitwise Operations in AVR"

+++
I've realised I've become abit rusty when it comes to microcontroller stuff. I've decided to tinker with things and I thought it'd be cool write about C bit manipulation since I use it alot when programming microcontrollers. Here's an example of a set of macros that uses bit manipulation:

```
#define output_low(port, pin) port &= ~(1<<pin)
#define output_hig(port, pin) port |= (1<<pin)
#define set_input(portdir, pin) portdir &= ~(1<<pin)
#define set_output(portdir, pin) portdir |= (1<<pin)
```
Here are the bit operators and their truth tables:

(1) __|__ : bit OR

 Input A | Input B | Output
---------|---------|-------
       0 |       0 |      0
       0 |       1 |      1
       1 |       0 |      1
       1 |       1 |      1

(2) __&__ : bit AND

| Input A | Input B | Output |
|---------|---------|--------|
|       0 |       0 |      0 |
|       0 |       1 |      0 |
|       1 |       0 |      0 |
|       1 |       1 |      1 |

(3)__^__ : bit XOR

| Input A | Input B | Output |
|---------|---------|--------|
|       0 |       0 |      0 |
|       0 |       1 |      1 |
|       1 |       0 |      1 |
|       1 |       1 |      0 |

(4) __~__ : bit NOT

| Input | Output |
|-------|--------|
|     1 |      0 |
|     0 |      1 |

The other bitwise operator commonly used is the `<<` or shift-left operator. Let's look at some use cases for the bitwise operators.

Let's say I to set I had an output pin called LED6 initialised to. To set(make the bit a 1) and then store the result back into LED6, I would do:

```
LED6 |= 0x01;
```

To clear(set the bit to 0) in LED6, I would do the following:

```
LED6 &= ~0x01;
```

Another important concept is that of shifting bits. Before we dive into this, let's talk about Bit MASKS. A bit mask is a binary number where the desired bits are one and the remaining are 0. We can use the `<<` operator to build bit masks. Here are examples:

```
// To build a bit mask with with bit 1 set:
(0x01 << 1)

// To build a bit mask with bit 5 set:
(0x01 << 5)

// To build a bit mask with bit 1 and 5 set:
(0x01 << 1 | 0x01 << 5)
```

### Useful Reads
[1]. [C Bit manipulation(aka "programming 101")](http://www.avrfreaks.net/forum/tut-c-bit-manipulation-aka-programming-101?page=all)

[2]. [AVR Bitwise operations in C](http://efundies.com/avr-bitwise-operations-in-c/ ) 

