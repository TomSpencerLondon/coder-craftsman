---
path: "/post-thirteen"
date: "2019-12-25"
title: "Lambdas and threads"
author: "Tom Spencer"
---


Let’s talk a bit about the main purpose of threads. We want to create programs that share information between different parts of the applications. This information should be solid enough so that it won’t get currupted or modified unexpectedly. In the future we will call this concurrent control. A thread is a piece of code that executes independently and only when you invoke it. Independence means that you can execute continuously without being invoked continuously. You tell it to start and it executes until you tell it to stop. Independently also means you can have multiple threads at the same time. This leads to some problems. The problem of concurrency concerns what happens when you have 2 threads running at the same time trying to access the same information at the same time. To manage this problem in the past Java developers used the concept of priority. Every thread has a priority from one to ten. One meaning biggest. Ten the lowest. It means that if two threads collide. The first one that executes is the one with the highest priority. 

Priority has a problem. You want pieces to execute at the same time to use CPU in the most efficient way. Two threads at the same time use different bits of your CPU. If we use priority it means that the CPU is going to execute the thread with the highest priority and then the second. We are not executing in parallel and keep on waiting for them to execute. We are not taking advantage of all the possibility given by threads.

After this, Java developers found another solution. Priority has two ways of being invoked. The first way is we as developers decide by hand and the second way is for the CPU to decide priority through inheritance or interface control. Higher class first, or variables final or static. 

An early solution was to use priorities and a new type of variable which was the variable of synchronising. We have a reserved synchronised keyword which is a non access modifier and this allows us to define how the threads execute our method. 

For example, suppose we have 2 threads trying to write something to a text file at the same time. If these two threads are not synchronised then the final file will be corrupted. Both will handle the same methods and variables and the CPU will not know how to unambiguously execute the task. The thread will fail. 

We define a buffer as a synchronised variable. Doing this means that the CPU knows we want this variable to be synchronised. It lets one of the threads execute first and then the other. The idea for our CPU is that it is much more important to let our synchronised method be accessed in an ordered way. It protects from being modified by two threads that are concurrent unexpectedly. 

#### Why is lambda useful for handling concurrency and threads?

Threads just share variables and methods. Suppose you have a method once you execute from two threads at the same time. If we don’t have a priority defined it means our methods can be ambiguously executed. Instead of letting the threads access our method what we could do is “send a copy of our methods to the threads”.  This solves the problem. The problem was that our threads were trying to execute the same method. The copy of the methods have different references to the methods and send the copies to different threads.

Java is object oriented so every time we execute a method it has to be instantiated. How do we send methods? How do we do it if we have an interface. The way of solving it is the concept of functional programming. Functional programming is the way of creating software that can handle operations with functions. By operations we mean passing them as arguments, putting them in threads or handling them concurrently.

The syntax for functional programming is the syntax of lambda calculus. The person who invented calculus tried to formalise how functions worked. This has a lot to do with functional programming. At some point programming and algorithms is just a branch of mathematics. At University people study algorithms as part of Maths logic courses. There are ways of implementing lambda calculus in programming. We will need to look at this later.

Now, lets introduce some of the fundamentals of lambda calculus in Java eg. Page 4: The Syntax of Lambda Expressions. Chapter 2 of the Java 8 in Action also. As an example suppose we have a function called Foo(){} and this function has n parameters.

Standard version would be:

| Access Modifiers | Non access modifier | Type | name |
| ---------------- | ------------------- | ----------------- | ------------------- |
Public   | static | Int, String, void (any object or class name) | Download
Private | synchronised
Protected | etc. 

Then we write parentheses and the  parameters. Each param has its own type:

```
public void Download (Int parameter1, String parameter2) {
  //// Todo… /// 
}
```
The important point here is that Todo would probably depend on the parameters. 

How can we make this into lambda calculus function?

First we have the parenthesis and params:
```
(Int parameter1, String parameter2) -> /// Todo /// 
```

If it fits in a line we write normally otherwise use curly brackets.

What is the advantage? First we don’t need a name. We can save space in memory. The second advantage is that this method can now be passed into another method so now you can share information about variables and other  methods.

If we look at the length comparator from page 2 of ***Java SE8 for the Really Impatient*** by ***Cay S. Horstmann*** we can see what happens when we write the versions of our functions:
```
class LengthComparator implements Comparator<String> {
  public int compare(String first, String second) {
      return Integer.compare(first.length(), second.length());
    }
}
```
Java is an object oriented language. Every method has to be on an instance of its class.  With lambdas this is not needed any more. We are making our code simpler because we don’t need so many classes:

```
(String first, String second) -> {
  if (first.length() < second.length()) return -1;
  else if (first.length() > second.length()) return 1;
  else return 0;
}
```
On page five they are creating a lambda function with more than one line. The next example shows that we can use lambda functions without parameters. This is not new because we said that functions don’t need to have parameters in general. This is just another way of writing functions. The functions or these pieces of code can be assigned as values to new variables. So these variables now contain the information to execute these methods. And these variables can be passed to other methods. We have assigned the function to an interface to expand the == method.

Sometimes with lambda expressions we don’t need to make the types of parameters explicit. We can just omit them. The idea is that the CPU and the compiler which is an abstraction of this when it executes the code deduces the names of the variables first and second they have to be strings in this case. 

The next important point to remember is method references. There are even shorter ways of creating lambda functions. These shorter ways are ways of referring to methods in a class. We have to create an instance of a class but we don’t need to create a lambda. We use the double colon. 

A good example is the Greeter method on page 9:
```
class Greeter {
  public void greet() {
    System.out.println("Hello, world!"); }
  }

class ConcurrentGreeter extends Greeter { 
  public void greet() {
    Thread t = new Thread(super::greet);
    t.start();
  }
}
```

We add a method on the class. Super::instanceMethod. Super is a reference to the current class in which the method greet is. We then write :: and we then write the name of the class. This is simpler than lambdas. If we pass a function to a parameter it is simpler than lambda expressions. 

In theory our interfaces cannot implement methods. The methods have to be used by classes. Now we can write the content of some methods by using the modifier default. 

Previously the Interfaces in Java when you create them you can only define the names of the method. You couldn’t implement them. You couldn’t specify what they do. The only way to do this was to create a new class implementing the interface and in that class defining what the methods do. 

Now in Java 8 you can create or define classes in the Interface by using the modifier default. On page 14 we see an Interface called Person with a String getName(). This was impossible before because we weren’t allowed to write code in the interface:
```
Default String getName(){ }
```

If we notice, this does not have an access modifier. Any standard method we write has this order. Normal methods have Public static void.This function has:
```
default String getName(){ }
```

Threads in Java are created in two ways. The first way is by creating a class that inherits the class Thread. This class Thread has a method called run and if you want to create a thread to run some code you use override for the method run in the class Thread.

For example suppose you want to run some code:
1st way of creating thread:
```
Class ExampleRunner{
   public static void main(){
      Example ex1 = new Example();
      ex.run();
          } 
}

Class Example extends Thread {
  public void run() {
     // Todo // 
  }


}

Class Thread implements Runnable {
  public void run(){   }
}
```
———————————
2nd way of creating a Thread:
Implementing an Interface called Runnable:
```
class Example implements Runnable {
   Public void run(){
  // code // 
  }
}

Class ExampleRunner{
   public static void main(){
      Thread thread1 = new Thread(new Example);
      thread1.run();
    } 
}
```

These two ways are doing the exactly the same thing but differently. The class Thread always implements the interface Runnable. 

