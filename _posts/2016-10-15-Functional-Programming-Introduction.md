---
layout: post
title: Functional Programming Introduction
---

The Functional Programming is not a new concept created all of sudden and the concept itself is even older than the OOP.
There are 3 typical environmental changes that motivates the FP.

✓ People starts to care about a concurrency to maximize a performance.
✓ People got tired of having so many bugs.
✓ Data is getting important and looking for a way to handle more efficiently.

## Function
Every programmers write a function. But the FP is based on the rules of mathematical function.
Consider 

> y = sin(x)

```sin(0) == 0```, this holds always true. There is no possibility that we would get 1 in this case. 
We say this function is **pure** and give us **referential transparency**.

The function is treated as a value, for example, ```tan(x) = sin(x) / cos(x)``` and when a function takes other functions as arguments or returns a function, it is called a **higher-order function**.
The higher-order function is sometimes called **combinator**. As its name stated, higher-order function glues functions, just like a Lego blocks, and it usually makes the code consent. 

## Immutable Variable
Unlikely the Procedural-oriented programming, In FP, variables are actually not really vary-able.
To change a value, Scala copies and creates new value instead of change one.
Performance? The book says Scala is highly optimized for object copying and provides number of ways to enhance the performance including ```lazy evaluation```
Some FP languages like, Haskell, taking a lazy evaluation as a default but scala is taking ```eager evaluation``` while providing a way to be ```lazy```.



## Closure

```scala211
(1 to 10) filter (_ % 2 == 0) map (_ * 2) reduce (_ * _)
```

A function literal with no free variables is called a closed term.
Any function literal with free variables, such as (x: Int) => x + more, is an open term.

```scala211
var factor = 2
val multiplier = (i: Int) => i * factor
(1 to 10) filter (_ % 2 == 0) map multiplier reduce (_ * _)
```

```scala211
factor = 3
(1 to 10) filter (_ % 2 == 0) map multiplier reduce (_ * _)
```

The resulting function value, which will contain a reference to the captured more variable, is called a ```closure```, therefore, because the function value is the end product of the act of closing the open term, (x: Int) => x + more.