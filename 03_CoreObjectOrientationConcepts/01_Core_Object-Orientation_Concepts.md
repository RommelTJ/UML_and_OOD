# Core Object-Orientation Concepts

## Brief History of Programming

* Computer programs started as non-structured programming (1950s).
  * Code was a sequence of instructions.
  * Hard to maintain or understand (spaghetti code)
* Then came Structure programming (1960s).
  * Breaks down code into logical steps and subroutines.
  * The C programming language is an example.
  * As programs got bigger, it became more complex.
* Then came Object-Oriented Programming (1980s)
  * Split apart program into self-contained objects.
  * An objects functions as a separate program and operates on its own data.

## Objects

* Objects have properties, identity (state), and behaviors.

## The Class

* We need a class to create objects. 
* The blueprint of an object.
* Classes have properties and actions (methods).
* Classes can be packaged into libraries and reused elsewhere.

## Abstraction

* A way of describing complex problems in simple terms by ignoring some details.
* We are naturally good at generalizing things.

## Encapsulation and Data Hiding

* Encapsulation
  * A method to pack together properties and methods in a class.
  * Hiding the gears and the levers.
  * Data Hiding
    * Avoid exposing inner workings of our objects to avoid external interference.
* Useful because we prevent unintended changes to our objects.
* When designing your classes, expose only as much detail as needed.
* A tightly-coupled system, with most of the objects depending on each other is a sign of bad design.
  * Updating or maintaining such a system is a pain.

## Inheritance

* Inheritance means code reuse
* Object-orientation is about granularity and separation of concerns.
* Each class should focus on a set of specific functionalities and do that well.
* Through inheritance, a class can inherit from a class. Subclasses can implement specialized behavior.

## Polymorphism

* Polymorphism is the condition of occurring in many forms.
* Method overriding
  * Subclasses can provide a specialized implementation of a method defined in a superclass.
* Polymorphism is about working freely with instances of many classes that share a common superclass.
