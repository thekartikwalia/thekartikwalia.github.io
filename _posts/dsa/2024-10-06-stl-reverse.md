---
title: "reverse()"
date: 2024-10-06 13:10:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, reverse]
math: true
---

## reverse()
In C++ STL, the `reverse()` function is used to reverse the order of elements in a given range. This function is part of the `<algorithm>` header and works with any container that supports bidirectional or random access iterators (such as `vector`, `deque`, `array`, etc.)

__Function Prototype__
```cpp
void reverse(BidirectionalIt first, BiDirectionalIt last);
```
- _first_ : Iterator pointing to the beginning of the range 
- _last_ : Iterator pointing to the end of the range (the position one past the last element)

__Time Complexity__ : $O(N)$, where N is the number of elements in range `[first, last)`.

## Example
```cpp
#include <algorithm>

int main() {
	vector<int> v = {1, 2, 3, 4, 5}

	// Reversing the entire vector 
	reverse(v.begin(), v.end());

	// Reversing a part of the vector (from index 1 to 4)
	reverse(v.begin() + 1, v.begin() + 5);

	return 0;
}
```

## How `reverse()` works ?
- The function works by swapping elements starting from both ends of the range and moving towards the center.
- It requires the container to have bidirectional iterators, which allow moving forward and backward in the range (containers like `list`, `vector`, `deque` support this).