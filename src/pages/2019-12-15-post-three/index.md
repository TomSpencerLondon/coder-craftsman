---
path: "/post-three"
date: "2019-12-15"
title: "Java Object Oriented Design"
author: "Tom Spencer"
---

Ruby like Java is a language famous for its use of Object Oriented Design. So in Ruby we might see

```
class Car
  attribute_accessors :petrol
  
  def initialize(petrol)
    @petrol = petrol
  end
end
```
Where `@petrol` is an attribute variable which we can use to store the state of the car. We may wish to use methods on the class like `def drive`. So OOP here is a mixture of state and behaviour. At the most basic level we can use this principle to inherit Car from Vehicle and then also use a Van class etc.

In general in OOP but in particular in Java a class has to be defined in two parts. The first part is the definition of instance variables. The second part is the definition of methods of the class. We only need to define how these attributes and methods behave.

There are two ways of defining behaviour of the elements of a class. In Java we define them by using some prefixes or what are called modifier types. There are two kinds of modifying types as shown in the table below:

Access Modifier | Non Access Modifier | Type
------------ | ------------- | ---
**public**<br>**synchronised**<br>**protected**<br>**private** | **static**<br>**final**<br>**abstract**<br>**synchronised** | **boolean** etc.  

The above table could be useful in looking at the different modifiers and types which we can use on classes.

I also include a visual representation of Java Types for reference:
![Java Types](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20191105111644/Data-types-in-Java.jpg)

### Access modifiers
Access modifiers set the accessibility of methods, attributes and instance variables on a class. The **public** access modifier means that a class is accessible to any other class outside of our class. The **private** access modifier means that whatever you define as a private is only accessible from within the class you define. We are protecting our information from outside the class. We are preventing errors from occurring from outside the class.

We also have the **protected** modifier. Protected means that this information can only be accessed within a **package** and in all sub-classes of the **package**. It is a medium step between **public** and **private**.

The **default** modifier can only be accessed within the package and all sub classes of the package. There are also non-access modifiers. These have nothing to do with access but are useful to create well defined classes. The first one is the **static** modifier. In order to understand what **static** does we need to understand a class and object. Sometimes we need our class to execute some method or have a variable which can be accessed without having to instantiate this class. Whatever you set as **static** means that you can execute or access the information without having to create an object of that class.

If we take the concrete example of the Java class **Integer** we can see that **Integer** has a lot of properties. For instance, it has a method called **parseInt()**. It takes any type and transforms it into a number. To use this you import the class **Integer** then you call it through **Integer.parseInt("1")**. This class method is static and means that we can use methods directly in our code without instantiating classes.

To access a method we can make it **static** or non static. Most methods are non static. We have to announce static methods.

We also have the **final** modifier. This **final** modifier has to do with inheritance. A subclass has all the methods and instance variables of a parent class except for private methods. The idea is that whenever you create something with **final** you cannot access it from any subclass.

In **OOP** we have a chain of classes:

```
Parent -> Child1 -> Child2
```
When we write **final** it means that the method cannot be accessed by the child classes.

We can now look at the **abstract** non access modifier. **static** has to do with access for a method on the class itself. The term **abstract** has to do with another property of classes called **polymorphism**. An **abstract** class is close to an **interface**. It does not impleemnt its methods but forces its children to implement its methods. If I have a class named Car and I defined that class to be **abstract** I could have two types of methods. I could have empty methods and regular methods with full code. The point with empty methods is that the methods can be defined by the subclasses. The subclasses define how to use them. In all object oriented programming parents define how to use the subclasses.

For instance, in Java an **Iterator** class in Java. It has two classes **ArrayList** and **Hashmap**. Both **ArrayList** and **HashMap** are subclasses of the **Iterator** class. The implementation of the loopThrough method is different in each class.

This is a new level of protection because suppose for example we have information about the **abstract** but not about the subclasses. We can therefore protect the code from programmers by organising our code to have levels of protection. We can modify subclasses without modifying the **abstract** classes from that which they inherit.

**abstract** classes can have empty empty and non empty methods. There is a type of **abstract** class which has to have all methods empty. An **interface** is like an **abstract** class but the only difference is that all of its methods have to be empty. If you try to create a method there it will create an error.

The **synchronised** modifier and **volatile** modifier both concern threads. The **synchronised** modifier organises how the class is executed. The **volatile** modifier controls when the thread creates objects of the same class.

### Types

There are actually two types of element. **Primitive** types refer to a location in memory. Here are the types again:

![Java Types](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20191105111644/Data-types-in-Java.jpg)

**Primitive** data types include **boolean**, **int**, **double**, **float** and **char**. There are some others such as **long** and **short** for longer integers but these are less common. Each **primitive** type is a place in memory defined by the number of **bits** that it uses.

A **bit** is just an abstract representation of an electronic part of the boards within a computer. This part is a bit of carbon. The point is that when you pass electricity to it the bit can be turned **on** or **off**. **on** in our abstraction represents the number 1 and **off** is 0. A **boolean** needs one bit because it can only be **on** or **off** or **true** or **false**.

An **Int** on the other hand needs 32 **bits**. Whenever you create a variable of type **Integer** you write:
```
Int integer;
```
The memory reserves a space of 32 bits for the information. This space is reserved for your element. So using elementary maths if we have 32 bits 1 bit is used for the positive or negative sign then there are 31 other bits reserved for the numbers. This means that the number can be a range of +- 2 billion - ie 32 bits or 2 to the power of 32 (...128, 64, 32, 16, 8, 4, 2). This is a lot but imagine we are dealing with more than 2 billion interactions perhaps on Twitter. We therefore use a variable which allows us to access higher numbers. We would then use a **long** which is 2 to the power of 63. This is +-9,223,372,036,854,775,808. All information can be represented by character symbols based on the ascii table:

![ascii table](https://upload.wikimedia.org/wikipedia/commons/d/dd/ASCII-Table.svg)

Every key on our keyboard has a bit and number representation so this allows us to work with characters. If we want to work with more complicated types Java has also introduced the concept of an abstract type.

We as programmers can create our own data types. All of our communication with computers uses bits. When we talk about an abstract data type we are not talking about changing the technology behind primitive types. On a higher abstract level we define a type then the system makes the translation to the bits.

An abstract data type is any class. If we create any class it behaves like a data type. **Integer** is an abstract representation of the primitive type **Int**. **Primitive** types are just places in memory whereas **abstract** types are just huge sets of memory directions that use the same way of sotring infromation but are just more complicated. In general the abstract types have much more properties. They can have methods, data structures and encapsulate state.
