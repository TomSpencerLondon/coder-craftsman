# Design Patterns

This is the second blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last podcast covered, the **Strategy Pattern** whcih you read here. 

This post will look at the **Observer Pattern**, which enables you to create a one-to-many dependency where a change in one object results in automatic notification and change in the other objects.

## The Observer Pattern

![observer pattern](https://user-images.githubusercontent.com/63193195/80313609-d0e1b400-87e3-11ea-90f9-14184f7f7042.jpg)

The Observer Pattern is one of the most heavily used patterns in the Java Development Kit, and it’s incredibly useful as it allows automatic notification and change in objects when notified by a subject. The observers or objects are dependent on the subject - the "one" in the relationship, so that when the subject’s state changes, the observers get notified. Depending on the type of notification, the observers may also be updated with new values.

This apporach specifies a "pull" interaction model. Instead of the Subject "pushing" what has changed to all Observers, each Observer is responsible for "pulling" its particular "window of interest" from the Subject. 

< Example ome auctions demonstrate this pattern. Each bidder possesses a numbered paddle that is used to indicate a bid. The auctioneer starts the bidding, and "observes" when a paddle is raised to accept the bid. The acceptance of the bid changes the bid price which is broadcast to all of the bidders in the form of a new bid.

There are various ways to implement the Observer Pattern but most revolve around a class design that includes Subject and Observer interfaces.

Let's take a look. 
