---
path: "/post-nine"
date: "2019-12-21"
title: "Trees and Graphs"
author: "Tom Spencer"
---

Let’s start with graphs. Every vertice and every edge in every graph has a label. The information we want to store is either in the vertices or the edge. This kind of data structure has an internal order. It is based on a parent child structure.

![graph](https://shapeofdata.files.wordpress.com/2013/08/graphwords.png)


### Trees

A tree is just a graph which has two properties. It has to be connected and there cannot be loops. A loop is three or more vertices connected. If you try to draw it you will get node at the top and branches going down. You cannot go up because going up means looping. These are good models for defining data structures for searching information because everything is connected. In trees the searching process is the fastest. With trees we have the same problems to solve. With graphs connectivity is not a problem. The shortest path is the search process.

We spoke about algorithms for sorting with arrays and stacks but in trees the complexity reduces a bit. One of the most important things about graphs and trees is the problem of finding paths between specific vertices. We can divide this problem into three different problems.

1. A connectivity problem - existence of a path. Are there edges to the vertices?
2. Finding all possible paths - also known as the complete problem - of path finding - we want all the solutions.
3. Optimisation of the path. We want to find the shortest or best path. Shortest in distance or cost.

These 3 are the main path finding problems for graphs and trees. The first two problems are solved by an algorithmic technique called backtracking. These algorithms to find one or other or all of the paths work well for a lot of problems. It seems inefficient but is good in terms of complexity. Backtracking tries to find every solution to a problem by using the best solutions in the process and ignoring the bad solutions. Backtracking takes the solutions that are possible and ignore those that are impossible. We use backtracking when we solve sudoku problems. We fill the boxes according to certain rules. If we have an empty place we can it with 1 and then try possible solutions that have 1 in this position. If we don't find the solution then we can go back to find one + 1. In essence we go back to find different path. This is a good way of resolving finding the solution. You have to go through all the vertices to find the path.

Optimisation is not easy in general. There are three ways of solving this problem:
* Using the backtracking approach
* (Compute all possible paths and choose the most efficient path - path with smallest weight) This is inefficient because you have to go through all possibilities.
* Dijkstra

### Dijkstra algorithm
With Dijkstra we use the concept of a heuristic. We are trying to get informed in the process. We need to find a right direction or at least an approximation to a right destination. It tries to compare and see if the right position of the algorithm is close enough to the goal. With Dijkstra we always try to find the best path by computing some information about how close to the goal we are. This is called informed path finding. We need to know where the goal is.

There are some types of uninformed searching. If presented with a basic graph and no information about where to look some people use a statistical approach. If we want to build random paths ie for vacuum cleaning we have to build paths without a goal. It is has the same spirit in the sense that if you are not informed about the goal. You have to find your way into the graph without knowing where to go. This is path building.

A star path finding is a variation of the Dijkstra algorithm. We need some extra information in each node to reach our goal.

### Depth first search

With **depth first search** we start by searching in the root and then go as deep as we can through the first branch that you find and once this branch has finished you go back to the next sibling and then follow it through. There are 3 ways of doing this: Inorder, Preorder and postorder.
```
                  1    
                /   \
               2     3
              / \
             4   5
```

Depth First Traversals:
(a) Inorder (Left, Root, Right) : 4 2 5 1 3
(b) Preorder (Root, Left, Right) : 1 2 4 5 3
(c) Postorder (Left, Right, Root) : 4 5 2 3 1

Why traverse trees like this? We don’t have a logical order to follow. A graph doesn’t have the concept of a next element. We are trying to build some standard ways of progressing through a tree. If not Binary then we are not guaranteed to have the same system. What are the implementations of the tree searching methods. Most of them have to use linear structures to solve them. List, stack or a queue. Some implementations of the trees use the fact that the RAM memory behaves like a stack and dip into the way of behaving the memory has. Building an empty stack. All the different searches have the same complexity. All of them are valid options for the searching process. What is the time complexity of this stuff?

Let’s suppose we are not using an extra stack but a memory stack. What we are doing at the bottom is just traversing the BST. At most this complexity is O(n) ie linear. Each of these traversing methods can be solved by recursive or iterative methods. When we are using recursive methods we are mostly using the stack. 

If we were to use in order Traversal (Practice) the steps would be as follows:
   1. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2. Visit the root.
   3. Traverse the right subtree, i.e., call Inorder(right-subtree)

Inorder traversal gives nodes in non-decreasing order. To get nodes of BST in non-increasing order, a variation of Inorder traversal where Inorder traversal s reversed can be used. Example: Inorder traversal for the above-given figure is 4 2 5 1 3. The pseudo code for iterative in order algorithm: 1st go to the left child, stack the current vertex into the stack, repeat this process until we get as deep as possible. Unstack elements from the stack. Then print the root and the right element.