---
path: "/post-twenty-five"
date: "2020-04-17"
title: "Dependency Inversion Principle"
author: "Tom Spencer"
---

# Dependency Inversion Principle:

This is the final piece in a series of five blogs on the SOLID Design Principles. Read about the fourth principle, the Interface Segregation Principle here [title](https://www.example.com)

The **Dependency Inversion Principle** (DIP), is primarily concerned with decoupling software modules. It states that one should "depend upon abstractions, [not] concretions."

![dependency inversion principle](https://user-images.githubusercontent.com/63193195/79238723-a7ca3680-7e67-11ea-85a3-c1e0423fdedd.jpg)

To elaborate, we can express DIP as follows:

- High-level modules should not depend on low-level modules. Both should depend on abstractions.
- Abstractions should not depend on details. Details should depend on abstractions.

As it dictates that both high-level and low-level objects must depend on the same abstraction, this design principle inverts the way some people may think about object-oriented programming, hence the name.

It sounds a lot more complex than it often is. Adhering to DIP is often a by-product of applying the Open-Closed Principle and the Liskov Substitution Principle to your code. This means that your interfaces are implemented by easily interchangeable concretions that are closed to modification and open to extension.

This is what Robert C Martin said about the principle:

> Consider the implications of high level modules that depend upon low level modules. It is the high level modules that contain the important policy decisions and business models of an application. It is these models that contain the identity of the application. Yet, when these modules depend upon the lower level modules, then changes to the lower level modules can have direct effects upon them; and can force them to change.

As Uncle Bob also states, this may seem unusual to us, given that the high level modules should normally be forcing the low level modules to change. 

Let's have a look at the DIP class to illustrate the point:
```
package DIP;

class Dip {
    public static void main(String[] args) {
        Person parent = new Person("Jakob", Role.PARENT);
        Person child1 = new Person("Alex", Role.CHILD);
        Person child2 = new Person("Anna", Role.CHILD);

        Relationships relationships = new Relationships();
        relationships.addParentAndChild(parent);
        relationships.addParentAndChild(child1);
        relationships.addParentAndChild(child2);

        Research research = new Research(parent, relationships);
        System.out.println(research);

    }
}
```
We are able to create Parent or child with our new Person class and then instantiate a new Research class with parent and relationships. The Person is a POJO:
```
package DIP;

public class Person {
    public String name;
    public Enum role;

    public Person(String name, Enum role) {
        this.name = name;
        this.role = role;
    }
}
```
We also have a role enum:
```
package DIP;

public enum Role {
    PARENT,
    CHILD
}
```
Next we have a RelationshipBrowser interface:
```
package DIP;

import java.util.List;

public interface RelationshipBrowser {
    List<Person> findAllChildrenOf(Person person);
}
```
This is implemented through the Relationship class:
```
package DIP;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

class Relationships implements RelationshipBrowser {
    public List<Person> findAllChildrenOf(Person person) {

        return relations.stream()
                .filter(p -> p.role.equals(Role.CHILD))
                .collect(Collectors.toList());
    }

    private List<Person> relations = new ArrayList<>();

    void addParentAndChild(Person person) {
        relations.add(person);
    }
}
```
We can then use the Research class to print out our information on the relationships:
```
package DIP;

import java.util.List;

public class Research {

    Research(Person parent, RelationshipBrowser browser) {
        List<Person> children = browser.findAllChildrenOf(parent);
        for (Person child : children)
            System.out.println(parent.name + " has a child called " + child.name);
    }

    @Override
    public String toString() {
        return "Research end";
    }
}
```
We can then revisit the DIP to look again at how it is instantiated:
```
package DIP;
s
class Dip {
    public static void main(String[] args) {
        Person parent = new Person("Jakob", Role.PARENT);
        Person child1 = new Person("Alex", Role.CHILD);
        Person child2 = new Person("Anna", Role.CHILD);

        Relationships relationships = new Relationships();
        relationships.addParentAndChild(parent);
        relationships.addParentAndChild(child1);
        relationships.addParentAndChild(child2);

        Research research = new Research(parent, relationships);
        System.out.println(research);

    }
}
```
As we can see, DIP makes our code is more adaptable, more robust and easier to maintain.

This piece rounds up the SOLID design principles blog series. To find out more about SOLID, see the first blog post on the Single Responsibility Principle. 
