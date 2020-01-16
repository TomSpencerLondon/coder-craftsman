---
path: "/post-eighteen"
date: "2019-12-30"
title: "Collect and Reduce"
author: "Tom Spencer"
---

The function #collect on a string uses methods from an Interface called Collector. Some of the methods in this Interface are for example toList, toSet, toMap and joining (lets you join a joinable object - ie strings or numbers) the method counting method that allows you to count number of elements in the stream. We also have summarising that sums the numbers in the string. We can use the function averaging to compute the average. Whenever we want to use one of these functions we use this structure:

We create the stream(). Then we use .collect(toList) for instance which applies the collector method toList to the stream. We then look at a few examples to use this correctly:
```
Optional<Dish> mostCalorieDish = menu.stream().collect(maxBy(dishCaloriesComparator)); 
```
Here we use maxBy with a comparator to get the dish with the most calories. If we want to use the methods in the collector Interface we need to import the Collector Interface. 

We now look at the Reduce Interface. Almost every method in the Collector Interface we can use in the Reduce Interface but the important point about Reduce is that it lets you use the information in the stream on a primitive type. For example we have functions like sum, count. It lets us pass from a complex data structure to a simple primitive data structure. 
```
.stream()
.reduce(sum(dish::getCalories)
```
This would sum all the calories in the menu. 

We can now look again at Parallel streams.
This is difficult to understand at the beginning. All streams work in parallel if they can. The parallel process is a syntactic parallelism. If for example we want to execute two callbacks or 2 anonymous functions on a specific stream context then sometimes you will need to perform them in parallel for them to work correctly. This is not something you do explicitly. This is a memory issue. Streams need to work in parallel to execute some lambda expressions. 

If we focus on the problem such as searching or sorting an array the parallelism is not automatic it is something you have to tell the CPU to do. To do this we use the parallel stream interface. For example if we want to filter some information from a huge stream we will write:
```
parallelStream().filter(d -> d.getCalories < 400)
```

This line might perform the stream in parallel. Parallel stream tries to use parallel streams but this depends on the number of cores of your processor CPU or
Core processing Unit.

Whenever you run something in parallel each process is run in a different core. It might happen that you don’t have the power to run threads in parallel.

