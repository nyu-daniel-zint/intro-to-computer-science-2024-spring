---
title: Documenting source code with Javadoc
permalink: /javadoc
---

# Documenting source code with Javadoc

**All programs must include javadoc comments in the source code.**

## Overview

[Javadoc](https://www.oracle.com/java/technologies/javase/javadoc-tool.html) is a tool built into the Java Development Kit that automatically generates documentation of your source code based on comments written in a particular syntax, and allows development environments, such as Eclipse, to offer intelligent tooltips that show this documentation when using methods or classes commented in such a manner. The javadoc tool depends upon you adding special comments into your code that include the necessary documentation. In order to use it effectively, you must add javadoc comments for all class definitions, method definitions.

The javadoc tool is run from Eclipse by clicking Project->Generate javadoc. This generates documentation in a folder named doc within your project folder. You can open this documentation in your web browser.

## Class definitions

### Required documentation

- a short layman's description of the class
- an `@author` tag for each author
- a `@version` tag

### Example

```java
/**
  * A program to output the message, "Hello world".
  *
  * @author Foo Barstein
  * @version 0.1
  */
  public class HelloWorld {
    // ...
  }
```

## Method definitions

### Required documentation

- a short layman's description of the purpose of the method
- a `@param` tag for each parameter for the method
- a `@return` tag if the method returns a value (not necessary for void methods)
- an `@exception` tag for each exception thrown by the method

### Example

```java
/**
  * Calculates the sum of two numbers.
  *
  * @param num1 The first number, as an integer.
  * @param num2 The second number to add to the first
  * @return The sum of the two integers
  * @exception IllegalArgumentException if num1 or num2 is less than 0
  */
  public static void sum(int num1, int num2) throws IllegalArgumentException {
    // ...
  }

```

## More

The documentation outlined here is the bare minimum of what javadoc offers. Here is a more complete reference list adapted from [David Flanagan, Java in a Nutshell, Second Edition, (O’Reilly 1997)](http://shop.oreilly.com/product/9781565922624.do), including javadoc tags that are not required in this course:

`@author` text

- Adds an "Author:" entry containing the specified text.
- Used to document class definitions

`@param` parameter-name description

- Adds the specified parameter and its specified description to the "Parameters:" section of the current method. If the description is longer than one line, it may be continued on the next.
- Used to document method definitions

`@return` description

- Adds a "Returns:" section containing the specified description to the documentation.
- Used to document method definitions

`@exception` full-classname description

- Adds a "Throws:" entry to the documentation. The entry contains the specified class name of the exception, and the description specified, which should explain the significance of the exception.
- Used to document method definitions

`@see` classname

- Adds a "See Also:" entry to the documentation that contains a hyperlink to the specified class (or interface).
- Used to document class, method, and field definitions

`@see` full-classname Type, Method, Field

- Adds a "See Also:" entry to the documentation that contains a hyperlink to the specified class (or interface).
- Used to document class, method, and field definitions

`@see` full-classname#method-name Type, Method, Field

- Adds a "See Also:" entry to the documentation that contains a hyperlink to the specified method of the specified class (or interface).
- Used to document class, method, and field definitions
