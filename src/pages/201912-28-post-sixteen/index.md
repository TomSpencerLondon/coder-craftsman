---
path: "/post-sixteen"
date: "2019-12-28"
title: "Java Streams"
author: "Tom Spencer"
---

Imagine we have a linear data structure such as a queue a stack or a list and we want to perform an operation on all the elements. We might want this operation to be carried out in 2 parts with 2 different threads to divide the time by 2. 

In order to do this the operation has to be independent of the order. If you are searching for something you can divide a data structure in 2 parts and search for the element in the two parts with different threads to reduce time of searching. 

Sometimes there are problems that cannot be parallised in this way. Suppose we want to find the minimum in a list. Elements of first part and second part are related so we can’t separate the search because we need all the information together and we can’t operate in two threads. 

Streams are the way in which we can perform multithreading in data strucutres. A stream is an abstraction of a linear data structure that can be parallelised. Formally in Java all the linear data structures are collected in a framework called Collections which uses the Iterable interface. 

Now what we want is to define what streams are and how to define a stream. 
What we are doing is copying all the words of the Alice.txt file into a list of strings called words and now the idea of the algorithm is to count how many of these elements have more than 12 characters. They do this by using a standard for loop.

Standard for loops or methods in Java are not going to multithread these problems. This is why Java created streams. The stream is being internally multithreaded. When you use streams the system makes this as efficient as possible. Whenever you use streams the program can decide whether to use threads or not. By default it will use as many threads as you want:
```
public static void main(String[] args) throws IOException {

    List<String> words = Files.readAllLines(Paths.get("src/alice.txt"));
    long count = words.stream().filter(w -> w.length() > 12).count();
    System.out.println(count);
}
```

In the first line we are creating a list of strings called words. Then we go into a standard Java class called files and we are using a method called readAllLines. This method accepts as parameter a string which is the direction of the file we want to read. We pass the direction of the file Alice.txt and the method readAllLines returns a list with all of the words of the file. We store this list into the list words.

So far words is a list with all of the words of the text.

The second line is important because it uses lambda expressions. We transform our list into a stream. This is the words.stream method. After that we apply a filter to the stream. The filter is truthing some elements according to a function which has to be written as a lambda function to be able to pass it to another function.

The confusion is that sometimes when we want to solve problem using linear data structure we sometimes want to use threads.

Streams with lambda expressions let us control the problem with threads. We can do this with every class in the Iterator interface. We cannot use this with trees as they are not in the collections framework. 
