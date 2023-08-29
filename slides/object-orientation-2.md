---
layout: presentation
title: Object Orientation
permalink: /slides/object-orientation-2/
---

class: center, middle

# Object-Oriented Programming (OOP)

Part 2

---

# Agenda

1. [Creating Difference](#difference-7)
2. [Controlling Belongingness](#belongingness)
3. [Comparing Sameness](#comparisons)
4. [Stringification](#stringification)
5. [The 4 Pillars of Object-Orientation](#pillars)
6. [Alternative Paradigms](#alternative-paradigms)
7. [Conclusions](#conclusions)

---

template: difference
name: difference-7

## Changing internal state

Constructors allow us to set up an object's internal state at the moment of its creation. But what if we wanted to update those values at some later date?

--

- For example, what if one of the 101 Dalmatians has a [happy] birthday and is now a year older... can we not update the age property?

--

- In other words, we would like to be able to do something like this:

```java
// instantiate an object with an initial internal statee
Dog dog1 = new Dog("Fido", "Bugle", 10);

// do some very important significant stuff...

// update the object's internal state at some later point
dog1.age = dog1.age + 1; // happy birthday!

```

--

By now, you know that this is not possible. The internal properties are **private** and cannot be accessed from 'user' code in a different class.

---

template: difference
name: difference-8

## Setters

To change an object's internal state, we need a '**setter**' function to allow us to set the value of an existing object.

--

```java
public class Dog {
    // ...etc etc

    // a setter function
    public void setAge(int age) {
        // first validate the value, and then use it if good
        if (age > 0 && this.age < 15) this.age = age;
    }

    // ...and so on and so forth
// ...
```

--

- Note that the setter method performs **validation** - it only allows good values to be placed into the property - this is typical of setters.

--

- Note also that the method is _public_, so it can be called from code outside the `Dog` class.

---

template: difference
name: difference-9

## Setters (continued)

With setters, it is possible to set the values of properties on existing objects.

--

Assuming we have created a Dog object...

```java
Dog dog1 = new Dog("Roly Poly", "Dalmatian", 10); // instantiate a dog
```

--

...we can now update its age using the setter

```java
dog1.setAge(11);
```

---

template: difference

## Setters (continued again)

If setters are present, they should _always_ be used whenever an object's property values need to be changed.

--

- if a **constructor** sets an object's initial starting property values, it should do so by calling the object's setters.

--

- if **any other method** adjusts an object's property values, it should do so by calling the object's setters.

--

- this guarantees that any **validation** performed within the setter function is always used, and this validation logic is written in only one place in the code - in the setter.

---

template: difference
name: difference-9

## Accessing internal state

What if you wanted to know a particular Dog's age... how could you find that out programmatically?

--

- For example, instead of hard-coding `11` in the statement `dog1.setAge(11);`, could we have programmatically determined `dog1`'s current age and simply added one to that?

--

- We certainly cannot do the following, since the age property is _private_ and cannot be read from code outside the `Dog` class:

```java
dog1.setAge ( dog1.age + 1 )
```

---

template: difference
name: difference-10

## Getters

Of course, we can allow access to an object's internal state. But we need to create '**getter**' functions to do so.

--

```java
public class Dog {
    // ...etc etc

    // a getter function
    public int getAge() {
        // simply return the value of the age property
        return this.age;
    }

    // ...and so on and so forth
// ...
```

--

- Note that this function simply returns the value of a private property of the object. It may seem a bit redundant, but this is typical of getters.

--

- Note also that the method is _public_, so it can be called from code outside the `Dog` class.

---

template: difference
name: difference-11

## Getters (continued)

With a getter function, we can read the current value of a property of an object...

--

```java
System.out.println ( dog1.getAge() ); // will output dog1's age
```

--

... and use that information to help us understand that object's internal state

```java
dog1.setAge( dog1.getAge() + 1 );
```

--

Knowledge of an object's internal state can help us make decisions

```java
if ( dog1.getBreed().equals("Dalmation") && dog1.getName().equals("Pepper") ) {
    // use your imagination
}
```

---

name: belongingness

# Controlling Belongingness

--

## Non-static properties and methods

Neither _setters_ nor _getters_, nor even the methods that represent actions of the object (e.g. _bark_, _fetch_, _sleep_) were declared with the keyword `static` in their method signatures. Neither were any of the properties (e.g. _name_, _breed_, _age_).

--

- The keyword, `static`, is used to indicate that a method or property _belongs to the class as a whole_, not to each particular object independently.

--

- Thus, properties and methods that we want to _belong to each object individually_ do not use the `static` keyword.

--

- Each dog has its own _name_, _breed_, _age_, and each dog does its own _barking_, _fetching_, and _sleeping_. So it makes sense that these properties and methods would not be static.

--

- Making such properties and methods static would indicate that all dogs share them - _one name for all_, _one breed for all_, _one age for all_, all _fetching as one_, _sleeping as one_, _eating as one_, etc.

---

template: belongingness

## Shared concerns

There are, of course, cases where it makes sense for a property or method to belong to the class as a whole... i.e. for it to be declared as `static`.

--

- For example, imagine that you wanted to keep track of how many dog objects had been instantiated from the Dog class.

--

- You could create a `static` property named `numDogs` that is incremented each time a Dog is instantiated.

---

template: belongingness

## Shared concerns (continued)

```java
public class Dog {
    //...
    public Dog(String name, String breed, int age) {
        //...
        Dog.numDogs++; // increment the static property
        //...
    }
    //...
    private static int numDogs = 0;

//...
```

--

- Note that we refer to the property as `Dog.numDogs`, rather than `this.numDogs`.

--

- `this.numDogs` would suggest that the `numDogs` property belongs only to the Dog being instantiated, which is not correct - an error!

--

- `Dog.numDogs` clearly communicates that the `numDogs` property belongs to the `Dog` class as a whole - correct!

---

template: belongingness

## Shared concerns (continued again)

Every time we instantiate a new `Dog` object, the counter will be incremented.

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

--

- Because the counter was declared as `private`, we cannot see how many dogs have been made from code outside the `Dog` class.

--

- if were to make a `public` _getter_ method for the `numDogs` property defined within the `Dog` class, we would be able to call it from outside the `Dog` class to find out how many dogs had been made.

--

```java
System.out.printf( "There exist %d dogs in our world.\n", Dog.getNumDogs() );
```

---

name: comparisons

# Comparing Sameness

--

## Different kinds of difference

There are a few ways we can compare two objects.

--

- by whether they are, in fact, the same object in memory

--

- by whether their internal states are the same or similar

---

template: comparisons

## Identity comparison

To check whether two supposedly-separate objects are, in fact, the same object, use the `==` operator.

--

```java
if (dog1 == dog2) {
    System.out.printf("%s is actually the same dog as %s!\n", dog1.getName(), dog2.getName);
}
```

--

- Objects in Java are **reference types**, meaning that a variable assigned to point to an object holds the memory address of that object.

--

- The `==` operator, when used with a reference type, thus compares memory addresses.

---

template: comparisons

## Objects as reference types

Because objects are reference types, when they are passed as arguments to a method, the memory address is what is passed.

--

- For example, imagine a method that changes any dog's name to "Dog"...

```java
public void rename(Dog d) {
        d.setName("Dog");
}
```

--

- ... and let's say we call that method from some other method.

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
rename(dog1);
System.out.println ( dog1.getName() )
```

--

- The dog object referred to within the `rename` method as `d` is the same dog object referred to by the calling method as `dog1` - they are **aliases**.

--

- So the printed output will be "Dog", not "Fido".

---

template: comparisons

## Internal state comparison

To check whether two objects share the same internal state, even if they are different objects in memory, we have to roll our own solution.

--

- Conventionally, this would be done by defining a method named `equals` that performs the comparison.

--

name: tedium

```java
public class Dog {
        //...

        public boolean equals(Dog that) {
            boolean sameName = this.name.equals( that.getName() ); // are the names the same?
            boolean sameAge = ( this.age == that.getAge() ); // same age?
            boolean sameBreed = ( this.breed.equals( that.getBreed() ) );
            boolean sameWeight = ( this.weight == that.getWeight() );
            return sameName && sameAge && sameBreed && sameWeight; // true if all the same, false otherwise
        }
        //...
```

---

template: comparisons

## Internal state comparison (continued)

To compare two dogs, you would use one of those dogs' `equals()` method.

```java
if ( dog1.equals(dog2) ) {
    System.out.printf("%s and %s have the same internal state!\n", dog1.getName(), dog2.getName);
}
```

---

name: stringification

# Stringification

--

## Concept

Converting an object to a String usually leads to unwanted text.

--

```java
// instantiate a Dog object
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);

// do something that requires the object to be converted to a String
String text = String.format("The dog as a string looks like: %s", dog2);

// see what you get...
System.out.println(text);
```

--

By default, the output would show the **class** name of the object and a **[hashcode](https://coderanch.com/t/321515/java/HashCode)** - random-looking text that is not probably what you hoped for.

```
The dog as a string looks like: Dog@63961c42
```

--

Wouldn't it be nice if we could instead output something descriptive, like,

```
The dog as a string looks like: Tobik, a 3-year-old German Shepherd
```

---

template: stringification

## Fulfilling our desires

Java allows an object to describe how it should be converted to a String with a special method named `toString()` that returns the String equivalent of the object.

--

```java
public class Dog {
    //...
    public String toString() {
        String myself = String.format( "%s, a %d-year-old %s", this.getName(), this.getAge(), this.getBreed() );
        return myself;
    }
    //...
}
```

--

Now, converting the object to a String will result in something more descriptive, such as:

```
Tobik, a 3-year-old German Shepherd
```

---

name: pillars

# The 4 Pillars of Object-Orientation

--

## Concept

No university course would pass the censors unless it mentioned at least one set of immutable laws students must memorize despite their better judgment.

--

- Our course is no different. So here they are.

--

The **four pillars of object-oriented programming**:

--

1. Abstraction

--

2. Encapsulation

--

3. Inheritance

--

4. Polymorphism

---

template: pillars

## Abstraction

> abstract (adjective): disassociated from any specific instance
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/abstract)

--

Abstraction is thus the _process of making something abstract_ or _the state of being abstracted_.

--

- The **black box metaphor** encourages abstraction.

--

- **Hiding implementation details** of code encourages abstration

--

- **Classes** are abstractions of the objects that are instantiated from them.

--

- **Static properties and methods** are abstractions, as they are not tied to any instance.

---

template: pillars

## Encapsulation

> encapsulate (verb): to enclose in or as if in a capsule
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/encapsulate)

--

Encapsulation is thus the _process of enclosing some things within other things_.

--

- **Instance properties and methods** are encapsulated within the objects to which they belong.

--

- **Static properties and methods** are encapsulated within the class to which they belong.

--

- **Classes** are encapsulated within the packages to which they belong.

--

- **Packages** may be encapsulated within parent packages.

---

template: pillars

## Inheritance

> inherit (verb): to receive from an ancestor
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/inherit)

--

Inheritance is thus _that which is inherited from an ancestor_.

--

- **Classes**, and the objects instantiated from them, can inherit properties and methods from ancestor classes (we have not discussed this yet).

--

- **Classes**, and the objects instantiated from them, can inherit properties and methods from ancestor interfaces (we have not discussed this yet).

---

template: pillars

## Polymorphism

> polymorphism (noun): the quality or state of existing in or assuming different forms
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/polymorphism)

--

- **Objects** can be instances of more than one class (we have not discussed this yet).

--

--

- **Objects** can also be instances of one or more interfaces (we have not discussed this yet).

---

name: alternative-paradigms

# Alternative Paradigms

--

## Free choice

There is currently no major threat to object-oriented programming, since it is so widespread. However, other programming paradigms do exist:

--

- **Functional programming** is focused on _data flow_ (i.e. immutable values being used in formulae to compute other values) , rather than control flow (i.e. "Do this, then do that!" and where variables are not values but rather memory locations with changing values over time). Popular languages for functional programming are **Excel** and **Haskell**. There is growing interest in this 70-year-old style! [Learn more!](https://www.infoq.com/presentations/Taming-Effect-Simon-Peyton-Jones/)

--

- **Procedural programming** was the standard paradigm before object-oriented programming took over. It is still what is taught 70 years later in many entry-level programming courses, where the instructors are perhaps afraid to talk (or think) abstractly. The problem to be solved by a program is decomposed into sub-problems, and procedures (a.k.a. functions) to solve each problem are written and executed in sequence.

---

template: alternative-paradigms

## The future

- Many see a **multi-paradigm future**, and some see a multi-paradigm present, where paradigms are mixed and matched, and each is used for its unique strengths.

---

name: conclusions

# Conclusions

--

You now have a basic understanding of object-oriented programming in Java. Well done.
