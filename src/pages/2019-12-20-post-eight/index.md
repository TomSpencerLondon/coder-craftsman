---
path: "/post-eight"
date: "2019-12-19"
title: "Types in Java"
author: "Tom Spencer"
---

Java has **primitive** types that are defined in terms of bits in memory and **abstract** types defined by IDE or by us as programmers. Some of the most important abstract types in Java include **String**, **Array**, **Classes** and **Interfaces**. Here we will focus on **String** and **Array** and **Integer**. We can see the data types in Java here:

![types](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20191105111644/Data-types-in-Java.jpg)

Here we are focussing on the Non-Primitive data types **String**, **Array** and **Integer**. 

As a short aside, there are also other abstract classes such as **interface** and **classes**.

An **interface** in the Java programming language is an abstract type that is used to specify a behavior that classes must implement. Starting with Java 8, default and static methods may have implementation in the **interface** definition.

**Classes** and **Objects** in Java are basic concepts of **Object Oriented Programming** which revolve around the real life entities. A **class** is a user defined blueprint or prototype from which objects are created.

Let's now look at **String**. What is a **string**? A string is just a string of characters. It is an array of **primitive types** (in particular the primitive type **char**). Since this is an abstract data type it has a lot of methods and variables that we can access. 

Lets make a list of the methods in the string class. A frequently used method in the **String** class is the method **indexOf**. If we execute
```
class Main {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```
We can see how the String class is referred to within the **Main** class. The main class takes an array of arguments with a public **class** method. In this **public** **static** method that returns nothing (**void**) we print the string "Hello World" to the console.

Whenever we are trying to execute an instance of a class we have to execute its constructor. In Ruby we may write:
```
Car.new.go
```
This is not mandatary but it is a style pattern. There is a subtle difference between the abstract data types and the concept of a class. The abstract data types in general don’t need a constructor to access the properties. Almost every method in the abstract data types is static. This is a design decision by the creators of Java as it makes the methods in the **String** and **Array** classes easier to use.

For a new string in Java we might write:
```
String helloWorld = “Hello World”;
```
Here we are not actually creating an object of that string when we call helloWorld. We are assigning to that object the string "Hello world". Suppose you have another class that we are creating ourselves. We might write: 
```
class HelloWorld = new Class();
```
This is the way you create an object in general. They are almost the same. When we create a new string. String doesn’t have a constructor. It is only there if you want to override it. 

**Integer** class is a wrapper class for the **primitive** type **int** which contains several methods to effectively deal with a int value like converting it to a string representation, and vice-versa. An object of **Integer** class can hold a single **int** value. 

We use data structures and types as the building blocks for problem solving. Most data structures are imported through **iterable**.

The Java **Iterable** interface (java.lang.Iterable) is one of the root interfaces of the **Java Collections API**. A class that implements the Java **Iterable** interface can be iterated with the Java **forEach** loop. By iterating I mean that its internal elements can be iterated.

There are several classes in Java that implement the Java **Iterable** interface. These classes can thus have their internal elements iterated via the Java **forEach** loop. There are also several Java **interfaces** that extend the **Iterable** interface.

The **Collection** interface extends Iterable, so all subtypes of **Collection** also implement the **Iterable** interface. For instance, both the Java **List** and **Set** interfaces extend the **Collection** interface, and thereby also the **Iterable** interface.

Trees are not included in iterable. A binary tree is a recursive data structure where each node can have 2 children at most.

A common type of binary tree is a binary search tree, in which every node has a value that is greater than or equal to the node values in the left sub-tree, and less than or equal to the node values in the right sub-tree.

Here's a quick visual representation of this type of binary tree:

![tree](https://www.baeldung.com/wp-content/uploads/2017/12/Tree-1.jpg)

Unlike **Arrays** and **Strings** trees do not implement the **Iterable** interface. 
Also, unlike **Array** and **linkedList**, binary tree has several ways of traversal. The traversal algorithms are broadly divided into **depth** first and **breadth** first traversal algorithms depending upon how algorithm actually works. As the name suggest, **depth** first explores binary tree towards depth before visiting **sibling**, while **breadth** first visits all nodes in the same level before going to next level, hence it is also known as level order traversal.
