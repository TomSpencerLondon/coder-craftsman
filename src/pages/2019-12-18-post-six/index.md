---
path: "/post-six"
date: "2019-12-18"
title: "Searching Algorithms"
author: "Tom Spencer"
---

The idea with searching is that most of the time we want to store information and access in a quick way. In general we don’t want to look at alll information to find what we want. We want a fast way to find what we want. For **searching** it is usually best to have the information **sorted** from lowest to greatest key, alphabetically or numerically.

We have way to access algorithm and compare whether algorithm better through **complexity**. Here the concept of **time execution** is important. It depends on the hardware as well as software. It depends on unit of time to be accepted. We usually think in terms of millisecond but for argument we just call these units.

To decide on efficiency we could count the units and then compare. However,depending on the amount of data algorithms can behave in different ways depending on how many elements are in the data structure.

The time to execute an algorithm can depend on the elements in the data structure. Therefore it becomes more difficult to think in terms of units for algorithmic efficiency. This number depends on the amount of data. 

Instead we can use functions to calculate how long an algorithm takes depending on how much data you are processing. So now we compare these functions instead of the numbers themselves. When do we say a function is better than another function? We talk about symptotic behaviour. 

When the amount of data is big enough then the time taken can be smaller for one function than for another one. So algorithms change their behaviour and efficiency depending on the amount of data which they are required to compute. In mathematics we talk about the tendency to **infinity**. Huge amounts of data compare algorithms when they have the maximum possible amounts of data.

A list of most common functions to compare algorithms might include:

1. Linear function denoted as **O(n)**. If you have one million data elements. This will take one million units.

2. Logarithmic function denoted as **O(log n)**.

3. Squared function shown as **O(n^2)**.

4. Linear logarithmic function represented as **O(n * log n)**.

5. Polynomial function (this is a generalisation of the 1st and third functions) - linear functions are polynomial 
**O($n^a$)** where a is a positive number bigger than 1.

Polynomial includes **O<sub>n</sub>**, **O<sub>n</sub>$^2$**, **O<sub>n</sub>$^3$** and so on.

We can see the difference between the different time complexities in the following graph:

