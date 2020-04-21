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
Rather than use an interface in a traditional way, the Strategy Pattern allows us to use an instance variable that is a subclass of the Flys interface.

Class animal doesn't care what flyingType does, it just recognises that the functionality is available to its subclasses

This concept is known as Composition - instead of inheriting an ability through inheritance, we compose the class with Objects which contain the right ability. This then allows the capabilities of objects to be changed at run time.

```
public Flys flyingType;
	
	public void setName(String newName){ name = newName; }
	public String getName(){ return name; }
	
	public void setHeight(double newHeight){ height = newHeight; }
	public double getHeight(){ return height; }
	
	public void setWeight(int newWeight){ 
		if (newWeight > 0){
			weight = newWeight; 
		} else {
			System.out.println("Weight must be bigger than 0");
		}
	}
	public double getWeight(){ return weight; }
	
	public void setFavFood(String newFavFood){ favFood = newFavFood; }
	public String getFavFood(){ return favFood; }
	
	public void setSpeed(double newSpeed){ speed = newSpeed; }
	public double getSpeed(){ return speed; }
	
	public void setSound(String newSound){ sound = newSound; }
	public String getSound(){ return sound; }
```
That's not the rght apporach. We don't want to add new methods to the super class. What we want is to separate what makes subclasses different from the the super class.

```
	public void fly(){
		
		System.out.println("I'm flying");
		
	}
	*/
	
	// Animal pushes off the responsibility for flying to flyingType
	
	public String tryToFly(){
		
		return flyingType.fly();
		
	}
```
	
So, if we want you want to be able to change the flyingType dynamically we need to do it using the following approach:

```	
	public void setFlyingAbility(Flys newFlyType){
		
		flyingType = newFlyType;
		
	}
	
}
```
```
public class Dog extends Animal{
	
	public void digHole(){
		
		System.out.println("Dug a hole");
		
	}
	
	public Dog(){
		
		super();
		
		setSound("Bark");
		
		// We set the Flys interface polymorphically
		// This sets the behavior as a non-flying Animal
		
		flyingType = new CantFly();
		
	}
	
```
This doesn't quite work either. We need ot make sure to abstract what is different to the subclasses. So we set a constructor to initialise all objects:

```
	* 
	public void fly(){
		
		System.out.println("I can't fly");
		
	}
	*/
	
}
```

```
public class Bird extends Animal{

```
	
	public Bird(){
		
		super();
		
		setSound("Tweet");
		
```
We can then set the Flys interface polymorphically to set the behavior as a non-flying Animal:

```
		
		flyingType = new ItFlys();
		
	}
	
}
```

So then, how do we make Bird.java fly? We need to find a method that continues to abstract out the classes. So we create a Flys interface:

```
// The interface is implemented by many other
// subclasses that allow for many types of flying
// without effecting Animal, or Flys.

// Classes that implement new Flys interface
// subclasses can allow other classes to use
// that code eliminating code duplication

// I'm decoupling : encapsulating the concept that varies

public interface Flys {
	
   String fly();
   
}

// Class used if the Animal can fly

class ItFlys implements Flys{

	public String fly() {
		
		return "Flying High";
		
	}
	
}

//Class used if the Animal can't fly

class CantFly implements Flys{

	public String fly() {
		
		return "I can't fly";
		
	}
	
}
```
	

A Strategy defines a set of algorithms that can be used interchangeably.

