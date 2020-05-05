# The Decorator Pattern #

This is the third blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Observer Pattern**,

This post will look at the **Decorator Pattern**, which attaches additional responsibilities to an object dynamically, enabling you to extend functionality by providing a flexible alternative to subclassing.

![Decorator pattern](https://user-images.githubusercontent.com/63193195/81114853-aea21180-8f1a-11ea-9278-8f58362eb6bb.jpg)


By using this pattern you can "decorate" you classes at runtime using a form of object composition. This means you can give your (or someone else’s) objects new responsibilities without having to change any of the code for the underlying classes.

**So, how does the Decorator Pattern work?** 

- Decorators must have the same supertype as objects they decorate.
- You can use one or more decorators to wrap an object.
- You can pass around a decorated object in place of the original (wrapped) object.
- The decorator adds its own behavior before and/or after delegating to the object it's decorating to do the rest of the job.
- You can decorate objects at any time, including dynamically at runtime with as many decorators as we like.

For example, the ornaments that are added to pine or fir trees are examples of Decorators. Lights, garland, candy canes, glass ornaments, etc., can be added to a tree to give it a festive look. The ornaments do not change the tree itself which is recognizable as a Christmas tree regardless of particular ornaments used. As an example of additional functionality, the addition of lights allows one to &quot;light up&quot; a Christmas tree.</p>
<p>Another example: assault gun is a deadly weapon on it's own. But you can apply certain &quot;decorations&quot; to make it more accurate, silent and devastating.</p>

So let's take a look at it in action. 

You neeed to make sure the context is a single core (or non-optional) component with several optional embellishments or wrappers, and an interface that is common to all.

Create a &quot;Lowest Common Denominator&quot; interface that makes all classes interchangeable.

Create a second level base class (Decorator) to support the optional wrapper classes.

The Core class and Decorator class inherit from the LCD interface.

The Decorator class declares a composition relationship to the LCD interface, and this data member is initialised in its constructor.

The Decorator class delegates to the LCD object.

Define a Decorator derived class for each optional embellishment.

Decorator derived classes implement their wrapper functionality - and - delegate to the Decorator base class.

The client configures the type and ordering of Core and Decorator objects.
```
<pre class="hljs"><code><div>Before
Inheritance run amok

class A {
    public void doIt() {
        System.out.print('A');
    }
}

class AwithX extends A {
    public  void doIt() {
        super.doIt();
        doX();
    }

    private void doX() {
        System.out.print('X');
    }
}

class aWithY extends A {
    public void doIt() {
        super.doIt();
        doY();
    }

    public void doY()  {
        System.out.print('Y');
    }
}

class aWithZ extends A {
    public void doIt() {
        super.doIt();
        doZ();
    }

    public void doZ() {
        System.out.print('Z');
    }
}

class AwithXY extends AwithX {
    private aWithY obj = new aWithY();
    public void doIt() {
        super.doIt();
        obj.doY();
    }
}

class AwithXYZ extends AwithX {
    private aWithY obj1 = new aWithY();
    private aWithZ obj2 = new aWithZ();

    public void doIt() {
        super.doIt();
        obj1.doY();
        obj2.doZ();
    }
}

public class DecoratorDemo {
    public static void main(String[] args) {
        A[] array = {new AwithX(), new AwithXY(), new AwithXYZ()};
        for (A a : array) {
            a.doIt();
            System.out.print(&quot;  &quot;);
        }
    }
}

</div></code></pre>
<pre class="hljs"><code><div>After
interface I { 
    void doIt(); 
}

class A implements I { 
    public void doIt() { 
        System.out.print('A'); 
    } 
}

abstract class D implements I {
    private I core;
    public D(I inner) {
        core = inner;
    }

    public void doIt() {
        core.doIt();
    }
}

class X extends D {
    public X(I inner) {
        super(inner);
    }

    public void doIt() {
        super.doIt();
        doX();
    }

    private void doX() {
        System.out.print('X');
    }
}

class Y extends D {
    public Y(I inner) {
        super(inner);
    }

    public void doIt()  {
        super.doIt();
        doY();
    }

    private void doY() {
        System.out.print('Y');
    }
}

class Z extends D {
    public Z(I inner) {
        super(inner);
    }

    public void doIt()  {
        super.doIt();
        doZ();
    }

    private void doZ() {
        System.out.print('Z');
    }
}

public class DecoratorDemo {
    public static void main( String[] args ) {
        I[] array = {new X(new A()), new Y(new X(new A())),
                new Z(new Y(new X(new A())))};
        for (I anArray : array) {
            anArray.doIt();
            System.out.print(&quot;  &quot;);
        }
    }
}
</div></code></pre>
<pre class="hljs"><code><div>Output
AX  AXY  AXYZ
```

So there we have it, a method to attach additional responsibilities to an object dynamically and a flexible alternative to subclassing to extending functionality.

Our next blog looks at the **Factory Pattern**, which handles object creation and encapsulates it in a subclass, decoupling it from the client code in the superclass from the object creation code in the subclass.