![graph of time complexity](https://res.cloudinary.com/practicaldev/image/fetch/s--sMct5uyv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/8ci1gllgkvpo52kj2e7b.png)


Here there is an important distinction between **polynomial** and **non polynomial** functions. **Non Polynomial** functions run faster than **polynomial** ones in general.

So we might ask: **If you have any algorithm with polynomial complexity is it possible to modify this algorithm to make it run with non polynomial complexity?** We don’t know yet. This is one of the biggest problems in mathematics right now and is also a very big economic problem.

When we compare algorithms we are comparing these functions rather than execution time. Which is faster linear or logarithmic function. **O<sub>n</sub>$^2$** is asymptotically slower than **0(n * log<sub>n</sub>)** but it can be faster when we talk about smaller number of elements of data.

Lets talk about the most important algorithms for searching. These can all be assigned a best, average and worst speed and also a space complexity:

![searching](https://devopedia.org/images/article/17/4837.1513922052.jpg)

The most simple search would involve **linear** searching. **Linear** searching is available in lists and arrays. It starts by searching at the root ie the first element in a list. The first element in the data structure. It goes searching one by one through all the elements in the data structure. This is linear searching. Going one by one and looking for the one you want to find. The complexity depends on the data structure. In general this is an O(n) complexity. Each operation takes one unit to execute. For every element it will take one unit of time. 

The other type of searching process is the **interval** search. The point of this search is that this is much more efficient. This algorithm involves going to the middle of the data structure and divide the data structures into two or more parts. The searches can execute in separate threads and this can improve the time. **Interval** searches don’t have to look one by one but look up multiple elements at the same time. They can also use **recursive** algorithms. **Binary** search is the most famous form of **interval** search. The most efficient form of binary search is a **Binary Search Tree**. **Binary Search Tree** is a node-based binary tree data structure.

### Binary search on an array.

Take array and divide into two parts. If the value you are looking for is less than you found in the middle it means that it is in the first part. This is Newton process mathematics invented when he was trying to create algorithm to find the roots of **polynomials**. If you have a **polynomial** you take a **value** and then you try to find another value close to it that has a smaller value than first one.

What is the complexity of the binary search in general. In general binary search is **O(log <sub>n</sub>)**.

### Exponentiation

The basis of mechanical systems is **exponentiation**. We have bits and the data we can create with **n bits** is **2$^n$**. Sometimes we need to know the inverse of exponentiation. What is the value for **2$^n$ = ??**. Logarithms help us find exponents. 

If you are familiar with the exponential function **b$^n$ = M** its logarithmic equivalence is **log <sub>b</sub> * M = N. These two seemingly different equations are in fact the same or equivalent in every way. Look at their relationship using the definition below.

Logarithms are infinite but always work towards a ceiling. Logarithmic functions mean that once you get to a certain data set it doesn’t matter if you 1 million or 10 million the efficiency will always remain the same. Exponentiation is exactly the opposite. Polynomial or exponential algorithms are much slower when you use a little bit more data. Java uses the word log with base **e**. **e** is a constant (roughly 2.71828) which makes it easier to talk about log numbers when calculating algorithmic efficiency. 


### Exponentiation and economics

It may help to think about money in terms of exponentiation. Here exponentiation is a ratio of money to be added. Take money you have and add ratio:

**a + **$\frac{A}{n}$** = A * (1 + **$\frac{1}{n}$**)**

Put money in bank for another year and the equation looks like this:

**a + **$\frac{A}{n}$** + **$\frac{A}{n}$** = A * (1 + **$\frac{1}{n}$**)**

Therefore we can describe this as:

A * (1 + $\frac{1}{n}$)$^k$

Suppose k = n * x then the equation would be:
A * (! + $/frac{1}{n}$)$^n$$^x$

If you make n go to infinity then you get 2.719 = e

Velocity of x. The answer is e$^x$. The function is its own velocity. It is the only function which is its own velocity.

Before we go into sorting algorithms it is important to go into Searching algorithms. We need to make order in the data structure. What happens if want to search in undordered search.

Interpolation search is an example of modified binary search. Same as binary in terms of splitting. But since not sorted use a formula to know what to choose. This is an approximation you can use in statistic tools. Eg confidence intervals. If we don’t have order we don’t know where to split. In the worst possible case. None of guesses find what looking but then get linear search. Best case find at first attempt. Best better than binary search. 

There are a few more ways of searching. You probably want to define a particular way of searching. Most of the ways of searching are easy to perform. We have iterables interface in Java. So basically we have those functions. At least we have linear search that is what iterable is. Binary search is find middle then iterate. Obviously you have to write the code to find the binary search not already done. All the tools. Index. Line method all included in interface. 

Probably if you want to perform a different search you need some other statistical tools. Tools not included in collection framework code would be more complicated. For example with interpolation search in order to predict where elements are we need calculation on a mean, normalisation. We would need to import statistical tool. 

With Python this is easy with Pandas. In java it is more difficult. Java was not created for statistic computations. It was created to perform multitasking with object oriented models. Python is almost as simple as Java but data structures are much more efficient than Java. Programming languages are classified in terms of levels. Programming languages are levelled in terms of how close to machine language:

* C is low level

* Python is high level and Java are roughly the same level.

The closer to human language the processor takes longer to process code. It has to not only compile but translate.

**C** code is the best low level language we have. If we have a program in Java and can’t optimise any further we then put it in C also.

**PhP** worse language ever. Every other language - has some pros. PhP designed as hypertext language similar to HTML then too lazy. Introduced code for logic. Incompatibilities. No single responsibility not in way React works. Different teams doing stuff at same time. Some code that is cannon you have to use but they are inefficient. They have to use PhP - but don’t like it. Java was well designed by Oracle. Team thought carefully how to design the language.

It has advantages and disadvantages. Complexity as high level language Java is heavy.