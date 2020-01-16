---
path: "/post-five"
date: "2019-12-17"
title: "Collections in Java"
author: "Tom Spencer"
---



As well as **Array** and **String** many other data structures are implemented through the **Collections** framework in Java. What is a framework in Java? It is a set of classes and interfaces which are connected. This Collection framework has some classes:

![collections](https://www.benchresources.net/wp-content/uploads/2016/08/2-Collection-interace-in-java.png)


The diagram above refers to extends and implements. Extends means that you are creating a subclass of the base class you are extending. You can only extend one class in your child class, but you can implement as many interfaces as you would like.


Arrays are fixed in size and only hold homogenous elements. **Collections** resolve this issue by grouping **Individual** objects. Unlike **Arrays** **Collections** are growable in nature. In a **collection** you can have any type of data element either **homogeneous** or **heterogeneous**.

**Collections** are useful for memory. Memory blocks can be wasted. Collections use memory as per the requirement whereas **Arrays** always use a fixed amount of memory. **Collections** can only hold object types. **Arrays** hold both primitive and object types.

Collections consist of 9 interfaces. Firstly Collection and the sub interface from Collections include **List** from which **ArrayList** is inherited, **LinkedList** and **Vector** with its child **Stack**.

**ArrayList** implements a data structure which is specific. It is implementing an Array. An array is just an ordered organised way of storing data. This data can be accessed by an index. A **LinkedList** is just a data structure in which the elements are not acccessed by an index but connected by a parent child connection. For each connection of a **LinkedList** we have root **node** which connects to the next one and so on.

The next sub interface from **Collection** is **Set**. The insertion order is not preserved in **Set** and no duplicates are allowed. The sub interfaces of **Set** include **HashSet** from which LinkedHashSet inherits and **SortedSet** whose child class is **NavigableSet**. A **set** interface is a set of data which is unordered. It is not only unordered but has no repetitions at all. If we want to store peoples’ ids we might want to use a **Set**.

**NavigableSet** includes navigations such as previous, next etc. **TreeSet** implements the **Navigable** and **SortedSet** interfaces. We then have **Queue** which follows first in first out order. Subclasses of **Queue** include **PriorityQueue** and **BlockingQueue**. **DeQueue** is short for double ended queue. It works exactly as a queue but you can extract elements from top and bottom of the queue. This is like a two sided queue. Both the first and the last element are accessible at the same time. If you have a thread then you can make one of them go for the first one and one of them go for the last one. Then they wouldn’t collide at the same time. 
 
To implement key value pairs we use **Map** which is a part of the **Collection** Framework. The **Map** Interface has **HashMap** with its child interface **LinkedHashMap**, **WeakHashMap**, **IdentityMap** and **Hashtable**. **Hashtable** extends the dictionary class. **SortedMap** and **NavigableMap** are used by **TreeMap**.

A Map is an object that maps keys to values. The Java platform contains three general-purpose **Map** implementations: **HashMap**, **TreeMap**, and **LinkedHashMap**. A map cannot contain duplicate keys: Each key can map to at most one value. It models the mathematical function abstraction. The Map interface includes methods for basic operations (such as put, get, remove, containsKey, containsValue, size, and empty), bulk operations (such as putAll and clear), and collection views (such as keySet, entrySet, and values). **Maps** are perfect to use for key-value association mapping such as dictionaries. The **maps** are used to perform lookups by keys or when someone wants to retrieve and update elements by keys.

In the **Map Interface** we have **Map** and **NavigableMap**. The **Map** is also called **Hash table**, or **dictionary** Java calls it a **Map**. A map stores elements by key value pairs. What is the difference between pairs and navigable map. Navigable Map has an order. What is the problem with this? We require more memory. It requires memory to store the pointers between elements as well as the keys. But it is quicker in the searching process. If we have pointers we can follow paths and store the paths in cache.

### Data Structures

In general a data structure is a way for organising information and the one you choose depends on the problem you are trying to solve. The process of choosing the data structure and algorithms in general is called **solution modelling**. 

Suppose you want to create an algorithm to store the clients of a Lidl store for example. Let’s suppose this store is selling computers and the clients of the computers are sent to the house. The question is what is the best way to store information about the client supposing we have at least 1 million sales.

Suppose we don’t have networking. Suppose we want to use local structures. An **array** in Java means we can only put one data type in this **array**. Suppose one client is a person and another is an institution. You can only put one type of data. None of the elements in the List interface will work. Do we need an order to attend these clients? We could use a queue. What happens if some person says I choose to buy an express sale so I want my product at home tomorrow. We will need access to element not at top. We need a special queue. The type we are looking for is a **priority queue**. This is implemented by an Interface Called **Heap Interface**. This is the general procedure we follow when we use data structures. It may happen that none of the data structures are good enough. We would have to make our own.

The Collection Framework is part of a bigger framework called **Iterable**. Everything in **Iterable** can be iterated and put in a for loop. We cannot put trees in loop. The way we run through a tree depends on the problem.

The **String** Type is just an array of characters. **String** is implementing the Collection Framework because it is an array. Strings are iterable. This means you can put a string into a for loop and extract character by character.
