---
title: "unique()"
date: 2024-10-06 13:15:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, unique, duplicates]
math: true
---

## Iterators 
__Iterators__ in C++ Standard Template Library (STL) are objects that act as pointers to elements within containers, allowing traversal and manipulation of the container's elements. They are a crucial part of the STL as they provide a uniform way to access elements of different container types (like `vector`, `set`, `map`, etc.).

__Mental Model__

![Iterators_mm.jpeg](/assets/img/dsa/Iterators_mm.jpeg)

__Looping using Iterators__
```cpp
vector<int> arr = {3, 2, 5, 7};

for(auto x:arr) {
	cout << x << " ";
}
cout << '\n';

// Alternate way 
for(int x:arr) {
	cout << x << " ";
}
```

## Key Concepts of Iterators 
1. __Pointer-like Behavior__: Iterators behave like pointers in that you can dereference them to access the elements they point to. They can be incremented (or decremented, depending on the iterator type) to move through the container.
2. __Container Agnostic__: Iterators provide a generic interface to traverse containers, meaning the same logic can be applied to different types of containers (e.g., `vector`, `set`, `map`) without needing container-specific traversal logic.
3. __Iterator Categories__: There are different types of iterators, each with different levels of capabilities:
    - _Input Iterators_: Can only read the data, and are used for single-pass algorithms.
    - _Output Iterators_: Can only write data.
    - _Forward Iterators_: Can read/write data and can move forward (used in `forward_list`).
    - _Bidirectional Iterators_: Can move forward and backward (used in `list`, `set`, `map`).
    - _Random Access Iterators_: Can move directly to any element (used in `vector`, `deque`, `array`).
4. __Iterator Functions__: Iterators are used with common STL functions such as:
    - `begin()`: Returns an iterator pointing to the first element.
    - `end()`: Returns an iterator pointing one past the last element (not the last element itself).
    - `rbegin()`: Returns a reverse iterator starting from the last element.
    - `rend()`: Returns a reverse iterator pointing to one before the first element.

## Types of Iterators 
1. __Forward Iterator__:
   Can only move in one direction (forward).
   Can be used with containers like `forward_list`.
   ```cpp
   forward_list<int> fl = {1, 2, 3}; 
   forward_list<int>::iterator it = fl.begin();
	```
	
1. __Bidirectional Iterator__:
   Can move both forward and backward.
   Used with containers like `list`, `set`, `map`.
   ```cpp
   list<int> lst = {1, 2, 3}; 
   list<int>::iterator it = lst.begin();
	```
    
3. __Random Access Iterator__:
   Can directly access any element, like an array index (`it + 3` for the 4th element).
   Used with containers like `vector`, `deque`, and `array`.
   ```cpp
   vector<int> vec = {1, 2, 3, 4, 5}; 
   vector<int>::iterator it = vec.begin(); 
   cout << *(it + 2);  // Outputs 3
	```
    
4. __Reverse Iterator__:
   Used to traverse containers from the end to the beginning.
   Common in containers like `vector`, `deque`, `list`.
   ```cpp
	vector<int> vec = {1, 2, 3, 4, 5}; 
	for (vector<int>::reverse_iterator rit = vec.rbegin(); rit != vec.rend(); ++rit) {  
		cout << *rit << " ";  // Output: 5 4 3 2 1 
	}
	```

## Advantages of Using Iterators
1. __Container Independence__: Iterators provide a common way to traverse different types of containers, allowing algorithms to be written in a container-agnostic manner.
2. __Efficiency__: Iterators are lightweight and efficient for accessing elements, especially in containers that don't support direct indexing (e.g., `list`, `set`).
3. __Flexibility__: They offer flexibility in traversing and modifying containers, including forward and backward traversal, and even random access in certain cases.
4. __STL Algorithm Compatibility__: Many STL algorithms (`std::sort`, `std::find`, etc.) rely on iterators, making them central to how STL operates.