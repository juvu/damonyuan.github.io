---
title:  "Digest: An introduction to functional programming"
description: "An introduction to functional programming"
date: 2018-04-15 18:00:00
categories: [Tech]
tags: [Digest]
---

# Digest: An introduction to functional programming

> * Original Article：[An introduction to functional programming](https://codewords.recurse.com/issues/one/an-introduction-to-functional-programming)
> * Author：[Mary Rose Cook](https://maryrosecook.com/)

## Characteristics: One thing in all - the absence of side effects

* **language features that aid functional programming**

1. immutable data

   An immutable piece of data is one that cannot be changed. Some languages, like Clojure, make all values immutable by default. Any “mutating” operations copy the value, change it and pass back the changed copy. This eliminates bugs that arise from a programmer’s incomplete model of the possible states their program may enter.

2. first class functions

   Languages that support first class functions allow functions to be treated like any other value. This means they can be created, passed to functions, returned from functions and stored inside data structures.

3. tail call optimisation

   Tail call optimisation is a programming language feature. Each time a function recurses, a new stack frame is created. A stack frame is used to store the arguments and local values for the current function invocation. If a function recurses a large number of times, it is possible for the interpreter or compiler to run out of memory. Languages with tail call optimisation reuse the same stack frame for their entire sequence of recursive calls. Languages like Python that do not have tail call optimisation generally limit the number of times a function may recurse to some number in the thousands. In the case of the race() function, there are only five time steps, so it is safe.

* **programming techniques used to write functional code**

1. mapping

2. reducing

3. pipelining

4. recursing

5. currying

   Currying means decomposing a function that takes multiple arguments into a function that takes the first argument and returns a function that takes the next argument, and so forth for all the arguments.

6. higher order functions

* **advantageous properties of functional programs**

1. parallelization

   Parallelization means running the same code concurrently without synchronization. These concurrent processes are often run on multiple processors.

2. lazy evaluation

   Lazy evaluation is a compiler technique that avoids running code until the result is needed.

3. determinism

   A process is deterministic if repetitions yield the same result every time.

## Thoughts: approach to eliminate side effects

1. Centralized states
2. Functional programming

Eg., React.js Redux library

* It has a centralized data source
* Data flow can only be changed in one direction (pipeline)