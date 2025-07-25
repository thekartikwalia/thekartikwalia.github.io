---
layout: post
title: "Push vs Emplace in STL"
date: 2024-10-07
categories: dsa
math: true
tags: [STL, C++, push, emplace, containers]
---

## Push() vs Emplace()
`push()` and `emplace` are both used to add elements to containers like `queue`, but they differ in how they handle the insertion of elements.
1. __`push()`__
   - _Usage_: `queue.push(value);`
   - _How it works_: The `push` function creates a copy (or move) of the element and then inserts it into the container.
   - If you pass an object to `push`, it will call the copy constructor (or move constructor if applicable) to create the object before placing it into the container.
   - Example:
		```cpp
		queue<pair<int, int>> q; 
		q.push(make_pair(1, 2));  // Creates a pair, then copies it to the queue.  
		```

2. __`emplace()`__
   - _Usage_: `queue.emplace(args...);`
   - _How it works_: The `emplace` function constructs the element **in place** directly within the container without making a copy or move. It forwards the arguments to the constructor of the element and creates it directly in the container. This avoids an extra copy/move operation and can be more efficient, especially with complex objects.
   - Example:
	    ```cpp
		queue<pair<int, int>> q; 
		q.emplace(1, 2);  // Constructs the pair directly in the queue.
		```   

## Key Differences 
- __Copy vs Direct Construction__
    - `push` requires creating an object first and then copying/moving it into the queue.
    - `emplace` constructs the object directly in place, which can be more efficient for complex objects.
- __Performance__
    - `emplace` can be faster than `push` since it eliminates the need for an extra copy or move.