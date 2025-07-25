---
layout: post
title: "Mental Models of Various Containers"
date: 2024-10-07
categories: dsa
math: true
tags: [STL, C++, mental-models, containers]
---


## Pair
A `pair` in C++ STL is used to store two values, which can be of the same or different types.

__Real-life Example__
Storing coordinates (x, y): `pair<int, int>` can be used to store the coordinates of a point in a 2D plane.

__Mental Model__

![pair_mm.jpg](/assets/img/dsa/pair_mm.jpg)

## Vector
A `vector` is a dynamic array that can grow and shrink in size as needed. It allows random access to its elements.

__Real-life Example__
Storing a list of student scores: `vector<int>` can be used to store the test scores of a class of students.

__Mental Model__

![vector_mm.jpeg](/assets/img/dsa/vector_mm.jpeg)

__NOTE__ 
For storing  2-3 values, use pair. Otherwise, use vector 
No need of using tuple 

## Stack
A `stack` follows the **LIFO (Last In, First Out)** principle, where the last element added is the first one to be removed.

__Real-life Example__
Undo operation in text editors: Each action (such as typing or deleting) is pushed onto a stack, and undo operations pop the actions from the stack.

__Mental Model__

![Stack_mm.jpeg](/assets/img/dsa/Stack_mm.jpeg)

## Queue
A `queue` follows the **FIFO (First In, First Out)** principle, where the first element added is the first one to be removed.

__Real-life Example__
Customer service line: Customers are served in the order they arrive, which can be modeled using a `queue<string>`.

__Mental Model__

![Queue_mm.jpeg](/assets/img/dsa/Queue_mm.jpeg)

## Deque
A `deque` is a container where you can add or remove elements from both ends (front or back). It supports both LIFO and FIFO operations.

__Real-life Example__
Browser history navigation: A `deque` can be used to store URLs, where you can navigate forward and backward in your browsing history.

__Mental Model__

![Deque_mm.jpeg](/assets/img/dsa/Deque_mm.jpeg)

## Set
A `set` is a container that stores unique elements in a sorted order. It does not allow duplicates.

__Real-life Example__
Storing a collection of unique email addresses: A `set<string>` can store email addresses to ensure no duplicates are added.

__Mental Model__

![Set_mm.jpeg](/assets/img/dsa/Set_mm.jpeg)

__NOTE__ 
- In general, whenever we have curly braces, we loose the feature of indexing (random access)
- Although set is not subscriptable, but it's iterable

## Map
A `map` stores key-value pairs, where each key is unique, and is used to look up values based on keys. It stores elements in sorted order of keys.

__Real-life Example__
Phone directory: A `map<string, string>` can be used to store names (keys) and their corresponding phone numbers (values).

__Mental Model - 1 (Infinite Sized Array)__

![map_mm1.jpeg](/assets/img/dsa/map_mm1.jpeg)

It's not like intermediate indexes are getting created in reality, it's just a mental model (how it's behaving and not how it's actually implemented)

__Mental Model - 2 (Set of Pairs)__

![map_mm2.jpeg](/assets/img/dsa/map_mm2.jpeg)

Since, it's a set, it'll always remain sorted, hence map are always sorted by the keys (unique)
All keys are unique because if you overwrite something, it'll get overwritten in value also

__NOTE__ : Size is equal to number of keys (as they're unique)

## Priority Queue
A `priority_queue` is a special type of queue where elements are ordered by their priority. By default, it's a max-heap, where the largest element is dequeued first.

__Real-life Example__
Task scheduling system: In a task scheduler, tasks with higher priority are processed before tasks with lower priority.

__Mental Model__

![priorityqueue_mm.jpeg](/assets/img/dsa/priorityqueue_mm.jpeg)

---

## Pending
List : At time of Linked List 
Bitset : At time of Bit Manipulation