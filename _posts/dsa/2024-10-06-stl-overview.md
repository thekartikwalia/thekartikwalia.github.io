---
title: "Standard Template Library (STL) – Overview"
date: 2024-10-06 10:00:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, containers, algorithms]
math: true
---

## Core Concepts for mastering STL
- [Pointers]({% post_url 2024-09-07-pointers %})
- [Array Pointers]({% post_url 2024-09-11-array-pointers %})
- [References]({% post_url 2024-09-07-references %})
- [Templates]({% post_url 2024-09-08-templates %})

## What is STL ?
The Standard Template Library (STL) is a powerful library that provides a set of common classes and functions, including algorithms and data structures like vectors, lists, stacks, queues and more. It is designed to handle generic programming, allowing developers to write code that works with any data type.

__NOTE__
In case you want to optimise on time or you're getting TLE in some problem and you're sure that the logic is correct, if you want to optimise you can try to remove STL from your codes because they're bit more inefficient than the static versions of the code.

## Key components of STL 
1. __Algorithms__
   STL provides wide range of algorithms to perform common operations on data, such as searching, sorting, and manipulating data. These algorithms are implemented as template functions, meaning they can work with any container that supports iterators.
   - [rand()]({% post_url 2024-10-06-stl-rand %})
   - [random_shuffle() and shuffle()]({% post_url 2024-10-06-stl-random-shuffle %})
   - [next_permutation()]({% post_url 2024-10-06-stl-next-permutation %})
   - [lower_bound() and upper_bound()]({% post_url 2024-10-06-stl-lower-upper-bound %})
   - [nth_element()]({% post_url 2024-10-06-stl-nth-element %})
   - [unique()]({% post_url 2024-10-06-stl-unique %})
   - [reverse()]({% post_url 2024-10-06-stl-reverse %})
   - [sort() and Lambda Comparators]({% post_url 2024-10-06-stl-sort-and-lambda-comparators %})
   - [__gcd() and gcd()]({% post_url 2024-10-06-stl-gcd %})
   - [min_element() and max_element()]({% post_url 2024-10-06-stl-min-max-element %})

   For reference, use website [cplusplus](https://cplusplus.com/)
2. __Containers__
   These are data structures like arrays, vectors, linked lists etc. that store collections of objects.
   
   All the containers in the C++ Standard Template Library (STL) are defined as templates. 
   This allows them to be __generic__ and work with any data type. 
   
   We aim to create mental models for how the STL containers should look in one's mind, making it easier to visualise problems and their solutions mentally.
   
   [Mental Models of various Containers]({% post_url 2024-10-07-stl-mental-models-of-various-containers %})
   
   For efficient traversal in various container types, we require [Iterators]({% post_url 2024-10-06-stl-iterators %})
   
   _Various Container Types in STL_
   - [Vector]({% post_url 2024-10-07-stl-vector %})
   - [Stack]({% post_url 2024-10-07-stl-stack %}) 
   - [Queue]({% post_url 2024-10-07-stl-queue %}) 
   - [Priority Queue]({% post_url 2024-10-07-stl-priority-queue %})
   - [Map]({% post_url 2024-10-07-stl-map %})
   - [Set]({% post_url 2024-10-07-stl-set %})
   - [Multiset and Multimap]({% post_url 2024-10-07-stl-multiset-and-multimap %})
   - [Deque]({% post_url 2024-10-07-stl-deque %})
   - [String]({% post_url 2024-10-07-stl-string %})
   
   __NOTE__ : [Push() vs Emplace()]({% post_url 2024-10-07-stl-push-vs-emplace %})
   
   The thing that gives major power to STL is [Nesting]({% post_url 2024-10-07-stl-nesting %})

## Problem Solving Paradigms (PSP)
__Most of the problems you ever counter will belong to one amongst the following paradigms__ 
1. _Brute Force_ : Try all possible solutions and choose the best one, regardless of efficiency
2. _Greedy_ : Make locally optimal choices at each step, hoping to find a global optimum
3. _Divide & Conquer_ : Break the problem into smaller subproblems, solve each independently, and combine the results
4. _Dynamic Programming_ : Recursion/Backtracking with Memory
5. _Graph_ : Solve problems by modeling the relationships between elements as nodes and edges, often using search or traversal algorithms

## Applications of STL 
1. [Budget Problem Variations]({% post_url 2024-10-08-budget-problem-variations %})
3. [Depth Counting]({% post_url 2024-10-08-depth-counting %}) (Both challenge variations remaining)
4. [Algorithmic Design]({% post_url 2024-10-08-algorithmic-design %})
5. Window Maintenance / Sliding Window
6. Subarray Finding