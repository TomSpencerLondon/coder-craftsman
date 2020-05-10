# The Singleton Pattern #

This is the fifth blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Factory Method Pattern**, which which defines an interface for creating an object, letting subclasses decide which class to instantiate. 

The **Singleton Patter** 

The Singleton Pattern ensures a class has only one
instance, and provides a global point of access to it.

The Singleton Pattern: your ticket to creating one-of-akind
objects, for which there is only one instance. You
might be happy to know that of all patterns, the Singleton is the simplest in terms
of its class diagram; in fact the diagram holds just a single class! But don’t get
too comfortable; despite its simplicity from a class design perspective, we’ll
encounter quite a few bumps and potholes in its implementation. So buckle
up—this one’s not as simple as it seems...

No big surprises there. But, let’s break it down a bit more:
ß What’s really going on here? We’re taking a class and letting it manage a
single instance of itself. We’re also preventing any other class from creating a
new instance on its own. To get an instance, you’ve got to go through the class
itself.
ß We’re also providing a global access point to the instance: whenever you
need an instance, just query the class and it will hand you back the single
instance. As you’ve seen, we can implement this so that the Singleton is created
in a lazy manner, which is especially important for resource intensive objects.

Java’s implementation of the
Singleton Pattern makes use
of a private constructor, a static
method combined with a static
variable.
ß Examine your performance
and resource constraints and
carefully choose an appropriate
Singleton implementation for
multithreaded applications
(and we should consider all
applications multithreaded!).
ß Beware of the double-checked
locking implementation; it is not
thread-safe in versions before
Java 2, version 5.
ß Be careful if you are using
multiple class loaders; this
could defeat the Singleton
implementation and result in
multiple instances.
ß If you are using a JVM earlier
than 1.2, you’ll need to create a
registry of Singletons to defeat
the garbage collector.
