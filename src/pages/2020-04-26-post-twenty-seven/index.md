---
path: "/post-twenty-seven"
date: "2020-04-17"
title: "Observer Pattern"
author: "Tom Spencer"
---

This is the second blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Strategy Pattern** whcih you read here. 

This post will look at the **Observer Pattern**, which enables you to create a one-to-many dependency where a change in one object results in automatic notification and change in the other objects.

## The Observer Pattern

![observer pattern](https://user-images.githubusercontent.com/63193195/80313609-d0e1b400-87e3-11ea-90f9-14184f7f7042.jpg)

The Observer Pattern is one of the most heavily used patterns in the Java Development Kit, and it’s incredibly useful as it allows automatic notification and change in objects when notified by a subject. The observers or objects are dependent on the subject - the "one" in the relationship, so that when the subject’s state changes, the observers get notified. Depending on the type of notification, the observers may also be updated with new values.

This apporach specifies a "pull" interaction model. Instead of the Subject "pushing" what has changed to all Observers, each Observer is responsible for "pulling" its particular "window of interest" from the Subject. 

< Example ome auctions demonstrate this pattern. Each bidder possesses a numbered paddle that is used to indicate a bid. The auctioneer starts the bidding, and "observes" when a paddle is raised to accept the bid. The acceptance of the bid changes the bid price which is broadcast to all of the bidders in the form of a new bid.

There are various ways to implement the Observer Pattern but most revolve around a class design that includes Subject and Observer interfaces.

Let's take a look. 

This is the Main method:
```
package BehavioralDesignPatterns.Observer;

class Main implements Observer<Person> {

    private Main() {
        Person person = new Person();
        person.subscribe(this);

        for (int i = 1; i < 3; ++i) {
            person.setId(i);
        }

        for (int i = 24; i < 26; ++i) {
            person.setAge(i);
        }
    }

    public static void main(String[] args) {
        new Main();
    }

    @Override
    public void handle(PropertyChangedEventArgs<Person> args) {
        System.out.println("Class: " + args.source.getClass().getSimpleName() + ", Property: " + args.propertyName.toLowerCase());
        System.out.println("Person's " + args.propertyName + " has been changed to " + args.newValue);
    }
}
```
We've now been able to create a Person class which we can call person.subscribe(this). We've used the handle method for this. We also need an Observable interface:
```
package BehavioralDesignPatterns.Observer;

import java.util.ArrayList;
import java.util.List;

class Observable<T> {
    private List<Observer<T>> observers = new ArrayList<>();

    void subscribe(Observer<T> observer) {
        observers.add(observer);
    }

    void propertyChanged(T source, String propertyName, Object newValue) {
        for (Observer<T> o : observers) {
            o.handle(new PropertyChangedEventArgs<>(source, propertyName, newValue));
        }
    }
}
```
This is the Observer interface:
```
package BehavioralDesignPatterns.Observer;

interface Observer<T> {
    void handle(PropertyChangedEventArgs<T> args);
}
```
We can now show the Person Class extending the Observable interface:
```
  
package BehavioralDesignPatterns.Observer;

class Person extends Observable<Person> {
    private int age;
    private int id;

    void setId(int id) {
        if (this.id == id) {
            return;
        }
        this.id = id;
        propertyChanged(this, "id", id);
    }

    void setAge(int age) {
        if (this.age == age) {
            return;
        }
        this.age = age;
        propertyChanged(this, "age", age);
    }
}
```
This is the PropertyChangedEventArgs:
```
package BehavioralDesignPatterns.Observer;

class PropertyChangedEventArgs<T> {
    T source;
    String propertyName;
    Object newValue;

    PropertyChangedEventArgs(T source, String propertyName, Object newValue) {
        this.source = source;
        this.propertyName = propertyName;
        this.newValue = newValue;
    }
}
```
We have now created one-to-many dependency where a change in one object - Person Class results in automatic notification and change in the other objects, such as Property Class. 

The next design pattern we cover is the Decorator Pattern.
