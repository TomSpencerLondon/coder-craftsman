# Design Patterns

This is the second blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last podcast covered, the **Strategy Pattern** whcih you read here. 

This post will look at the **Observer Pattern**, which enables you to create a one-to-many dependency where a change in one object results in automatic notification and change in the other objects.

## The Observer Pattern

![observer pattern](https://user-images.githubusercontent.com/63193195/80313609-d0e1b400-87e3-11ea-90f9-14184f7f7042.jpg)

The Observer Pattern is one of the most heavily used patterns in the Java Development Kit, and it’s incredibly useful as it allows automatic notification and change in objects when notified by a subject. The observers or objects are dependent on the subject - the "one" in the relationship, so that when the subject’s state changes, the observers get notified. Depending on the type of notification, the observers may also be updated with new values.

There are various ways to implement the Observer Pattern but most revolve around a class design that includes Subject and Observer interfaces.

Let's take a look. 
