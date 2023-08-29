---
layout: presentation
title: Object Orientation
permalink: /slides/object-orientation-1/
---

class: center, middle

# Object-Oriented Programming (OOP)

Part 1

---

# Agenda

1. [Overview](#overview)
2. [Black Box](#black-box)
3. [Files](#example-1)
4. [Dogs](#example-2)
5. [Creating Difference](#difference)

---

name: overview

# Overview

---

template: overview
name: overview-1

## Concept

Object-Oriented Programming (OOP), first experimented with in the 1950's, is today the standard programming paradigm. Nearly all major contemporary programming languages offer the ability to program with objects.

--

- code is written to represent virtual _things_.

--

- each thing has certain **properties** (i.e. variables) that belong to it.

--

- each thing has certain **actions** (i.e. methods) that it can perform.

---

template: overview
name: overview-2

## Concept (continued)

With object-oriented programming, a developer writes a _description_ of things of a certain type.

--

- This acts as a fixed plan or _concept_ for things of this type - a **class**.

--

- Things are then created that _embody_ the abstract concept - **objects**.

---

template: overview
name: concept-digression

## Digression

In the 5th century, B.C., the astonishingly brilliant philsopher, Plato, described what we now call the [Theory of Forms](https://philosophynow.org/issues/90/Plato_A_Theory_of_Forms).

--

- In this theory, **forms** are the non-physical essences of all things, of which **objects** in the physical world are merely imitations or stand-ins.

--

- Things, transient as they are, are not as **real** or true as the eternal concepts or blueprints from whence they come.

--

- So, for example, any given **tree** is not as real as the concept of Tree.

--

- But we cannot **encounter** forms directly, only through the objects that embody them, however imperfectly.

--

- It took us only 2.5 thousand years to begin to code in that direction.

---

template: overview
name: overview-2

## Understand this: it's imperative!

Object-oriented programming is a variety of **imperative programming**.

--

- With imperative programming, we instruct the computer **how** to solve the tasks.

--

- Programs make heavy use of memory and **control flow**: loops, conditional statements with branching, and so on, to establish the sequence of steps necessary to solve the problem.

--

- An alternative to imperative programming would be **declarative programming**, where a desired end goal is declared, but the implementation details of how to achieve it are not. **SQL** is an example of a declarative language.

---

name: black-box

# Black Box Metaphor

---

template: black-box
name: black-box-1

Despite being a form of imperative-style programming, specifying in detail how problems are to be solved, object-orientation nevertheless attempts to put to practice the [black box metaphor](https://en.wikipedia.org/wiki/Black_box) of engineering, where, provided particular inputs, a machine produces a predictable output and _the user of it doesn't have to know the implementation details_, even though they are written in the code.

![Black box metapahor](../files/oop-black-box-metaphor.png)

---

name: example-1

# Example 1 - Files

---

template: example-1
name: example-1a

## Concept

Imagine you wanted to write code that represented **files** on a computer's hard drive.

---

template: example-1
name: example-1b

## Properties

Every file on the hard drive might have some properties, e.g.

- the data stored within the file
- metadata: filename, size, date modified, etc.

--

The values these properties hold collectively represent the _internal state_ of any given file at any given moment in time.

---

template: example-1
name: example-1c

## Actions...

If we say a file is in control of its own destiny (a big if), we could say a file has a few actions it could take, e.g.:

- update the data it holds
- change its filename
- save itself to a particular location on the hard drive

---

template: example-1
name: example-1d

## ... and their consequences

These actions represent a _public interface_ through which other code can interact with any given file and instruct it what actions to take.

--

```java
// telling the thing what to do...
myFile.setFilename("foobar.txt");
myFile.storeData(someData);
```

--

Calling these methods automatically updates the internal state of the _thing_.

--

```java
// ...causes an internal update of its state - i.e. the values of the properties
filename = "foobar.txt";
data = someData;
```

---

template: example-1
name: example-1d

## UML class diagram

There is a standardized way of representing such _things_, called the Unified Modeling Language (UML). Here is an example of a UML '**class**' diagram:

![UML file example](../files/oop-uml-file-example.png)

---

template: example-1
name: example-1e

## Class definition

This diagram can be translated into code as such:

```java
public class File {
    // properties
    private byte[] data;
    private String filename;
    private int size;
    private int modifiedDate;

    // actions
    public byte[] getData() { ... };
    public void setData(byte[] data) { ... };
    public String getFilename() { ... };
    public void setFilename(String filename) { ... };
    public void saveTo(String filePath) { ... };
}
```

---

template: example-1
name: example-1f

## Intention

A **class** definition is a template from which as many **objects** can be made as we like.

--

- Each specific File object has its own copy of the properties and methods defined in the File class - these are termed **instance properties ** and **instance methods**.

--

- Each specific File object can have its own specific set of values for the properties defined in the class.

--

- Each specific File object will respond to calls to it using any of the methods defined in the class.

--

- The internal state of each object is hidden by making the properties private. Code written inside other class definitions cannot see them.

---

name: example-2

# Example 2 - Dogs

---

template: example-2
name: example-2a

## Concept

Imagine **dog**, the concept.

---

template: example-2
name: example-2b

## Properties

Every dog might have some properties, e.g.

- name
- age
- breed
- weight

--

Different dogs will probably have different values for each of these properties.

--

- The value of each dog's properties at any given moment in time repesents that dog's **internal state**.

---

template: example-2
name: example-2c

## Actions...

If we say a dog is in control of its own destiny (a big if), we could say a dog has a few actions it could take, e.g.:

--

- bark

--

- fetch

--

- sleep

---

template: example-2
name: example-2d

## ... and their complications

Two dogs with different internal states might implement these same actions differently.

--

- For example, a lightweight lap dog might have a rapid fire tinny yapping sort of bark, whereas a heavy shepherd might occasionally produce a mellow deep woof sound.

--

- A young dog might generally successfully fetch an object, while an elderly dog might generally fail at this.

--

- A breed known for its abilities as a guard dog might bark more often and more fiercely than others.

---

template: example-2
name: example-2g

## UML class diagram

A UML class diagram for this dog thing:

![UML dog example](../files/oop-uml-dog-example.png)

---

template: example-2
name: example-2h

## Class definition

This diagram can be translated into code as such:

```java
public class Dog {
    // properties
    private String name;
    private int age;
    private String breed;
    private int weight;

    // actions
    public void bark() { ... };
    public void fetch() { ... };
    public void sleep() { ... };
}
```

---

template: example-2
name: example-2i

## Intention

This Dog **class** definition is a template from which as many Dog **objects** can be made as we like.

---

template: example-2i
name: example-2j

- Each specific Dog object has its own specific values for each of the properties the class defines.

---

template: example-2j
name: example-2k

- Each specific Dog object will respond to calls to any of the methods that the File class defines.

---

template: example-2k
name: example-2l

- The actions produced by these method calls may differ slightly, depending upon the internal state of each Dog object

---

name: difference

# Difference

---

template: difference
name: difference-1

## Constructing different objects from the same class

Our intention in creating a class is to be able to instantiate multiple distinct objects from that class template.

---

template: difference-1
name: difference-2

- We typically want these objects to have some differences from one-another.

---

template: difference
name: difference-2

## No difference

The following code, _placed in the code of some other class definition_, would instantiate two Dog objects from our Dog class.

```java
Dog dog1 = new Dog();
Dog dog2 = new Dog();
```

---

template: difference-2
name: difference-2a

These are different _things_ in memory.

```java
(dog1 == dog2) // false... they are different references
```

--

But they do not have any difference in terms of their _internal states_.

--

- `String name` -> `null` by default
- `int age` -> `0` by default
- `String breed` -> `null` by default
- `int weight` -> `0` by default

---

template: difference
name: difference-3

## Difference!

If the internal properties of each Dog object were **public** or **protected** (which they are not), it might be possible to give each object distinct values:

--

```java
Dog dog1 = new Dog();
// the following won't work, since the Dog's properties are all private
dog1.name = "Fido";
dog1.breed = "Bugle";
dog1.age = 10;

Dog dog2 = new Dog();
// the following won't work, since the Dog's properties are all private
dog2.name = "Tobik";
dog2.breed = "German Shepherd";
dog2.age = 3;
```

--

But this requires us to make visible the internal properties of the object, which goes against the black box metaphor and imperative-style programming.

---

template: difference
name: difference-3

## Difference! (continued)

If we were able to set each Dog's name, breed, and age to different internal states, while retaining hidden internal properties for each object, then we would achieve our goal.

--

We would like to be able to do something like this:

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

--

At the moment, our class definition provides no mechanism for setting a given object's internal properties.

---

template: difference
name: difference-4

## Constructors

In order to be able to set each object's properties discretely, we need to modify the Dog class to have a special **constructor** function.

--

```java
public class Dog {

    // a constructor function!
    public Dog(String name, String breed, int age) {
        // set this object's internal properties
        this.name = name;
        this.breed = breed;
        this.age = age;
    }

    // properties
    private String name;
    private int age;
    private String breed;
    // and so on...
//...
```

---

template: difference
name: difference-5

## Constructors (continued)

Note that constructor functions do not specify a return type.

```java
public class Dog {
    //...
    public Dog(String name, String breed, int age) {
        //...
    }
    //...
}
```

---

template: difference
name: this

## This, not that

The `this` keyword is used to indicate which object we are talking about it.

--

- Since a single class is a blueprint that can be used to create many objects, Java needs to know which object we are referring to.

--

- So `this` always automatically refers to the object upon whom the current method is being called.

Imagine we defined the `Dog` class's bark method:

```java
public class Dog {
    //...
    public void bark() {
        System.out.printf( "%s says, 'Woof!' ", this.name );
    }
    //...
```

--

- Which dog's name will be output when this method is called?

---

template: difference

## This, not that (continued)

The answer is, "whichever dog the method is called upon".

--

If somewhere we call that method on a dog named Fido, then Fido's name will be output.

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);

//...

dog1.bark(); // outputs "Fido says, 'Woof!' "
```

--

Whereas, if we were to call that method on a dog named Tobik, then Tobik's name would be output.

```java
Dog dog2 = new Dog("Tobik", "Bugle", 10);

//...

dog2.bark(); // outputs "Tobik says, 'Woof!' "
```

---

template: difference
name: difference-5

## Instantiating objects

With constructor functions, we can instantiate as many objects as we like with whatever property values we want them to have.

--

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

---

template: difference
name: difference-6

## Instantiating objects (continued)

We could make 101 Dalmatians with random names and ages, if we wanted...

```java
// let's make a random mix of names and ages objects
String[] names = "Patch,Lucky,Cadpig,Roly Poly,Penny,Freckles,Pepper".split(",");
int[] ages = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14 };

Dog[] dogs = new Dog[101]; // will hold 101 Dalmatians

for (int i=0; i<dogs.length; i++) {
    // assign each dog random property values from these arrays
    String randomName = names[ (int) (Math.random() * names.length) ];
    int randomAge = ages[ (int) (Math.random() * ages.length) ];

    dogs[i] = new Dog( randomName, "Dalmatian", randomAge ); // instantiate a Dog object

    dogs[i].bark(); // make each dog bark

}
```
