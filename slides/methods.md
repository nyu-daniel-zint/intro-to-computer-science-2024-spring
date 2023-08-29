---
layout: presentation
title: Methods
permalink: /slides/methods/
---

class: center, middle

# Methods

---

# Agenda

1. [Overview](#concept)
1. [Simple Methods](#simple)
1. [Parameters & Arguments](#parameters)
1. [Return Values](#return)
1. [Overloading](#overloading)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

Methods are modular reusable blocks of code.

--

- The control flow of a program can easily switch to code within a method from anywhere else in the code.

--

- Switching to code within a method is termed 'calling' or 'invoking' that method.

--

- Calling a method is a form of unconditional branching - disrupting the 'usual' flow of a program.

--

- Once the control flow reaches the end of an invoked method, the control flow returns to the line of code from which it originally branched.

---

name: simple

# Simple Methods

--

## Super simple

At their simplest, methods can have no parameters and no return value.

For example, a method named 'doSomething1':

```java
public static void doSomething1() {
    System.out.println("Running  doSomething1");
    // imagine some useful stuff happens in the middle here
    System.out.println("Exiting  doSomething1");
}
```

---

template: simple
name: simple-2

## Methods calling methods

Of course, methods can call other methods, as our `doSomething1` already displayed - it called the `System.out.println` method several times.

Note the order in which the print statements are executed.

```java
public static void doSomething1() {
    System.out.println("Begin doSomething1");
    // imagine some useful stuff happens in the middle here
    System.out.println("End doSomething1");
}

public static void doSomething2() {
    System.out.println("Begin doSommething2");
    doSomething1(); // call the method
    System.out.println("End doSomething2");
}
```

---

template: simple
name: simple-3

## Call stack

The order is determined by the control flow of the program.

--

- Each method invocation creates a new 'stack frame' - an area of memory dedicated to the newly invoked method.

--

- The Java interpreter is only ever looking at the method invocation at the top of the stack - the most recently invoked method.

--

- Each stack frame has its own variable namespace, so you can have two variables named `x` in two different method invocations, and they will be different variables in two different areas of memory with potentially different values.

--

- Once a method that has been invoked completes, its stack frame is popped (deleted) from the call stack and its memory is wiped clean.

---

name: parameters

# Parameters

--

## Concept

Methods can accept 'arguments' - values sent into the method.

--

- These arguments are stored in 'parameters' - local variables within the namespace of the method invocation's stack frame.

--

- Once the method invocation completes, any local variables, including parameters, are wiped out of memory.

--

```java
public static void doSomething1(int x) {
    x++; // increment x
    System.out.println("Begin doSomething1, x=" + x);
    System.out.println("End doSomething1, x=" + x);
}
```

---

name: return

# Return values

--

## Concept

Methods can return a single value in Java.

--

- The method signature line must state the data type of the returned value

--

- This value is returned to the part of the code from which the method was originally invoked.

--

- Think of it as if the method invocation is replaced by that method's return value.

--

```java
public static int doSomething1(int x) {
    x++; // increment x
    System.out.println("Begin doSomething1, x=" + x);
    System.out.println("End doSomething1, x=" + x);
    return x;
}
```

---

name: overloading

# Overloading

--

## Concept

Java allows multiple methods with the same name but different parameter sets. These are called overloaded methods.

--

- Which version of the method is invoked depends upon the arguments in the method call.

--

```java
public static void foo() {
    ...
}

public static void foo(String bar) {
    ...
}

public static void foo(String bar, boolean baz) {
    ...
}
```

---

name: best-practices

# Best Practices

A method should

--

- represent **one** task

--

- fit into your screen

--

- be self explaining - think of good names

--

- as generic as possible

--

- deal with bad input and throw errors

--

- expect occuring errors

---

name: conclusions

# Conclusions

--

You now have a basic understanding of methods in Java.
