# Liskov substitution principle


The **Liskov substitution princip** is one of the harder principles to conceptualise. It was First introduced by Barbara Liskov, in a 1987 conference keynote address titled Data abstraction and hierarchy, the Liskov substitution principle (LSP) is a particular definition of a subtyping relation, called (strong) behavioral subtyping.

It can be stated as such:

If S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program

Or in duck terms:

If it looks like a 🦆, quacks like a 🦆 but needs batteries - you probably have the wrong level of abstraction

This dictates that, for your code to adhere to LSP, all subclasses* must be completely interchangeable with their parent class.
```
Here we have an illustration of Liskov substitution using a Rectangle Factory:
```
package LSP;

public class Lsp {
    public static void main(String[] args) {
        Rectangle rectangle = RectangleFactory.newRectangle(2, 4);
        Rectangle square = RectangleFactory.newSquare(4);

        showArea(rectangle);
        showArea(square);
    }

    private static void showArea(Rectangle figure) {
        System.out.println("Expected area is " + figure.getArea() + " for " + figure.toString());
    }
}
```
Here the RectangleFactory returns a square or rectangle depending on what we require in the client:
```
package LSP;

public class RectangleFactory {
    public static Rectangle newSquare(int side) {
        return new Rectangle(side, side);
    }

    public static Rectangle newRectangle(int width, int height) {
        return new Rectangle(width, height);
    }
}
```
This is the Rectangle itself:
```
package LSP;

public class Rectangle {
    private int width, height;

    Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    int getArea() {
        return width * height;
    }

    @Override
    public String toString() {
        return "Figure(" +
                "width=" + width +
                ", height=" + height +
                ')';
    }
}
```
We can then create a Rectangle or a Square depending on what we send to the Factory and each instance is interchangeable:
```
package LSP;

public class Lsp {
    public static void main(String[] args) {
        Rectangle rectangle = RectangleFactory.newRectangle(2, 4);
        Rectangle square = RectangleFactory.newSquare(4);

        showArea(rectangle);
        showArea(square);
    }

    private static void showArea(Rectangle figure) {
        System.out.println("Expected area is " + figure.getArea() + " for " + figure.toString());
    }
}
```
through our showArea method.
