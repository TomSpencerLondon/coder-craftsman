# The Factory Pattern #

This is the fourth blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Decorator Pattern**,

This post will look at the **Factory Pattern**, which which defines an interface for creating an object, letting subclasses decide which
class to instantiate. 

![factory pattern](https://user-images.githubusercontent.com/63193195/81115292-62a39c80-8f1b-11ea-8179-a4080e0033aa.jpg)

As with every factory, the Factory Method Pattern gives us a way to encapsulate the
instantiations of concrete types. Looking at the class diagram below, you can see that the
abstract Creator gives you an interface with a method for creating objects, also known as the
“factory method.” Any other methods implemented in the abstract Creator are written to
operate on products produced by the factory method. Only subclasses actually implement
the factory method and create products.
As in the offi cial defi nition, you’ll often hear developers say that the Factory Method lets
subclasses decide which class to instantiate. They say “decides” not because the pattern
allows subclasses themselves to decide at runtime, but because the creator class is written
without knowledge of the actual products that will be created, which is decided purely by
the choice of the subclass that is used
The Simple Factory isn’t actually a Design Pattern; it’s more of a programming idiom.
But it is commonly used, so we’ll give it a Head First Pattern Honorable Mention.
Some developers do mistake this idiom for the “Factory Pattern,” so the next time
there is an awkward silence between you and another developer, you’ve got a nice
topic to break the ice.
Just because Simple Factory isn’t a REAL pattern doesn’t mean we shouldn’t check out
how it’s put together. Let’s take a look at the class diagram of our new Pizza Store:

a creational pattern that uses factory methods for creating objects without specifying the exact class of object that is created. In factory method pattern the object creation logic is hidden and the newly created object is returned to the client using either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes (using a common interface).

factory method is
abstract so the subclasses
are counted on to handle
object creation.
A factory method may be
parameterized (or not)
to select among several
variations of a product.
A factory method isolates the client (the
code in the superclass, like orderPizza())
from knowing what kind of concrete
Product is actually created.
A factory method returns
a Product that is typically
used within methods defined
in the superclass.
