# The Adapter and Facade Pattern #

This is the seventh blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Command Pattern** which encapsulates a command request as an object.

This blog looks at the Adapter and Facade Pattern, whcih converts the interface of a class into another interface, thereby matching interfaces of different classes.

![adaptor and facade](https://user-images.githubusercontent.com/63193195/81504237-0ad0b100-92e0-11ea-965d-dfbff0834bdc.jpg)


The Adapter Pattern converts the interface of a class
into another interface the clients expect. Adapter lets
classes work together that couldn’t otherwise because of
incompatible interfaces.

In this chapter we’re going to attempt such impossible feats as
putting a square peg in a round hole. Sound impossible? Not when we have
Design Patterns. Remember the Decorator Pattern? We wrapped objects to give them new
responsibilities. Now we’re going to wrap some objects with a different purpose: to make their
interfaces look like something they’re not. Why would we do that? So we can adapt a design
expecting one interface to a class that implements a different interface. That’s not all; while
we’re at it, we’re going to look at another pattern that wraps objects to simplify their interface.

You know what the adapter does: it sits in between the plug of your laptop and the
European AC outlet; its job is to adapt the European outlet so that you can plug your
laptop into it and receive power. Or look at it this way: the adapter changes the interface
of the outlet into one that your laptop expects.
Some AC adapters are simple – they only change the shape of the outlet so that it matches
your plug, and they pass the AC current straight through – but other adapters are more
complex internally and may need to step the power up or down to match your devices’
needs.

Facade is just what you need: with the Facade Pattern you can take a complex
subsystem and make it easier to use by implementing a Facade class that
provides one, more reasonable interface. Don’t worry; if you need the power
of the complex subsystem, it’s still there for you to use, but if all you need is a
straightforward interface, the Facade is there for you.

A facade not
only simplifies
an interface, it
decouples a client
from a subsystem
of components.
Facades and
adapters may
wrap multiple
classes, but a
facade’s intent is
to simplify, while
an adapter’s
is to convert
the interface
to something
different.
facade versus adapter
Download at
Okay, that’s the real world, what about object oriented adapters? Well, our OO adapters
play the same role as their real world counterparts: they take an interface and adapt it to
one that a client is expecting.

The adapter acts as the middleman by receiving requests from the client and converting
them into requests that make sense on the vendor classes.

Intent
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
Wrap an existing class with a new interface.
Impedance match an old component to a new system
Problem
An "off the shelf" component offers compelling functionality that you would like to reuse, but its "view of the world" is not compatible with the philosophy and architecture of the system currently being developed.

Discussion
Reuse has always been painful and elusive. One reason has been the tribulation of designing something new, while reusing something old. There is always something not quite right between the old and the new. It may be physical dimensions or misalignment. It may be timing or synchronization. It may be unfortunate assumptions or competing standards.

It is like the problem of inserting a new three-prong electrical plug in an old two-prong wall outlet – some kind of adapter or intermediary is necessary.

Adapter real example

Adapter is about creating an intermediary abstraction that translates, or maps, the old component to the new system. Clients call methods on the Adapter object which redirects them into calls to the legacy component. This strategy can be implemented either with inheritance or with aggregation.

Adapter functions as a wrapper or modifier of an existing class. It provides a different or translated view of that class.

Structure
Below, a legacy Rectangle component's display() method expects to receive "x, y, w, h" parameters. But the client wants to pass "upper left x and y" and "lower right x and y". This incongruity can be reconciled by adding an additional level of indirection – i.e. an Adapter object.

Scheme of Adapter

The Adapter could also be thought of as a "wrapper".

Scheme of Adapter

Example
The Adapter pattern allows otherwise incompatible classes to work together by converting the interface of one class into an interface expected by the clients. Socket wrenches provide an example of the Adapter. A socket attaches to a ratchet, provided that the size of the drive is the same. Typical drive sizes in the United States are 1/2" and 1/4". Obviously, a 1/2" drive ratchet will not fit into a 1/4" drive socket unless an adapter is used. A 1/2" to 1/4" adapter has a 1/2" female connection to fit on the 1/2" drive ratchet, and a 1/4" male connection to fit in the 1/4" drive socket.

Example of Adapter

Check list
Identify the players: the component(s) that want to be accommodated (i.e. the client), and the component that needs to adapt (i.e. the adaptee).
Identify the interface that the client requires.
Design a "wrapper" class that can "impedance match" the adaptee to the client.
The adapter/wrapper class "has a" instance of the adaptee class.
The adapter/wrapper class "maps" the client interface to the adaptee interface.
The client uses (is coupled to) the new interface
Rules of thumb
Adapter makes things work after they're designed; Bridge makes them work before they are.
Bridge is designed up-front to let the abstraction and the implementation vary independently. Adapter is retrofitted to make unrelated classes work together.
Adapter provides a different interface to its subject. Proxy provides the same interface. Decorator provides an enhanced interface.
Adapter is meant to change the interface of an existing object. Decorator enhances another object without changing its interface. Decorator is thus more transparent to the application than an adapter is. As a consequence, Decorator supports recursive composition, which isn't possible with pure Adapters.
Facade defines a new interface, whereas Adapter reuses an old interface. Remember that Adapter makes two existing interfaces work together as opposed to defining an entirely new one.

Adapter in Java: Before and after
Before
Because the interface between Line and Rectangle objects is incompatible, the user has to recover the type of each shape and manually supply the correct arguments.
```
class Line {
    public void draw(int x1, int y1, int x2, int y2) {
        System.out.println("Line from point A(" + x1 + ";" + y1 + "), to point B(" + x2 + ";" + y2 + ")");
    }
}

class Rectangle {
    public void draw(int x, int y, int width, int height) {
        System.out.println("Rectangle with coordinate left-down point (" + x + ";" + y + "), width: " + width
                + ", height: " + height);
    }
}

public class AdapterDemo {
    public static void main(String[] args) {
        Object[] shapes = {new Line(), new Rectangle()};
        int x1 = 10, y1 = 20;
        int x2 = 30, y2 = 60;
        int width = 40, height = 40;
        for (Object shape : shapes) {
            if (shape.getClass().getSimpleName().equals("Line")) {
                ((Line)shape).draw(x1, y1, x2, y2);
            } else if (shape.getClass().getSimpleName().equals("Rectangle")) {
                ((Rectangle)shape).draw(x2, y2, width, height);
            }
        }
    }
}
```
```
Output
Line from point A(10;20), to point B(30;60)
Rectangle with coordinate left-down point (30;60), width: 40, height: 40
```

After
The Adapter's "extra level of indirection" takes care of mapping a user-friendly common interface to legacy-specific peculiar interfaces.
```
interface Shape {
    void draw(int x, int y, int z, int j);
}

class Line {
    public void draw(int x1, int y1, int x2, int y2) {
        System.out.println("Line from point A(" + x1 + ";" + y1 + "), to point B(" + x2 + ";" + y2 + ")");
    }
}

class Rectangle {
    public void draw(int x, int y, int width, int height) {
        System.out.println("Rectangle with coordinate left-down point (" + x + ";" + y + "), width: " + width
                + ", height: " + height);
    }
}

class LineAdapter implements Shape {
    private Line adaptee;

    public LineAdapter(Line line) {
        this.adaptee = line;
    }

    @Override
    public void draw(int x1, int y1, int x2, int y2) {
        adaptee.draw(x1, y1, x2, y2);
    }
}

class RectangleAdapter implements Shape {
    private Rectangle adaptee;

    public RectangleAdapter(Rectangle rectangle) {
        this.adaptee = rectangle;
    }

    @Override
    public void draw(int x1, int y1, int x2, int y2) {
        int x = Math.min(x1, x2);
        int y = Math.min(y1, y2);
        int width = Math.abs(x2 - x1);
        int height = Math.abs(y2 - y1);
        adaptee.draw(x, y, width, height);
    }
}

public class AdapterDemo {
    public static void main(String[] args) {
        Shape[] shapes = {new RectangleAdapter(new Rectangle()),
                          new LineAdapter(new Line())};
        int x1 = 10, y1 = 20;
        int x2 = 30, y2 = 60;
        for (Shape shape : shapes) {
            shape.draw(x1, y1, x2, y2);
        }
    }
}
```
```
Output
Rectangle with coordinate left-down point (10;20), width: 20, height: 40
Line from point A(10;20), to point B(30;60)
```

