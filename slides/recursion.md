---
layout: presentation
title: Recursion
permalink: /slides/recursion/
---

class: center, middle

# Recursion

> Use recursive procedures for recursively-defined data structures.
>
> –Kernighan and Plauger, in [The Elements of Programming Style](http://www2.ing.unipi.it/~a009435/issw/extra/kp_elems_of_pgmng_sty.pdf)

---

# Agenda

1. [Overview](#concept)
1. [Fibonacci Numbers](#fibonacci)
1. [Flipping Strings Backwards](#backwards)
1. [Calculating Powers](#powers)
1. [Generalized Pattern](#pattern)
1. [Fractals](#fractals)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

In mathematics and computer science, recursion is a function or procedure that is defined in terms of itself.

---

name: fibonacci

# Fibonacci Numbers

--

## A sequence

A classic example of a recursive algorithm is the calculation of the [Fibonacci Sequence](https://en.wikipedia.org/wiki/Fibonacci_number), a mathematical formula known to mathematicians since at least the 4th century B.C in India.

--

- The first two numbers in the sequence are `0` and `1`.

--

- Every subsequent number in the sequence is _the sum of the previous two_.

--

- e.g. `0`, `1`, `1`, `2`, `3`, `5`, `8`, `13`, `21`, `34`, `55`, etc.

--

- this is a recursive algorithm because to find the *n*th number in the sequence, you must determine the _n-1_ and _n-2_ numbers in the sequence.

--

- mathematically, this formula could be: `F(n) = F(n − 1) + F(n − 2)`

---

template: fibonacci

## In code

In Java, a recursive formula could be written to calculate the Fibonacci number at any *n*th position in the sequence.

--

```java
public static int fibonacci(int n) {
  if (n == 1) return 0;
  if (n == 2) return 1;

  return fibonacci(n - 1) + fibonacci(n - 2);
}
```
---

template: fibonacci

## Call stack

The following diagram illustrates the changes to the call stack over time as our algorithm calculates the Fibonacci number at position `5` in the sequence.

--

[![Calculating Fibonacci numbers](../files/recursion-fibonacci.png)](../files/recursion-fibonacci.png)

- [Click to view larger](../files/recursion-fibonacci.png)

--

- Notice that the `fibonacci()` method is called 9 times: once from `main()` and 8 additional recursive calls.

---

name: backwards

# Flipping Strings Backwards

--

## Another example

Let's take a simpler example of a recursive algorithm for a function used to flip a string backwards.

--

1. If the original string is only one character long, the reversed form is the same as the original. For example, `"e"` backwards is `"e"`. So simply return the original.

--

2. Otherwise, return the last character of the original string concatenated to the reversed version of the remainder (excluding the last character). For example, `"nonplussed"` backwards is `"d" + backwards("nonplusse")`

---

template: backwards

## In code

In Java, the recursive string flipping algorithm might look like this:

--

```java
public static String backwards(String original) {

    // if string is one character or less, return the original
    if (original.length() <= 1) {
      return original;
    }

    // otherwise, return the last character + the backwards of the remainder
    char lastChar = original.charAt(original.length() - 1);
    String remainder = original.substring(0, original.length() - 1);
    return lastChar + backwards(remainder);

}
```

---

template: backwards

## Call stack

Understanding recursion can sometimes be assisted by diagramming the _step-wise changes to the function call stack_, including the arguments and return values from each new function invocation.

--

[![Flipping a string backwards](../files/recursion-backwards.png)](../files/recursion-backwards.png)

---

name: powers

# Calculating Powers

--

## Solving power equations

Another illustrative example is to solve power equations recursively. For example, the problem of calculating the value of a base raised to a certain exponent, such as _6<sup>12</sup>_.

--

- If the desired power is `0`, we can simply return `1`, since anything raised to the power `0` equals `1`.

--

- Otherwise, we can decompose the problem and return _base x base<sup>pow - 1</sup>_. For example, _6<sup>12</sup>_ is the same as _6 x 6<sup>11</sup>_

---

template: powers

## In code

In Java, the recursive power algorithm might look like this:

--

```java
public static int power(int base, int exp) {

  if (exp == 0) {
    return 1;
  }

  return base * power(base, exp-1);

}
```

---

template: powers

## Call stack

The changes to the function call stack over time for calculating _5<sup>2</sup>_ might look like:

--

[![Calculating powers](../files/recursion-powers.png)](../files/recursion-powers.png)

---

name: pattern

# Generalized Pattern

--

## Concept

A recursive function almost universally follows a general pattern.

--

- check for a **base case**, and return a fixed value that doesn't require recursion, if found

--

- otherwise, decompose the problem in some way and return a value obtained from a **recursive function call**

---

template: pattern

## Fibonacci example

For example, let's revisit the Fibonacci algorithm.

--

```java
public static int fibonacci(int n) {
  // base case: we know the answer
  if (n == 1) return 0;
  if (n == 2) return 1;

  // recursive case: return the sum of two recursive calls
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

--

- the _base case_ occurs when the argument is either `1` or `2` - we simply return a `0` or `1` in response.

--

- in the _recursive case_, we return the sum of two recursive calls with smaller arguments than the original.

---

template: pattern

## Flipping string backwards example

And let's revisit the backwards string algorithm.

--

```java
public static String backwards(String original) {

    // base case: return the original
    if (original.length() <= 1) {
      return original;
    }

    // recursive case: return the last character + the backwards of the remainder
    char lastChar = original.charAt(original.length() - 1);
    String remainder = original.substring(0, original.length() - 1);
    return lastChar + backwards(remainder);

}
```

--

- the _base case_ occurs when the length is 1 or 0, we return the original.

--

- the _recursive case_ decomposes the problem and returns a value resulting, in part, from recursion.

---

template: pattern

## Calculating powers

The same pattern applies to the power equation.

--

```java
public static int power(int base, int exp) {

  // base case: return 1 when raised to power 0
  if (exp == 0) {
    return 1;
  }

  // recursive case: decompose the problem including recursion
  return base * power(base, exp-1);

}
```

--

- the _base case_ occurs when the exponent is `0`... we return `1`.

--

- the _recursive case_ decomposes the problem and returns a value resulting, in part, from a recursive call.

---

name: fractals

# Fractals

--

## Concept

Fractals are a category of _algorithmically-generated images that exhibit a high-degree of self-similarity_.

--

- In other words, the whole image can be decomposed into parts that resemble, or are identical, to the whole image.

--

- They are typically generated using recursive algorithms.

--

- we will not try to derive the algorithms used to generate fractals, but will simply enjoy some pretty recursive pictures.

---

template: fractals

## Sierpiński triangle

One of the "classic" fractal images is the [Sierpiński triangle](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle#Constructions).

--

[![Sierpiński triangle](../files/recursion-sierpinski-triangle.gif)](../files/recursion-sierpinski-triangle.gif)

---

template: fractals

## Koch snowflake

Another is the [Koch snowflake](https://en.wikipedia.org/wiki/Koch_snowflake).

--

[![Koch snowflake](../files/recursion-koch-snowflake.gif)](../files/recursion-koch-snowflake.gif)

---

template: fractals

## Mandelbrot set

Perhaps the most famous fractal images are those derived from the [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set).

--

[![Mandelbrot set fractal](../files/recursion-mandelbrot.gif)](../files/recursion-mandelbrot.gif)

---

name: conclusions

# Conclusions

--

Recursion takes some time to get familiar with. However, it can describe some problems that are inherently recursive in a more intuitive way, with simpler code, than other forms of iteration.

--

- Thank you. Bye.
