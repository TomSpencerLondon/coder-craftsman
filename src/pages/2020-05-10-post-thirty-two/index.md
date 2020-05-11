# The Adapter and Facade Pattern #

This is the seventh blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Command Pattern** which encapsulates a command request as an object.

This blog looks at the **Adapter and Facade Pattern**, which converts the interface of a class into another interface, thereby matching interfaces of different classes.

![adaptor and facade](https://user-images.githubusercontent.com/63193195/81504237-0ad0b100-92e0-11ea-965d-dfbff0834bdc.jpg)

So looking at the Adapter Pattern first. It's a method which converts the interface of a class into another interface the clients expect, letting classes work together, which ordinarily wouldn't work due to their incompatible interfaces. 

Hence the name "adapter" - it functions in the way an adapter you take on holiday with you functions - it adapts the plug on a device to a foreign plug socket of another shape. Or in other words, the adapter changes the interface of the outlet into one that your device expects and can use. 

Or imagine it as fitting a square peg in a round hole. Like the Decorator Pattern, where we wrapped objects to give them new
responsibilities. Adapter let's us wrap some objects with a different purpose: to make their interfaces look like something they’re not. 
It means we can adapt a design expecting one interface to a class that implements a different interface. T

Coming onto Facade. Whilst some plug AC adapters are simple, only changing the shape of the socket so that it matches your plug, other have more complexity internally and may need to alter the power to suit your device. With the Facade Pattern you can take a complex
subsystem and make it easier to use by implementing a Facade class that provides one, more reasonable interface. 
straightforward interface, the Facade is there for you. What's more, a Facade not only simplifies an interface, it decouples a client from a subsystem of components.

To clarify the difference, Facades and Adapters wrap multiple classes, but a Facade’s intent is to simplify, while an Adapter’s is to convert the interface into something different.

Putting it into the world of Object Orientated coding, an Adapter receives requests from clients and converts them into requests that make sense on the vendor classes.

Adapters lets classes work together that couldn't otherwise, including wrapping an existing class with a new interface where you're trying to use an old component in a new system. So it lets you reuse older parts of the code to avoid reinventing the wheel. 

How to use Adapter and Facade

Below, a legacy Rectangle component's display() method expects to receive "x, y, w, h" parameters. But the client wants to pass "upper left x and y" and "lower right x and y". This incongruity can be reconciled by adding an additional level of indirection – i.e. an Adapter object.

So, to implement this pattern, you need to do the following:
- You need to identify the players: the component(s) that you want to accommodate (i.e. the client), and the component that needs to adapt (i.e. the adaptee).
- Then identify the interface that the client requires.
- Design a "wrapper" class that can "impedance match" the adaptee to the client.
- The adapter/wrapper class "has a" instance of the adaptee class.
- The adapter/wrapper class "maps" the client interface to the adaptee interface.
- The client uses (is coupled to) the new interface

Let's look at Adapter in Java, before and after.

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

By using the Adapter its "extra level of indirection" maps a user-friendly common interface to legacy-specific peculiar interfaces.
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
So, that's how we make use of the Adapter. It can seem quite similar to other patterns, so let's quickly differentiate from some of the obvious comparisons:

- An Adapter makes things work after they're designed whereas a Bridge makes them work before they are. Bridge is designed up-front to let the abstraction and the implementation vary independently whilst Adapter is retrofitted to make unrelated classes work together.

- Adapter provides a different interface to its subject whereas Proxy provides the same interface. 

- Decorator provides an enhanced interface, whereas Adapter is about changing the interface of an existing object. Decorator also enhances another object without changing its interface and is thus more transparent to the application than an adapter is. As a consequence, Decorator supports recursive composition, which isn't possible with pure Adapters.

In essence, Adapter makes two existing interfaces work together as opposed to defining an entirely new one. Facade defines a new interface, whereas Adapter reuses an old interface. 

The next and final blog in our series with focus on the **Iterator Pattern**, which provides a way to access the elements of a collection of objects sequentially without exposing its underlying representation.
