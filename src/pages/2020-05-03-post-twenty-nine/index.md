# The Factory Method Pattern #

This is the fourth blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Decorator Pattern**, which attaches additional responsibilities to an object dynamically, enabling you to extend functionality by providing a flexible alternative to subclassing.

This post will look at the **Factory Method Pattern**, which which defines an interface for creating an object, letting subclasses decide which
class to instantiate. 

![factory pattern](https://user-images.githubusercontent.com/63193195/81115292-62a39c80-8f1b-11ea-8179-a4080e0033aa.jpg)

The Factory Method Pattern enables you to establish an interface for creating objects in a superclass, but also allows subclasses to alter the type of objects that will be created. The creation logic for objects is hidden and the newly created object is returned to the client using either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes (using a common interface).

Factory Method makes a design more customisable and can add more complexity. Whereas other design patterns require new classes, it requires a new operation. Factory Method is to creating objects as Template Method is to implementing an algorithm. A superclass specifies all standard and generic behavior (using pure virtual &quot;placeholders&quot; for creation steps), and then delegates the creation details to subclasses that are supplied by the client.

Scheme of Factory Method

Factory Methods enables a static method of a class that returns an object of that class' type, but unlike a constructor, the actual object it returns might be an instance of a subclass and an existing object can be reused, instead of creating a new objec. Factory methods can have different and descriptive names (e.g. Color.make_RGB_color(float red, float green, float blue) and Color.make_HSB_color(float hue, float saturation, float brightness).

To illustrate, we can use an example from the world of toys. Manufacturers of plastic toys process plastic moulding powder, and inject the plastic into moulds of the toy shape. The class of toy (car, action figure, etc.) is determined by the mould.

The client is totally decoupled from the implementation details of derived classes. Polymorphic creation is now possible.</p>

So if we look at the tools to use this patttern, we need a framework to standardise the architectural model for a range of applications, but which allows for individual applications to define their own domain objects and provide for their instantiation.

If you have an inheritance hierarchy that exercises polymorphism, consider adding a polymorphic creation capability by defining a static factory method in the base class.

Design the arguments to the factory method. What qualities or characteristics are necessary and sufficient to identify the correct derived class to instantiate?

Consider designing an internal &quot;object pool&quot; that will allow objects to be reused instead of created from scratch.

Consider making all constructors private or protected.


