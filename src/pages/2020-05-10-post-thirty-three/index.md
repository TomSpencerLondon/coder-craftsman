# The Iterator Pattern #

This is the eighth and final blog post in a series on Design Patterns, in which we're looking at some of the most helpful design patterns for your software design.

The last post covered, the **Adapter and Facade Pattern**, which converts the interface of a class into another interface, thereby matching interfaces of different classes.

The **Iterator Pattern** provides a way to access the elements of a collection of objects sequentially without exposing its underlying representation.

![iterator](https://user-images.githubusercontent.com/63193195/81504508-9bf45780-92e1-11ea-893e-b742837a3c5b.jpg)

The Iterator provides ways to access elements of an aggregate object sequentially without exposing the underlying structure of the object. It can be compared with a filing symstem in an office, where the adminstrator creates a set up they understand and can naigate to find the file another member of the office is looking for - they are the "iterator" in this setting. 

The key idea with the Iterator is to take the responsibility for access and traversal out of the aggregate object and put it into an Iterator object, defining a standard traversal protocol. Given that the task of traversal is placed on the iterator object, rather than the aggregate, the aggregate interface and implementation is simpler as responsibility is placed where it should be. 

The Iterator abstraction is fundamental to an emerging technology called "generic programming", which seeks to explicitly separate the notion of "algorithm" from that of "data structure". The idea behind it is to promote component-based development, boost productivity, and reduce configuration management.

**Using the iterator**

The Client uses the Collection class' public interface directly, with access to the Collection's elements encapsulated behind the additional level of abstraction called Iterator. Each Collection derived class knows which Iterator derived class to create and return. After that, the Client relies on the interface defined in the Iterator base class.

To make use of the Iterator, you need to add a create_iterator() method to the "collection" class, and grant the "iterator" class privileged access. Design an "iterator" class that can encapsulate traversal of the "collection" class.

Clients ask the collection object to create an iterator object. Clients use the first(), is_done(), next(), and current_item() protocol to access the elements of the collection class.



Let's take a look at the Iterator in Java, before and after. 

Without Iterator the class SomeClassWithData provides access to its internal data structure. Clients can accidentally or maliciously trash that data structure.

```
class IntegerBox {
    private final List<Integer> list = new ArrayList<>();

    public void add(int in) {
        list.add(in);
    }

    public List getData() {
        return list;
    }
}

public class IteratorDemo {
    public static void main(String[] args) {
        IntegerBox box = new IntegerBox();
        for (int i = 9; i > 0; --i) {
            box.add(i);
        }
        Collection integerList = box.getData();
        for (Object anIntegerList : integerList) {
            System.out.print(anIntegerList + "  ");
        }
        System.out.println();
        integerList.clear();
        integerList = box.getData();
        System.out.println("size of data is: " + integerList.size());
    }
}

Output
1  2  3  4  5  6  7  8  9
size of data is 0

```
If we use Iterator, we take traversal-of-a-collection functionality out of the collection and promote it to "full object status". This simplifies the collection, allows many traversals to be active simultaneously, and decouples collection algorithms from collection data structures.

```
class IntegerBox {
    private List<Integer> list = new ArrayList<>();

    public class Iterator {
        private IntegerBox box;
        private java.util.Iterator iterator;
        private int value;

        public Iterator(IntegerBox integerBox) {
            box = integerBox;
        }

        public void first() {
            iterator = box.list.iterator();
            next();
        }

        public void next() {
            try {
                value = (Integer)iterator.next();
            } catch (NoSuchElementException ex) {
                value =  -1;
            }
        }

        public boolean isDone() {
            return value == -1;
        }

        public int currentValue() {
            return value;
        }
    }

    public void add(int in) {
        list.add(in);
    }

    public Iterator getIterator() {
        return new Iterator(this);
    }
}

public class IteratorDemo {
    public static void main(String[] args) {
        IntegerBox integerBox = new IntegerBox();
        for (int i = 9; i > 0; --i) {
            integerBox.add(i);
        }
        // getData() has been removed.
        // Client has to use Iterator.
        IntegerBox.Iterator firstItr = integerBox.getIterator();
        IntegerBox.Iterator secondItr = integerBox.getIterator();
        for (firstItr.first(); !firstItr.isDone(); firstItr.next()) {
            System.out.print(firstItr.currentValue() + "  ");
        }
        System.out.println();
        // Two simultaneous iterations
        for (firstItr.first(), secondItr.first(); !firstItr.isDone(); firstItr.next(), secondItr.next()) {
            System.out.print(firstItr.currentValue() + " " + secondItr.currentValue() + "  ");
        }
    }
}
```
```
Output
9  8  7  6  5  4  3  2  1
9 9  8 8  7 7  6 6  5 5  4 4  3 3  2 2  1 1
```
Polymorphic Iterators rely on Factory Methods to instantiate the appropriate Iterator subclass. Memento is often used in conjunction with Iterator. An Iterator can use a Memento to capture the state of an iteration. The Iterator stores the Memento internally.
