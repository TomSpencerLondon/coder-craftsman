# The Decorator Pattern #

This is the third blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Observer Pattern** whcih you read here. 

This post will look at the **Decorator Pattern**, which enables you to create a one-to-many dependency where a change in one object results in automatic notification and change in the other objects.

We’ll re-examine the typical overuse of inheritance and you’ll learn how to decorate
your classes at runtime using a form of object composition. Why? Once you know the
techniques of decorating, you’ll be able to give your (or someone else’s) objects new
responsibilities without making any code changes to the underlying classes.

O k ay, h e re’s w hat we k n o w s o f a r.. .
ß Decorators have the same supertype as the objects they decorate.
ß You can use one or more decorators to wrap an object.
ß Given that the decorator has the same supertype as the object it decorates, we can pass
around a decorated object in place of the original (wrapped) object.
ß The decorator adds its own behavior either before and/or after delegating to the object it
decorates to do the rest of the job.
ß Objects can be decorated at any time, so we can decorate objects dynamically at runtime
with as many decorators as we like.

The Decorator Pattern attaches additional
responsibilities to an object dynamically.
Decorators provide a fl exible alternative to
subclassing for extending functionality.

Pg 91
