---
layout: presentation
title: String & Related Classes
permalink: /slides/strings-as-objects/
---

class: center, middle

# String & Related Classes

---

# Agenda

1. [Overview](#concept)
1. [String Class](#string)
1. [Immutability](#immutable)
1. [Character Class](#character)
1. [StringBuilder Class](#string-builder)
1. [Apache Commons Lang](#stringutils)
1. [Apache Commons Text](#commons-text)
1. [Apache Commons CSV](#commons-csv)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview
name: overview-1

## Concept

The term 'String', used in programming to indicate a 'string of characters', first came into regular usage in the mid 1960's, as languages such as Lisp allowed textual data processing to flourish. A more general meaning, to order a series of mathematical values, as if beads on a string, dates possibly to the 1930's.

--

- We will reframe our existing understanding of Strings in light of our newfound mastery of object-oriented programming.

---

name: string

# String Class

--

## Instantiation

Like all objects in Java, Strings can be instantiated using the `new` operator and passing the **constructor** a `char` array.

```java
char[] charr = { 'w','o','r','r','y',' ', 'n','o','t' };
String myMessageToYou = new String(charr);
```

--

- To make Strings appear more like primitive values, i.e. to simplify their overly verbose usage, Java offers syntactic sugar for their instantiation.

```java
String myMessageToYou = "worry not";
```

---

template: string

## Many functions return Strings

Rather than directly instantiating a String object, there are many functions in the Java API that instantiate new String object's on our behalf, e.g.

--

- `String myMessageToYou = "worry" + " " + "not";`

--

- `myMessageToYou.concat(", weary heads");`

--

- `myMessageToYou.substring( 0, myMessageToYou.indexOf(' ') );`

--

- `myMessageToYou.toUpperCase();`

--

- `myMessageToYou.toUpperCase().toLowerCase();`

--

- `myMessageToYou.replace("worry", "fear");`

--

- `String.format( " '%s', he said to the child. ", myMessageToYou )`

---

template: string

## .toString( ) methods

And every class can optionally declare a method named `toString()` that indicates how an object of that class should be converted to a String.

--

```java
public class Moped {
    // ...
    public String toString() {
        return String.format(
            "A moped at %s & %s facing %s",
            this.getStreet(),
            this.getAvenue(),
            this.getOrientation()
        )
    }
    // ...
}
```

--

```java
// ... assume we instantiated a Moped object ...
System.out.println( myMoped ); // output it as a String
```

---

template: string

## .toString( ) methods (continued)

Even if you don't define a `.toString()` method in your custom classes, one exists automatically anyway.

--

- How does this work?!

--

- Every object automatically _inherits_ some properties and methods from the oldest ancestor class in the Java API named `Object`.

--

- `toString()` is one of those.

--

- Here is `Object`'s implementation of its `toString()` method.

```java
//...
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
//...
```

---

template: string

## What's inside a String?

There are several useful functions for investigating the internals of a String.

--

- `int num = myMessageToYou.length();`

--

- `char c = myMessageToYou.charAt(5);`

--

- `char[] charr = myMessageToYou.toCharArray();`

--

- `int num = myMessageToYou.indexOf(" ");`

--

- `boolean isInThere = myMessageToYou.contains("not");`

--

- `boolean startsRight = myMessageToYou.startsWith("worry");`

--

- `boolean endsRight = myMessageToYou.endsWith("not");`

---

template: string

## Comparing two Strings

Comparing two strings can be done in a few different styles.

--

- `(myMessageToYou == "worry not")`

--

- `myMessageToYou.equals("worry not")`

--

- `myMessageToYou.equalsIgnoreCase("WORRY NOT")`

---

name: immutability

# Immutability

--

## Concept

String objects are immutable - once they have been instantiated, their contents cannot be changed.

--

- Creating immutable objects is quite simple in Java.

--

- One can create a class with a constructor that sets one or more private properties.

--

- So long as there are no public `setter` methods provided, those private properties can be frozen at their initial values.

--

```java
public class ImmutableDog {
    public ImmutableDog( String name, String breed, int age ) {
        this.setName(name);
        this.setBreed(breed);
        this.setAge(age);
    }
    // ... assume we define private setter methods
}
```

---

name: character

# Character Class

--

## Concept

The Character class is a _wrapper class_, used to do processing and analysis of char primitive values, e.g.

--

- `char[] a = "my, my".toCharArray();`

--

- `Character x = new Character(a[4]);`

--

- `x.equals('m')` -> true, of course

--

- `Character.isDigit(a[3])` -> false, of course

--

- `Character.isLetter(a[3])` -> true, of course

--

- `Character.toUpperCase(a[3])` -> 'L'

--

- `Character.isUpperCase(a[3])` -> false

---

name: string-builder

# StringBuilder Class

--

## Concept

Since Strings are immutable, concatening many Strings together or modifying the contents of a String tends to require a lot of code and more memory than it should. Enter StringBuilder.

--

- **StringBuilder** is an easy-to-use, memory-efficient class for mutating text.

--

- `StringBuilder myBuilder = new StringBuilder("Welcome");`

--

- `int num = myBuilder.length();`

--

- `myBuilder.append(" to class!");` // it's mutable!

--

- `myBuilder.insert( 11, "this wonderful " );` // it's easy to insert

--

- `myBuilder.delete( 16, 25 );` // it's easy to delete parts

--

- `myBuilder.reverse();` // because we can

---

template: string-builder

## Extracting the String from StringBuilder

Converting the contents of a StringBuilder to a regular String is a facile matter.

--

- `myBuilder.toString()`

--

- `myBuilder.substring(11, 15)`

---

name: stringutils

# Apache Commons Lang

--

## Patching the Java API

Java, remarkable though it is, is lacking in many basic functionality today's programmers might expect. [Apache Commons Lang](https://commons.apache.org/proper/commons-lang/) attempts to fill in many of those gaps.

**StringUtils** is one class in the Apache Commons Lang library that might be of interest to us here.

--

- to use it, you can [download](https://commons.apache.org/proper/commons-lang/download_lang.cgi) a compiled (binary) version of the library.

--

- unzip it and place the main `.jar` file into your project's `lib` directory.

--

- then in code, import it with `import org.apache.commons.lang3.StringUtils;`

---

template: stringutils

## StringUtils Examples

```java
// align the text "foo" within 10 spaces
String s1 = StringUtils.center("foo", 10); // -> "   foo    "
String s2 = StringUtils.leftPad("foo", 10); // -> "foo       "
String s3 = StringUtils.rightPad("foo", 10); // -> "       foo"
```

--

```java
// check whether a string is uppercase or has all alphabetic or numeric characters
boolean isUps = StringUtils.isAllUpperCase("help"); // -> false
boolean isAlphas = StringUtils.isAlpha("abcdef"); // -> true
boolean isNums = StringUtils.isNumeric("12345"); // -> true
boolean isAlphaNums = StringUtils.isAlphanumeric("abcdef12345"); // -> true
```

--

```java
// join an array
String[] foo = {"foo", "bar", "baz", "bum"};
String s = StringUtils.join(foo, ","); // -> "foo,bar,baz,bum"
```

--

Full documentation of StringUtils [here](https://commons.apache.org/proper/commons-lang/javadocs/api-release/index.html).

---

name: commons-text

# Apache Commons Text

Similar to [Commons Lang](#stringutils), Apache's [Commons Text](https://commons.apache.org/proper/commons-text/) project aims to give developers access to common string algorithms and processes that are not supported by the Java API or the various text-related classes added by Commons Lang. Classes include:

--

- `StringSubstitutor` - a class for substituting variables within a String.

--

- `WordUtils` - a class containing methods specific to text composed of words, for example capitalization changes of the first letter of each word or line-wrapping text based on word boundaries.

--

- `StrTokenizer` - contains methods to tokenize (i.e. parses or split) a string based on delimiters and pattern matching.

--

- `StringEscapeUtils` - a class containing methods to escape and unescape Java, JavaScript, HTML and XML.

--

- various classes to help calculate similarity or difference between two Strings.

---

name: commons-csv

# Apache Commons CSV

[Commons CSV](https://commons.apache.org/proper/commons-csv/) is another project by Apache to make dealing with CSV (**comma**- or **character**-separated values) text files easier.

--

- CSV text files are those plain text files that store data in lines, where the values in each line are separated by a standard separator (often - but not always - a comma `,` character)

--

- Commons CSV can parse data in files following standard CSV format, Excel format, and other similar formats.

--

- As with Commons Lang, the main `.jar` file of Commons Text must be added as a dependency to a project, such as by placing it within the `lib` directory.

---

name: conclusions

# Conclusions

--

You now have increased your knowledge of the String and related classes as examples of typical object-oriented Java classes.
