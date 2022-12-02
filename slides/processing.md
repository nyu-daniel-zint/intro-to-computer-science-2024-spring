---
layout: presentation
title: The Processing Framework
permalink: /slides/processing/
---

class: center, middle

# The Processing Framework

> You’ve baked a really lovely cake, but then you’ve used dog shit for frosting.
>
> ―Steve Jobs, critiquing a designer's work

---

# Agenda

1. [Overview](#concept)
1. [Installation](#installation)
1. [Run a Program](#run)
1. [Lifecycle Methods](#lifecycle)
1. [Animation](#animation)
1. [Inherited Functions](#functions)
1. [Adding Sounds](#sounds)
1. [Responding to Events](#events)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

[Processing](https://processing.org) is a code framework for animation. It is also the name of a non-profit foundation that attempts to teach programming and spread software literacy.

--

- The original concept - an animation framework that allows new coders to visualize programming concepts and have fun - has proven popular, not just with newbies.

--

- Initially Java-only, Processing has now been _ported_ to other popular languages, including [Python](https://py.processing.org/) and [Javascript](https://p5js.org/).

--

- The Javascript version, named p5.js, is debatably now the most popular implementation, allowing developers to easily create web-based animations, data visualizations, and games.

---

name: installation

# Installation

--

## Concept

Processing consists of a few **J**ava **AR**chive (`.jar`) files that you can import into your code.

--

- A `.jar` file is a package file, like `.zip`, that contains Java class definitions plus some settings.

--

- Once we properly import these Processing class definitions into our project, our code will be able to reference and use those Processing classes.

--

- How we import the `.jar` files depends on which Integrated Development Environment (IDE) we are using.

--

- The **Processing team produces its own IDE**, which is overly simple (albeit intentionally so) for our purposes - **do not use it**.

--

- You are advised to use the [Visual Studio Code](https://code.visualstudio.com) IDE.

---

template: installation

## Download Processing

Go to the [Processing web site](https://processing.org) and download the appropriate version for your system.

--

- Install it as you would any other application.

--

- You will now have the stand-alone Processing application, which includes the main file we need named `core.jar`.

--

- To locate `core.jar` on Mac, `Control`-click on the application in Finder and click `Show Package Contents`. Then find the file within at `Contents/Java/core.jar`

--

- To locate `core.jar` on Windows, find the file at `PATH_TO_PROCESSING/core/library/core.jar`, where `PATH_TO_PROCESSING` is the directory where it is installed.

--

- Copy this `core.jar` file and place it somewhere temporarily convenient, such as the `Desktop`.

---

template: installation

## Install Java SE 8

Processing currently **only works with Java 8** (a.k.a 1.8). If you are running a more recent version of Java, you must downgrade to Java SE version 8.

--

- Download and install the [jdk8u242-b08 version of OpenJDK 8](https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/tag/jdk8u242-b08) (be sure to select the file with `jdk` in its name, not the one with `jre` in its name.) (On MacOS, select the appropriate `.pkg` file; on Windows, select the appropriate `.msi` file.)

--

- Note the file path to the directory where this new JDK was installed. We'll refer to this directory later as `THE_PATH_TO_JDK_8`.
  - On Mac, it is probably in `"/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home"`. Note the inclusiong of `Contents/Home` at the end of the path - we'll need it with this addition in the settings file.
  - On Windows, it is probably in `C:\Program Files (x86)\AdoptOpenJDK\jdk-8.0.242.08-hotspot`, which would have to have its back slashes escaped to be `"C:\\Program Files (x86)\\AdoptOpenJDK\\jdk-8.0.242.08-hotspot"` in the settings file.

---

template: installation

## Set Up Visual Studio Code

Processing can be integrated into the popular [Visual Studio Code](https://code.visualstudio.com) IDE relatively simply.

--

- Install the [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack), if you haven't already.

--

- In Visual Studio Code, go to Settings (on MacOS, go to `Code`->`Preferences`->`Settings`; on Windows, go to `File`->`Preferences`->`Settings`.)

--

- Enter "`java jdt ls java home` into the search field. You should see an option with a link to `Edit in settings.json` - click that link to open that file in the editor.

--

- In the `settings.json`, edit the "`java.configuration.runtimes`" setting so that it includes the new JDK. Replace `THE_PATH_TO_JDK_8` in the example code below with the correct path to your JDK 8).
  - If there is no such setting currently in the `settings.json` file.
  - Place the following just before the last `}` at the end of the file. The previous line of code above this new code should end in a comma.

```javascript
  "java.configuration.runtimes": [
      {
        "name": "JavaSE-1.8",
        "path": "THE_PATH_TO_JDK_8",
        "default": true
      }
  ],
```

---

template: installation

## Set Up Visual Studio Code (continued)

We now install Processing's `core.jar` file as a dependency of a new Java project.

--

- Create a new Java Project. Do this by opening `View` -> `Command Palette` and type `Java: Create Java Project` into the Command Palette's text field and finish the setup.

--

- Drag the `core.jar` file from wherever you saved it, and drop it into the `lib` directory of the Java project.

--

- Configure the project-specific settings file. If your project does not already have a sub-directory named `.vscode`, create one and create a file therein named `settings.json`. If your project already has this directory and file, open it up. Enter the following code into the `.settings` file:

```javascript
{
  "java.project.sourcePaths": ["src", "test"],
  "java.project.outputPath": "bin",
  "java.project.referencedLibraries": ["lib/**/*.jar"]
}

```

---

template: installation

## Set Up Visual Studio Code (continued again)

We must now select Java 8 as the Java runtime to use for this new Java project.

--

- With the Java project open in Visual Studio Code, go to the Command Palette (`View`->`Command Palette`) and search for "`Java: Configure Java Runtime`". Click on the matching option that appears.

--

- In the `Configure Java Runtime` setting document, click the icon to edit the current runtime setting for this project and change it to the newly-installed JDK.

--

- In the Command Palette again (`View`->`Command Palette`), search for "`Java: Clean Language Server Workspace`". Click the matching option that appears and confirm that you would like to reset the Java language server.

--

At this point, we are ready to write Java code using the Processing library.

---

name: run

# Run a Program

--

## What we need to do in code

To use Processing, you must...

--

- import the classes within the `processing.core` package into your own project code

--

- make sure your custom class inherits properties and methods from the class, `PApplet`

--

- pass the `PApplet.main()` method the full name of your custom class

--

- set up lifecycle methods named `settings()`, `setup()`, and `draw()`

---

template: run

## Starter code

For example, enter the following starter code within the `src/fb1258` directory in a file named `MyClass.java`.

```java
package fb1258;

import processing.core.*;

public class Circle extends PApplet {
    public void settings() {
  		this.size(600, 400); // open a window that is 600x400, diameter=100
    }
    public void setup() {
    }
    public void draw() {
		  this.ellipse(250, 150, 100, 100); // draw an ellipse at x=250, y=150
    }
    public static void main(String[] args) {
  		PApplet.main("fb1258.Circle"); // this String must match exactly this class's package and class name
    }
}
```

---

template: run

## On syntax

You will note in our starter code that we use the `this` keyword as a prefix when referring to instance methods and instance properties. This is good code style.

```java
this.ellipse(250, 150, 100, 100);
```

--

- If you review any of the official Processing documentation or example code, you will note that they do not use the `this` keyword at all.

```java
ellipse(250, 150, 100, 100);
```

--

- Processing's goal is to avoid showing anything remotely object-oriented in their code so as to not scare newbies.

--

- _You_ should always prefix instance properties and methods with `this` and static properties and methods with the class name.

---

template: run

## Run it!

Run this program - if it works, you are in good shape!

---

name: lifecycle

# Lifecycle Methods

--

## Concept

The three methods we added to our code are automatically called by `PApplet`'s code at certain times in the life of the program.

--

- [settings()](https://processing.org/reference/settings_.html) is called once at the start of the program in order to set up the size of the application window that pops open.

--

- [setup()](https://processing.org/reference/setup_.html) is called once at the start of the program and can optionally be used to pre-load any images or other media that might be used later in the application.

--

- [draw()](https://processing.org/reference/draw_.html) is initially called directly after `setup()` and on an automatic timer every `60` seconds thereafter until the program stops animating. The code placed within this method is used to draw the frames of the animation.

---

name: animation

# Animation

--

## Concept

In frame-based animation, objects are redrawn in rapid succession at slightly different locations on the screen in order to give the illusion of movement.

```java
package fb1258;
import processing.core.*;
public class CircleSliding extends PApplet {

  private int x = 250; // starting x position of ellipse
  private int y = 150; // starting y position of ellipse

  public static void main(String[] args) {
    PApplet.main("fb1258.CircleSliding");
  }
  public void settings() {
    this.size(600, 400); /* open a window that is 600x400 */
  }
  public void draw() {
    this.background(0, 0, 0); // fill screen with black (R,G,B = 0,0,0)
    this.fill(255, 255, 255); // paint with white (R,G,B = 255,255,255)
    this.ellipse(this.x, this.y, 100, 100); // draw ellipse with fill color
    this.x++; // next time draw ellipse at slightly different location
    this.y++;
  }
}
```

---

name: functions

# Inherited functions

--

## Drawing

`PApplet` bestows a variety of useful functions upon our custom class, including many functions for drawing shapes to the screen.

--

- [ellipse(x, y, width, height)](https://processing.org/reference/ellipse_.html) - draws an ellipse

--

- [rect(x, y, width, height)](https://processing.org/reference/rect_.html) - draws a rectangle

--

- [line(x1, y1, x2, y2)](https://processing.org/reference/line_.html) - draws a line

--

- [loadImage(stringPathToImageFile)](https://processing.org/reference/loadImage_.html) - returns a `PImage` object that can be passed to the image() function

--

- [image(pImageObject, x, y)](https://processing.org/reference/image_.html) - draws any pImage object to the screen

--

- [textSize(intFontSize)](https://processing.org/reference/textSize_.html) - sets the size of any text to be drawn

--

- [text(someString, x, y)](https://processing.org/reference/text_.html) - draws text to the screen

---

template: functions

## Colors

There are several color-related properties that can be set using several appropriately-named functions...

--

- [background(r, g, b)](https://processing.org/reference/background_.html) - fills the entire screen with a solid color

--

- [fill(r, g, b)](https://processing.org/reference/fill_.html) - the color to use next time a shape is drawn to the screen

--

- [noFill()](https://processing.org/reference/noFill_.html) - don't use any fill for the next shape drawn to the screen

--

- [stroke(r, g, b)](https://processing.org/reference/stroke_.html) - the color to use for the outline around the next shape drawn to the screen

--

- [noStroke()](https://processing.org/reference/noStroke_.html) - don't use any stroke for the next shape drawn to the screen

---

template: functions

## ... and much more

These were just the easy functions to get started with.

--

- There are many more functions inherited by your class from `PApplet` - see [the full reference](https://processing.org/reference/)

--

- There is also a large ecosystem of 3rd-party libraries that add additional functionality not present in Processing itself - see [the official list of add-on libraries](https://processing.org/reference/libraries/)

---

name: sounds

# Adding Sounds

--

## Overview

An additional [`sound` library](https://processing.org/reference/libraries/sound/index.html) can be added to a project to provide sophisticated audio functionality.

--

- Download a zip file containing [the latest release](https://github.com/processing/processing-sound/releases) of this library.

--

- Unzip this file.

--

- Copy all the `.jar` files located within the `library` subdirectory into your project's `lib` directory.

---

## Playing Sounds (continued)

An example of a program that plays a sound when the user clicks.

```java
package fb1258;

import processing.core.*;
import processing.sound.*; // note this additional import

public class CircleWithSound extends PApplet {
    private SoundFile soundClick; // will refer to a sound file to play
    public void settings() {
  		this.size(600, 400); // open a window that is 600x400, diameter=100
    }
    public void setup() {
      // assuming you have created an audio file named thump.mp3 and placed it within a sounds subdirectory of your project
      this.soundClick = new SoundFile(this, "sounds/thump.mp3"); // if you're on Windows, you may have to change this file path to "sounds\\thump.mp3"
    }
    public void draw() {
		  this.ellipse(250, 150, 100, 100); // draw an ellipse at x=250, y=150
    }
    public void mouseClicked() {
      this.soundClick.play(); // play the sound!
    }
    public static void main(String[] args) {
  		PApplet.main("fb1258.CircleWithSound"); // this String must match exactly this class's package and class name
    }
}
```

---

name: events

# Responding to Events

--

## Mouse clicks

Processing's code can automatically call a function in your code anytime the user clicks a mouse.

--

- To take advantage of this, create a function named `mouseClicked()` in your code.

--

- This function will be called immediately _after_ the user clicks the mouse.

--

- Within this function, you can access the `x` and `y` coordinate at which the user clicked the mouse via the `this.mouseX` and `this.mouseY` properties of objects of your class.

--

```java
public void mouseClicked() {
  System.out.printf("clicked at %d, %d\n", this.mouseX, this.mouseY);
}
```

---

template: events

## Other mousing around

Processing will also call other functions you define for a variety of other mouse-driven events.

--

- a `mouseMoved()` function will be called whenever the user moves the mouse.

--

- a `mousePressed()` function will be called whenever the user presses the mouse.

--

- a `mouseReleased()` function will be called whenever the user releases the mouse button.

--

- a `mouseDragged()` function will be called whenever the user clicks and drags the mouse.

---

template: events

## Keyboard events

Processing can respond to various keyboard-driven events if you define functions to handle them.

--

- a `keyPressed()` function will be called whenever the user presses a key.

--

- a `keyReleased()` function will be called whenever the user releases a previously-pressed key.

--

- a property named `this.key` is always set to the most recently pressed key, as a `char` value.

--

- for common control keys, such as BACKSPACE, TAB, ENTER, RETURN, ESC, UP, DOWN, LEFT, RIGHT, and DELETE, the property `this.keyCode` contains a numeric code representing the key that was pressed.

--

- these `keyCode` values can be compared to constants Processing supplies, named after the key they represent, e.g.

```java
if (this.keyCode == UP) { /* ... */ }
```

---

name: multiple-classes

# Multiple Classes

--

## One window, please

When writing programs that use the Processing library, we must have a custom class that inherits from `PApplet`. But what do we do when we have more than one custom class?

--

- The `PApplet` class includes code to open an app window when it is instantiated. So every class we define that inherits from PApplet will also pop open a window when instantiated. You probably don't want that.

--

- **Only one custom class in a given project should inherit from `PApplet`**.

--

- Do not have more than one class do so or you will have many unrelated windows pop open unexpectedly.

---

template: multiple-classes

## Passing around PApplet

It might be the case that you desire to use one of `PApplet`'s functions from within a class that does not inherit from PApplet.

--

- To do so, simply pass an object that does inherit from `PApplet` to that other class.

--

- For example, let's say we have a program that pops open a window and draws a circle and a square that move around randomly on the screen.

--

- Following good object-oriented design principles of **encapsulation** and **abstraction**, we would want separate objects for the circle and the rectangle - each thing should be an object.

--

- Furthermore, we would want each the circle object and the rectangle object to _move and draw themselves_ around the screen.

--

- How can they draw themselves if only one class can inherit from PApplet?

---

template: multiple-classes

## Passing around PApplet (continued)

Define one class that inherits from `PApplet`, and have it pass itself to the other objects.

```java
// ... insert the package and import statements here...
public class App extends PApplet {

  private Circle circle; // a custom class we will define
  private Rectangle rectangle; // a custom class we will define

  // ... insert the main method and settings method go here.

  public void setup() {
    // instantiate the two objects... notice we pass *this*
    this.circle = new Circle(100, 100, this);
    this.rectangle = new Rectangle(100, 100, this);
  }

  public void draw() {
    // have the two objects draw themselves to the screen
    this.circle.draw();
    this.rectangle.draw();
  }
}
```

---

template: multiple-classes

## Passing around PApplet (continued again)

Within the `Circle` and `Rectangle` class constructors, we accept an `App` object that we caan use to draw to the screen.

```java
// ... insert the package statement and any imports here ...
public class Circle {
  private int x; // the x coordinate of this object
  private int y; // the y coordinate of this object
  private App app; // a property that will hold an App object, which inherits from PApplet

  // notice that we accept an App object into the constructor and store it into this object
  public Circle(int x, int y, App app) {
    this.x = x; // ideally we would use a setter that performs some validation
    this.y = y; // ideally we would use a setter that performs some validation
    this.app = app; // this is the trick - store the App object!
  }

  public void draw() {
    this.x = this.x + 2 // change the x coordinate a bit
    this.app.ellipse(this.x, this.y, 100, 100); // using PApplet's draw method!
  }

}
```

---

name: conclusions

# Conclusions

--

Hopefully this has been a pleasant foray into creating frame-based animations in Java using the Processing framework.

--

- Thank you. Bye.
