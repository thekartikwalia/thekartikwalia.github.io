---
title: "Modulus Operator"
date: 2024-10-17 8:05:00 +0530
categories: [DSA, Modular Arithmetic]
tags: [modulo, arithmetic, stl]
math: true
---

## Basics of Modulus Operator 
The `a % b` gives remainder when a is divided by b.

If `a % b = c`, then it can also be written as $a \, \equiv \, c \,\, mod (b)$, which says $a$ will give remainder of $c$ when divided by $b$. Eg: `7 % 3 = 1` can also be written as $7 \, \equiv \, 1 \,\, mod (3)$

__NOTE__ : Modulo `%` has more precedence than `+`, that's why `5 + 2 % 3 = 7`

## The Behavior of Modulus with Negative Integers
The expression `-4 % 3` gives different results in different languages:
- In python, it gives output as 2 
- In C++, it gives output as -1

Ideally, if we look according to periodicity, then it should have been 2 only as we always consider range of expression `a % b` from 0 to (b-1). 

But C++ treats modulus in a different way, i.e. C++ treats `-a % b` as `-(a % b)`
C++ is not so good at handling negative things, it  treats even `((-a) % (-b))` as `-(a % b)` because C++ treats part after modulo as positive always (remainder with negative number isn't valid)
Thatswhy, we don't deal much with negative numbers in modulo part.