---
path: "/post-twenty-three"
date: "2020-04-15"
title: "Liskov Substitution"
author: "Tom Spencer"
---

This is the second in a series of five blogs on the SOLID Design Principles. Read about the first principle, the Single responsibility principle here [title](https://www.example.com), and the second - the Open-closed principle here. 

The **Liskov substitution principle** states that objects in a programme should be replaceable with instances of their subtypes without altering the correctness of that programme.

![Liskov](https://user-images.githubusercontent.com/63193195/79231166-8fedb500-7e5d-11ea-8688-f8f1527e05db.jpg)

One of the harder principles to make sense of, it was first introduced by Barbara Liskov at a 1987 conference keynote address titled Data abstraction and hierarchy. The Liskov substitution principle (LSP) is a particular definition of a subtyping relation, called (strong) behavioral subtyping.

**It can be stated as such:**

If S is a subtype of T, then objects of type T in a programme may be replaced with objects of type S without altering any of the desirable properties of that programme.

**You can express it mathematically as:**

*Let ϕ(x) be a property provable about objects x of type T.
Then ϕ(y) should be true for objects y of type S, where S is a subtype of T.*

**Or to make it simpler, here it is in "duck terms":**

If it looks like a 🦆, quacks like a 🦆 but needs batteries - you probably have the wrong level of abstraction.

This dictates that, for your code to adhere to LSP, all subclasses* must be completely interchangeable with their parent class.

Let's look at an illustration of LSP substitution using a Rectangle Factory:

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
So we can see that through our showArea method this becomes clear.

As we have seen LSP enables us to replace objects in a programme with instances of their subtype without altering the correctness of that programme.

Next we will look at the Interface segregation principle. 
