---
path: "/post-one"
date: "2019-12-13"
title: "Java Programming An introduction"
author: "Tom Spencer"
---

The following is a short summary of my first learnings in Java. In this article I would like to focus on three parts of Java Language. Firstly, Data Structures, i.e. how to organise data in Java. Secondly, I will talk about Threads, as in how Java can be executed. Thirdly, I will talk about Networking with Java, i.e. how we can connect to databases and create servers with Java.

## 1. Data Structures
#### How to organise data into accessible formats.

Java has a number of ways to store and organise information in a localised manner if we are not using a database. Every data structure has two main properties: 1. How accessible it is, 2. How the information can be stored.

The first most basic form of data structure is an array. It is easy to read from an array but difficult to order. You can append items to an array but what if you have an array of numbers and you want to an element in the middle? This is a slow process. So arrays are easy to read but difficult to write. Arrays in Java are static. You have to define the size of the array. For example you are given five spaces for an array (if you have defined it with five spaces). Lists, on the other hand, are not static. Their size is dynamic. You can add as many elements as you want. Lists therefore are effectively arrays with dynamic size.

Queues and stacks are more complex data structures. They are like lists but they have an inherent order which is defined by their names. When we think of queues we might think of waiting in line for service at a bank. The queue here is first in first out. The first person in the queue is the first to get served.

For stacks, on the other hand, we might think of a stack of books. We must take the last book from the stack unless we want it to fall down. So for stacks the rule is first one in, first one out.

Queues and stacks help us to resolve the issue of the ends and beginnings on lists and these structures are very important for serving information to clients. However the middle of the list is still an issue for both queues and stacks.

The issue of the middle of lists can be resolved if we use dictionaries. A dictionary is most efficient at storing information in a specific way. It assigns a label to each bit of data in key and value pairs. For dictionaries in Java in there is no concept of order. we just have a list of keys and we have to know the key to access its values. Reading and writing to dictionaries is very fast. It is just a matter of assigning a label to data and storing the label. We only have to look for a key to read. This is a lot faster than a list.

The data concept of trees on the other hand allows us to have dictionaries with order. For instance we may have a list of clients and want to keep them in order but also be able to query them for who pays the highest fee. This data structure uses the concept of a tree. Every data element has a parent and a child. This is faster than a list because we have an upper node and inner nodes and we can shorten the path to the upper node's children by simply going one step from top to bottom. This makes it more simple to go through all the structures. Here The reading and writing is very fast.
We only look for key to read. This is therefore a lot faster than a list.

In Java it is also possible to combine the data structures. For instance we could have a tree with queue structure putting all the elements of the tree one before the other.

## 2. Threads
#### Multitasking programming for Java. Simultaneous sub programs.

A thread is just a piece of code that executes at run time. Threads unlike loops can execute for ever. They only stop when you tell it to stop. The subtle difference between threads and loops is that loops are static. Loops execute one task at a time and the program waits until it stops before it executes the next one. Threads on the other hand give us the possibility of executing multiple tasks simultaneously. We can therefore complete five two second tasks concurrently so that completing all the tasks takes two minutes. There are problems with threads. In order to execute them we need their processes to be independent. We can't use information from the first thread but can only do this with independent processes. It is possible to create as many threads as you want.

There are other issues with threading. Every thread requires our memory to execute them in a certain priority. RAM can affect the thread speed. We therefore have to be very careful to control how we execute threads. Threads must be synchronised and we have to tell the system exactly what to do. Once we have solved all these problems, however, threads can be very useful. In fact, multi-tasking programming is the most usual way of doing programming.

## 3. Networking with Java
#### Connecting to databases, creating servers.

This topic also involves threading. What happens if we want to make our threads work in an effective way? If you have two threads and these include complicated loops of complex data structures this may overload our memory. One solution is to take the thread to another computer to execute there. Each computer would then execute the thread individually. This then involves the process of connecting computers together. We can therefore multi-task using different computers. Here by connection we mean not only the process of sending information but also synchronisation. We can therefore put our applications on different computers. We synchronise these computers through the concept of a server.

A server is a program that serves information to every user. Here we can use the concept of user server programming. When you want to access procedures or information we can use two procedures, the server and the client (or user).

The server in this relationship is a program that serves information to every user or client. The server controls who can access the information, when and from where. Here we use security to decide who we allow to get in and this depends on good passwords.

The user or client prgram on the other hand requests information. People must never have access to the server program. We should only be able to access the server through client requests.

In layman terms the internet is literally a lot of client programs trying to access servers. Networking is therefore the process of connecting computers. When we talk about urls we are talking about keys to access information from a server domain name.

Urls or uniform resource locations and uris or uniform resource identifiers are keys to access information from a server domain name through an IP address. Every time we use valid url we always get a page. This key is a key to access the server. This doesn't mean that we access all the information from the server. With this key you know where the server is and can make some requests. For instance when we log into a site we request it to give another key. Public servers give us access to all information whereas private servers only give us access when we have a second key for instance a password or Captcha (security validation on a server).

Often it can be useful to learn how to break something in order to know how it works. The most common access programs for servers can include code injection and impersonation.

Code injection can take place through SQL injectioon, HTML or other types of code to introduce bugs to the server. Other more dangerous forms of access can include impersonation i.e. when you create a program that goes between the server and the client. This program makes the server believe it is a client and the client think it is a server. They store information in the middle. One example could include: downloading software from internet with a link to apply. 

Impersonation could include making us think that we are dealing with a bank but then stealing information from our interaction with the 'Bank'.

Code injection simple to solve. We just need to know what people put in forms. We can therefore then say we don’t want backslashes etc. we just want characters. 

Impersonation can be more difficult to protect against. We can double the security on our server, set a password on the Client or enforce self generation of passwords.

