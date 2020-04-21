# Design Patterns

Welcome to the first in a new blogs series on Design Patterns, in which we'll look at some of the most helpful design patterns, their use and benefits, so that you can use them in your software design.

Design patterns are general, reusable solutions to commonly occurring problems in software designs. They aren’t a finished design that can directly be turned into code, rather they are a description or template you can use to solve a problem in many different contexts. 

This means they can help speed up the development process by as they provide test, proven best practices that you can use, thereby improving code readability and avoiding problems down the line. They also enable the use of common names for software interactions between developers and can be improved over time, making them more robust than ad-hoc designs.

### In this blog series we will cover the following design patterns:
1. **The Strategy Pattern** - Defines a family of algorithms, encapsulates them and makes them interchangeable.
2. **Observer Pattern** - A one-to-many dependency where a change in one object results in automatic notification and change in the other objects.
4. **Factory**
5. **Singleton** - Ensures a class has only a single instance and provides a global point of access to it.
6. **Command** - Encapsulates a command request as an object.
7. **Adapter and facade** - Converts the interface of a class into another interface, thereby matching interfaces of different classes. 
8. **Iterator pattern** - Provides a way to access the elements of a collection of objects sequentially without exposing its underlying representation.

## The Strategy Pattern

The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It enables the algorithm to vary independently from clients that use it. As such, it captures the abstraction in an interface and buries implementation details in derived classes.

Let's explore the Strategy Pattern by looking at an example of some bad code. 

We have Animal.java and Dog.java and Bird.java:

```
public class Animal {
	
	private String name;
	private double height;
	private int weight;
	private String favFood;
	private double speed;
	private String sound;
  
```
  // Instead of using an interface in a traditional way
	// we use an instance variable that is a subclass
	// of the Flys interface.
	
	// Animal doesn't care what flyingType does, it just
	// knows the behavior is available to its subclasses
	
	// This is known as Composition : Instead of inheriting
	// an ability through inheritance the class is composed
	// with Objects with the right ability
	
	// Composition allows you to change the capabilities of 
	// objects at run time!
	
	

A Strategy defines a set of algorithms that can be used interchangeably.

