# The Singleton Pattern #

This is the fifth blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered the **Factory Method Pattern**, which defines an interface for creating an object, letting subclasses decide which class to instantiate. 

This blog will look at the **Singleton Patter**, which ensures a class has only a single instance and provides a global point of access to it.

![Singleton](https://user-images.githubusercontent.com/63193195/81503672-d4456700-92dc-11ea-90ed-e936fc76d866.jpg)

The Singleton Pattern enables you to create one-of-akind objects, for which there is only one instance. In terms of its class diagram, it's the simplest of the Desing Patterns because the diagram holds just a single class. But it's not as straightforward as you might assume. 

This pattern is named after the singleton set, which is defined to be a set containing one element. We can compare it with the office of the President of the United States. The United States Constitution specifies the means by which a president is elected, limits the term of office, and defines the order of succession. As a result, there can be at most one active president at any given time. Regardless of the personal identity of the active president, the title, "The President of the United States" is a global point of access that identifies the person in the office.

So with the Singleton, you're taking a class and letting it manage a single instance of itself. This in turn prevents any other class from creating a new instance on its own. To get an instance, you’ve got to go through the class itself.

It also provides a global access point to the instance: whenever you need it, just query the class and it will hand you back the single instancee, this is especially important for resource intensive objects.

The Singleton design pattern is one of the most inappropriately used patterns. Singletons are intended to be used when a class must have exactly one instance, no more, no less. Designers frequently use Singletons in a misguided attempt to replace global variables. A Singleton is, for all intents and purposes, a global variable. The Singleton does not do away with the global; it merely renames it. 

Singleton can be thought of as "just-in-time initialisation" or "initialisation on first use". You need to make the class of the single instance object responsible for creation, initialisation, access, and enforcement. Declare the instance as a private static data member and provide a public static member function that encapsulates all initialisation code, and provides access to the instance.

The client calls the accessor function (using the class name and scope resolution operator) whenever it needs a reference to the single instance.

To make use of the Singleton, you need to meet the following criteria:

- You can't reasonably assign ownership of the single instance 
- You want lazy initialisation 
- Global access is not otherwise provided for 

However, if ownership of the single instance, when and how initialisation occurs, and global access are not issues, Singleton is not the best route. 

**Structure Scheme of Singleton**

To make use of the Singleton Pattern, define a private static attribute in the "single instance" class. Then define a public static accessor function in the class. 

Do "lazy initialisation" (creation on first use) in the accessor function. Define all constructors to be protected or private. Clients can only use the accessor function to  use the Singleton. 

The inner class is referenced no earlier (and therefore loaded no earlier by the class loader) than the moment that getInstance() is called. Thus, this solution is thread-safe without requiring special language constructs (i.e. volatile or synchronised).

```

public class Singleton {
    private Singleton() {}

    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

The advantage of Singleton over global variables is that you are absolutely sure of the number of instances when you use Singleton, and, you can change your mind and manage any number of instances. 

When is Singleton unnecessary? Short answer: most of the time. Long answer: when it's simpler to pass an object resource as a reference to the objects that need it, rather than letting objects access the resource globally. The real problem with Singletons is that they give you such a good excuse not to think carefully about the appropriate visibility of an object. 

In our next blog we look at the Command Pattern, which encapsulates a command request as an object.
