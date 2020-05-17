# The Command Pattern #

This is the sixth blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Singleton Pattern**, which ensures a class has only a single instance and provides a global point of access to it.

The **Command Pattern** encapsulates a command request as an object.

![command pattern](https://user-images.githubusercontent.com/63193195/81503957-7fa2eb80-92de-11ea-8ea5-276f3306829c.jpg)

By encapsulating a request as an object you can parametrise clients with different requests, queue or log requests, and support undoable operations. 

For example, the bill you receive at a restaurant is like a Command Pattern. The waiter or waitress takes an order or command from a customer and encapsulates that order by adding it to the bill. The order is then queued for serving. Note that the pad of "bills" used by each waiter is not dependent on the menu, and therefore they can support commands to cook many different items.

A command object encapsulates a request by binding together a set of actions on a specific receiver. In order to do this, it packages the actions and the receiver up into an object that exposes just one method, execute().

When called, execute() causes the actions to be invoked on the receiver. From the outside, no other objects really know what
actions get performed on what receiver; all they know is that they when they call the execute() method, their request will be serviced.

**How to use the Command Pattern**

So, the Command Pattern decouples the object that invokes the operation from the one that knows how to perform it. To achieve this separation, the designer creates an abstract base class that maps a receiver (an object) with an action (a pointer to a member function). The base class contains an execute() method that simply calls the action on the receiver.

Clients of Command objects treat each object as a "black box" by simply invoking the object's virtual execute() method whenever the client requires the object's "service".

A Command class holds some subset of the following: an object, a method to be applied to the object, and the arguments to be passed when the method is applied. The Command's "execute" method then causes the pieces to come together.

The client that creates a command is not the same client that executes it. This separation provides flexibility in how you time and sequence commands, and making commands objects, enables you to pass, stage, share, load in a table, and otherwise use them like any other object.

To make use of Command:

- You need to define a Command interface with a method signature like execute(). 
- Then create one or more derived classes that encapsulate some a subset such as a "receiver" object, the method to invoke, the arguments to pass. 
- You then instantiate a Command object for each deferred execution request, passing the Command object from the creator to the invoker.
- The invoker decides when to execute(). 

So, looking at Command in java, we can decouple a producer from a consumer:

```
interface Command {
    void execute();
}

class DomesticEngineer implements Command {
    public void execute() {
        System.out.println("take out the trash");
    }
}

class Politician implements Command {
    public void execute() {
        System.out.println("take money from the rich, take votes from the poor");
    }
}

class Programmer implements Command {
    public void execute() {
        System.out.println("sell the bugs, charge extra for the fixes");
    }
}

public class CommandDemo {
    public static List produceRequests() {
        List<Command> queue = new ArrayList<>();
        queue.add(new DomesticEngineer());
        queue.add(new Politician());
        queue.add(new Programmer());
        return queue;
    }

    public static void workOffRequests(List queue) {
        for (Object command : queue) {
            ((Command)command).execute();
        }
    }

    public static void main( String[] args ) {
        List queue = produceRequests();
        workOffRequests(queue);
    }
}
```
```
Output
take out the trash
take money from the rich, take votes from the poor
sell the bugs, charge extra for the fixes
```
Don't forget that Commands give us a way to package a piece of computation (a receiver and a set of actions) and pass it around as a first-class object. The computation itself may be invoked long after some client application creates the command object and may even be be invoked by a different thread. So we can take this scenario and apply it to many useful applications such as schedulers, thread pools and job queues, to name a few. These are just some of the mnay ways Command is useful to us.

The next blog in the series will look at the **Adapter and Facade Pattern**, whcih converts the interface of a class into another interface, thereby matching interfaces of different classes.

