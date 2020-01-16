---
path: "/post-four"
date: "2019-12-16"
title: "Achitecture"
author: "Tom Spencer"
---

Architecture in general for computer software has three parts. The first part is software architecture. The second part is hardware architecture. The third part is the integration of software and hardware. The first part, software architecture includes pattern design. This is particularly well supported in Java because it implements certain patterns that do not exist in other languages.

What is the purpose of a pattern design? A design is just a standard way of solving standard problems. These standard problems were categorised by Java and for each one we implement a pattern to solve the problem.

The Java design patterns can be classified into three big sets. The first set is creational design patterns. With this pattern we are trying to create objects in the most efficient and simple way possible. There are many creational patterns including:
* Singleton Pattern
* Factory Pattern
* Abstract Factory Pattern
* Builder Pattern
* Prototype Pattern

In software engineering, the **singleton** pattern is a software design pattern that restricts the instantiation of a class to one "single" instance. This is useful when exactly one object is needed to coordinate actions across the system. The term comes from the mathematical concept of a singleton.

A **Factory** Pattern or **Factory Method** Pattern says that just define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate. In other words, subclasses are responsible to create the instance of the class. The **Factory Method** Pattern is also known as **Virtual Constructor**.

The **abstract** factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes.

**Builder** is a creational design pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

The second set is what is called the design patterns. These includ the following patterns:
* Adapter Pattern
* Composite Pattern
* Proxy Pattern
* Decorator Pattern

They are trying to create a standard on how to create class relationships and how to work with inheritance.

An **adapter** allows two incompatible interfaces to work together. This is the real-world definition for an **adapter**. Interfaces may be incompatible, but the inner functionality should suit the need. The **adapter** design pattern allows otherwise incompatible classes to work together by converting the interface of one class into an interface expected by the clients.

The **composite** pattern is a partitioning design pattern and describes a group of objects that is treated the same way as a single instance of the same type of object. The intent of a **composite** is to “compose” objects into tree structures to represent part-whole hierarchies. It allows you to have a tree structure and ask each node in the tree structure to perform a task.

A **proxy**, in its most general form, is a class functioning as an interface to something else. The **proxy** could interface to anything: a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate. In short, a proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes.

**Decorator** is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

The third set is what we might call the behavioural design pattern. These patterns are used to address issues such as how everything interacts in a program, how objects interact with each other and how to create more flexibility. These might include:

* Command Pattern
* Iterator Pattern
* Observer Pattern
* State Pattern

The **command** pattern encapsulates a request as an object, thereby letting us parameterize other objects with different requests, queue or log requests, and support undoable operations.

**Iterator Pattern** is a relatively simple and frequently used design pattern. There are a lot of data structures/collections available in every language. Each collection must provide an iterator that lets it iterate through its objects. However while doing so it should make sure that it does not expose its implementation.

The **State** pattern allows an object to change its behavior when its internal state changes. This pattern can be observed in a vending machine. Vending machines have states based on the inventory, amount of currency deposited, the ability to make change, the item selected, etc. When currency is deposited and a selection is made, a vending machine will either deliver a product and no change, deliver a product and change, deliver no product due to insufficient currency on deposit, or deliver no product due to inventory depletion.

The best way of working with a problem is to take a big problem and split it into separate problems. Say you are building web page. We have at least 3 big problems. Firstly the **design** problem. The **design** problem is solved by using CSS files, the second one is ***structural** (how you put the information on the web) via html, and the last one is a **behavioural** problem which you solve by using logic with Javascript. Each one of these problems can be divided into a number of smaller problems. Design could be foreground and background design and components design. The components design can then be divided into smaller problems. 

When we are working with Java specifically all problems can be divided down until they are atomic. If we solve them for one software we can solve them for another problem. Java decided to take a list of the atomic problems and design efficient ways to solve these issues. 

Imagine you are using Java modules for logic in website and you want to connect to the internet. This is a complicated thing to do but one of the things you have to do is control the ports that your computer allows to communicate with the outside. So the steps in order of complexity could be:

* Creating the web (already done!)
* Defining behaviour of a site
* Building a connection
* Managing permissions in the port

The permissions are a few lines of code but there are a few ways of doing it. Java says that you have to use the proxy design pattern. What the proxy does is give access in the program to external software to the database or whatever you need to connect to. You can’t code at random. It has to work in the most efficient way. It not enough to know how to program. It is important to learn how to do this correctly. 

#### Hardware architecture

Software design patterns are not the only part of architecture. We also need to consider **hardware** architecture. **Hardware** architecture has to do with how we connect our hardware units in place. For example if we are a medicare company controlling the incoming and out going of patients we need to be able to connect the **hardware** to the parts of the house or building you are solving problems. For this we need to know something about **networks**. **Networks** has a software and a hardware part and this has to do with the concept of a server both in a real and metaphorical sense. 

**Servers** are made to share information between different units. We are talking now about physical servers - not the abstract concept of server we use in software development.

Most of the time the **hardware** part has nothing to do with us as developers. They connect us to wifi and fix our computers. We need to know a bit of this ie how to put together the software.

When we are working as a programmer in a big company. There are different areas within the company to which we can be directed. New employees might be directed towards software, hardware or integration. Most developers will work in software part. Sometimes we have to go into other teams.

### Integration of software and hardware

We want our software to be specialised enough to work with hardware. Suppose we have the optimum way of running a process. We have to use a hardware to run this system. There should be a correspondence between the time our software is meant to run and the hardware. Once we have computers, lines, etc. We have to modify software to work in efficient way.

Questions regarding hardware might include first how much money do we have to afford specialised hardware? Second how good are the programmers?

A slow machine and good programmer can work. A company could decide go big and buy the best hardware. This would allow them to pay programmers less.

The integration of **hardware** and **software** is a general way of organising software development. You don’t have to be in a big company to use these principles. You have to take into account software, machines and how to integrate them.













