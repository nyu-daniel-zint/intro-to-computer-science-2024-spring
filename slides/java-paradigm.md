---
layout: presentation
title: The Java Paradigm
permalink: /slides/java-paradigm/
---

class: center, middle

# The Java Paradigm

"Write once, run anywhere"

---

# Agenda

1. [Computers](#computers)
2. [Programming](#programming)
3. [Machine code](#machine-code)
4. [Assembly languages](#assembly)
5. [High-level languages](#high-level-languages)
6. [Compiling](#compiling)
7. [Interpreting](#interpreting)
8. [Java](#java)
9. [Conclusions](#conclusions)

---

name: computers

# Computers

---

template: computers
name: computers-1

## Definition

> "[People don't have buttons and a computer does](http://www.youtube.com/watch?v=kccWna71sqk)"
>
> -Some little kid from PS-272 in Brooklyn in the 1980s

--

A computer is any device, entity, or object that can perform computations.

--

- [human computers](https://en.wikipedia.org/wiki/Computer_%28job_description%29)

--

- [mechanical computers](https://en.wikipedia.org/wiki/Mechanical_computer)

--

- [electronic computers](https://en.wikipedia.org/wiki/Computer#Digital_computers)

--

- [biological computers](https://en.wikipedia.org/wiki/Biological_computing)

--

- [quantum computers](https://en.wikipedia.org/wiki/Quantum_computing)

---

name: processor

# Processor

--

The processor is the part of an electronic computer that does the computation.

--

At any given moment, a processor only does one of a few different types of things.

--

- jump to a particular location in memory

--

- read a number from RAM

--

- save a number to RAM

--

- add two numbers together

--

- compare two numbers to see which is larger

--

- send a number to a particular device (e.g. a monitor)

--

- receive a number from a particular device (e.g. a keyboard)

--

Ultimately, every statement in a computer program must be reduced to a sequence of these processor actions.

---

name: programming

# Programming

---

template: programming
name: programming-1

## Purpose

> Computer programming is the process of designing and building an executable computer program for accomplishing a specific computing result.
>
> -[Wikipedia](https://en.wikipedia.org/wiki/Computer_programming)

---

template: programming
name: programming-2

## Levels of abstraction

Programmers have established increasingly higher levels of abstraction in order to make programming faster and more intuitive to humans.

--

### Low level:

- Machine languages
- Assembly languages

--

### High level:

- High-level programming languages
- [Visual programming](https://en.wikipedia.org/wiki/Visual_programming_language)

---

name: machine-code

# Machine code

--

## Binary instructions

At the lowest level, a programming can directly inform a computer what it should do by sending binary instructions directly to the processor.

--

Example of a set of machine instructions for an x86 processor to move the number 97 to the AL memory register:

```
10110000 01100001
```

--

The number `1011` is the machine instruction to do a move operation, `0000` is the address of the AL register, and `01100001` is the number `97` written in binary.

--

Each family of processors is designed to "understand" particular binary numbers to mean particular operations.

---

name: assembly

# Assembly languages

---

template: assembly
name: assembly-1

## Mnemonics

It's easier for most humans to memorize words than binary numbers. Assembly languages provide mnemonics that a programmer can write, which are converted automatically to machine language equivalents.

--

Example of a set of assembly instructions for an x86 processor to place the number 97 in the memory register called AL:

```
MOV AL, 61h
```

--

`MOV` is a mnemonic for `1011`, `AL` is a mnemnoic for `0000`, and `61` is the number `97` written in hexadecimal notation.

---

template: assembly
name: assembly-4

## Assembling

Converting code written in assembly language to the equivalent machine language is known as **assembling** - it's essentially a search/replace operation where mnemonics are replaced with their machine code equivalents.

The program to do so is called an **assembler**.

---

name: high-level-languages

# High level languages

---

template: high-level-languages
name: high-level-languages-1

## Abstraction

High-level languages are more intuitive for most humans to read and write.

The written code is further abstracted away from the machine instructions the processor will ultimately execute.

---

template: high-level-languages
name: high-level-languages-2

## Example

Storing the number 97 in a memory register using the C programming language:

```c
register int i = 97;
```

--

Other high-level programming languages include C, C++, C#, Java, Python, Ruby, Scratch, Javascript, and PHP. All offer higher-level capabilities, such as looping, functions, branching, etc.

---

template: high-level-languages
name: high-level-languages-4

## Translation to machine code

Converting code written in a high-level language to the equivalent machine code is done via one of two processes:

- compiling
- interpreting

---

name: compiling

# Compiling

--

## Concept

Code written in a high-level programming language is translated to its machine code equivalent all at once as a single bulk operation.

--

- a tool called a **compiler** reads the code, analyzes it, makes optimizations, and outputs a file with the required machine code instructions.

--

- time-consuming

--

- efficient

--

- many errors easily detected during compilation

--

- processor-specific

---

template: compiling
name: compiling-5

## C language

The C programming language is a classic example of a compiled language.

--

- There are different compilers to translate C to machine code for each popular processor family.

--

- The high-level source code must often be tweaked to match the features of the target processor before compiled.

--

- Not very portable!

--

- But fast!

---

name: interpreting

# Interpreting

--

Code written in a high-level programming language is translated to its machine code equivalent _and executed_ as a series of small steps.

--

- a tool called an **interpreter** traditionally reads one statement of high-level code at a time, converts it to its machine code equivalent, and immediately executes that machine code.

--

- starts running immediately

--

- not necessarily efficient, since only looking at one-statement at a time

--

- does not traditionally identify errors in statements that have not yet been interpreted

---

name: java

# Java

--

## Write once, run anywhere

Unlike C code, Java source code is highly portable, being executable on machines with almost any processor. How is this possible?

--

- Java is both compiled and interpreted

--

- Java high-level source code is compiled to **byte code**.

--

- Java byte code is then interpreted to machine code by one of the **Java Virtual Machines** (JVM)

--

- JVMs are created for most popular processor families

--

- Thus Java byte code is highly portable

--

- This is the Java paradigm!

---

template: java
name: java-8

## Write once, run anywhere

![The Java paradigm](../files/java_paradigm.png)

---

template: java
name: java-9

## Byte code and the JVM

Byte code is somewhere between machine code and high-level source in abstraction - an _intermediate-level_ language.

--

- The Java Virtual Machines are virtual computers (a software simulating a physical computer), which are designed to view byte code as their native machine code.

--

- These JVMs contain interpreters that can translate this byte code to the appropriate machine code for whichever physical processessor they are actually running on.

--

- Any programaming language that can be compiled into Java byte code can run in a JVM... Groovy, Kotlin, and Scala are popular high-level languages with different syntax from Java that take advantage of this.

---

template: java
name: java-13

## Byte code and the JVM

When viewed as hexadecimal, all byte code files start with the text, `cafe babe` - this is a [magic number](https://en.wikipedia.org/wiki/Magic_number_%28programming%29).

```
cafe babe 0000 0034 001f 0700 0201 0033
6564 752f 6e79 752f 6373 2f66 6231 3235
382f 6469 6666 6572 656e 745f 7061 636b
6167 652f 5468 6972 6443 6c61 7373 436c
...
```

One of Java's inventors, James Gosling, has [explained the origin of this](http://radio-weblogs.com/0100490/2003/01/28.html).

---

template: java

## commands

The `javac` command compiles Java source code into Java byte code, while the `java` command sends the Java byte code to the JVM's interpreter for execution.

--

```bash
foo@bar$ javac -d bin src/foo/bar/SomeFile.java
```

--

```bash
foo@bar$ java -cp bin foo.bar.SomeFile
```

---

name: conclusions

# Conclusions

--

You now have a basic understanding of compiling, interpreting, and how the Java paradigm fits into these schemes.

--

- Thank you. Bye.
