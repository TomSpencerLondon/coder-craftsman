---
path: "/post-twenty-two"
date: "2020-04-16"
title: "Open Closed Principle"
author: "Tom Spencer"
---

# Open Closed Principle:

This is the second in a series of five blogs on the SOLID Design Principles. Read about the first principle, the Single responsibility principle here [title](https://www.example.com)

The **Open Closed Principle** states that software entities should be open for extension, but closed for modification.

![open closed](https://user-images.githubusercontent.com/63193195/79230176-1bfedd00-7e5c-11ea-9851-ce427a91e1cc.jpg)

Bertrand Meyer first came up with the term “open/closed principle” in the 1980s. What he meant by the principle, was that a module is “open” if it is still available for extension and a module is “closed” if it is available for use by other modules, ie it has been given a well-defined, stable description.

During the 1990s, Robert C. Martin redefined the principle as: "you should be able to extend the behavior of a system without having to modify that system". Meaning interface specifications can be reused through inheritance but implementation doesn’t have to be.

Let's suppose you have written code in one place within your application and that code is now used elsewhere. You want to be able to adapt this to different purposes by writing additional code but not by modifying the code itself. This is because modifying it will likely cause changes to be made everywhere it is used.

This is an example of the Open Closed principle:

```


package OCP;

import java.util.List;

public class Ocp {
    public static void main(String[] args) {
        Product apple = new Product("Apple", Color.RED, Size.SMALL);
        Product tree = new Product("Tree", Color.GREEN, Size.MEDIUM);
        Product house = new Product("House", Color.BLUE, Size.LARGE);

        List<Product> products = List.of(apple, tree, house);
        ImplFilter implFilter = new ImplFilter();

        implFilter.filter(products, new ColorSpecification(Color.GREEN))
                .forEach(p -> System.out.println(p.name + " is green"));

        implFilter.filter(products, new SizeSpecification(Size.LARGE))
                .forEach(p -> System.out.println(p.name + " is large"));

        implFilter.filter(products,
                new AndSpecification<>(new ColorSpecification(Color.BLUE), new SizeSpecification(Size.LARGE)))
                .forEach(p -> System.out.println(p.name + " is large and blue"));
    }
}
```
Here we are able to change the behaviour of each product according to name, colour and size. We can then use different versions of our ColorSpecification, SizeSpecification to show the correct products. This is the POJO of the Product:
```
package OCP;

class Product {
    String name;
    Color color;
    Size size;

    Product(String name, Color color, Size size) {
        this.name = name;
        this.color = color;
        this.size = size;
    }
}
```
Size and colour are enums:
```
  
package OCP;

public enum Size {
    SMALL,
    MEDIUM,
    LARGE,
}
```
Color:
```
package OCP;

public enum Color {
    RED,
    GREEN,
    BLUE
}
```
We then have a filter interface which returns a Stream():
```
package OCP;

import java.util.List;
import java.util.stream.Stream;

public interface Filter<T> {
    Stream<T> filter(List<T> items, Specification<T> spec);
}
```
The implementation of the Filter interface is the following:
```
package OCP;

import java.util.List;
import java.util.stream.Stream;

public class ImplFilter implements Filter<Product> {
    public Stream<Product> filter(List<Product> items, Specification<Product> spec) {
        return items.stream().filter(spec::isSatisfied);
    }
}
```
This then allows us to use different specifications for each type of product:
```
  
package OCP;

public interface Specification<T> {
    boolean isSatisfied(T item);
}
```
Each class is then able to override the isSatisfied() method:
```
package OCP;

public class AndSpecification<T> implements Specification<T> {
    private Specification<T> first, second;

    AndSpecification(Specification<T> first, Specification<T> second) {
        this.first = first;
        this.second = second;
    }

    @Override
    public boolean isSatisfied(T item) {
        return first.isSatisfied(item) && second.isSatisfied(item);
    }
}
```
Here the specification enables us to combine the Specifications:
```
package OCP;

public class ColorSpecification implements Specification<Product>{
    private Color color;

    ColorSpecification(Color color) {
        this.color = color;
    }

    public boolean isSatisfied(Product p) {
        return p.color == color;
    }
}
```
The is the SizeSpecification:
```
package OCP;

public class SizeSpecification  implements Specification<Product>{
    private Size size;

    SizeSpecification(Size size) {
        this.size = size;
    }

    public boolean isSatisfied(Product p) {
        return p.size == size;
    }
}
```
Finally we implement the system in the following manner:
```
package OCP;

import java.util.List;

public class Ocp {
    public static void main(String[] args) {
        Product apple = new Product("Apple", Color.RED, Size.SMALL);
        Product tree = new Product("Tree", Color.GREEN, Size.MEDIUM);
        Product house = new Product("House", Color.BLUE, Size.LARGE);

        List<Product> products = List.of(apple, tree, house);
        ImplFilter implFilter = new ImplFilter();

        implFilter.filter(products, new ColorSpecification(Color.GREEN))
                .forEach(p -> System.out.println(p.name + " is green"));

        implFilter.filter(products, new SizeSpecification(Size.LARGE))
                .forEach(p -> System.out.println(p.name + " is large"));

        implFilter.filter(products,
                new AndSpecification<>(new ColorSpecification(Color.BLUE), new SizeSpecification(Size.LARGE)))
                .forEach(p -> System.out.println(p.name + " is large and blue"));
  ```
We have made sure our code is compliant with the Open Closed principle by using inheritance and implementing interfaces that enable classes to polymorphically substitute for each other.

The next principle is the Liskov substitution principle, read the blog here. 
