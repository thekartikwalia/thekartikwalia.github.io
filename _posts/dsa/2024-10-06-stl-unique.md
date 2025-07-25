---
title: "unique()"
date: 2024-10-06 13:05:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, unique, duplicates]
math: true
---

## unique()
In C++ STL, `unique` is a function that removes __consecutive duplicate elements__ from a sorted or unsorted range. It reorders the range such that only the first occurrence of each element is kept, and all consecutive duplicates are removed. The function does not shrink the container but returns an iterator to the new logical end of the unique elements, allowing you to resize the container manually if needed.

__Syntax__
```cpp
ForwardIterator unique (ForwardIterator first, ForwardIterator last);
ForwardIterator unique (ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
```
- __first__ : Iterator to the first element of the range.
- __last__ : Iterator to the element one-past-the-last in the range.
- __pred__ : (Optional) A binary predicate that defines the condition for determining duplicates.

__Example__
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 2, 2, 3, 4, 4, 4, 5, 6, 6};

    // Using std::unique to remove consecutive duplicates
    auto it = unique(v.begin(), v.end());

    // Resize the vector to remove undefined elements
    v.resize(distance(v.begin(), it));

    cout << "Unique elements: ";
    for (int x : v) {
        cout << x << " ";
    }
    cout << endl;

    return 0;
}
```
Output
```
Unique elements: 1 2 3 4 5 6 
```

## Key Points about `unique()`
1. **Consecutive Duplicates**: `std::unique` only removes **consecutive** duplicates. To use it effectively on an unsorted container, you must first sort the container (if you want all duplicates removed
   ```cpp
   sort(v.begin(), v.end());
	```
2. **In-place Modification**: The function works in-place, modifying the original container. The range after the returned iterator remains unchanged but contains unspecified values, so resizing the container is necessary.
3. **Iterator Returned**: The function returns an iterator to the new end of the unique range. This iterator points to one-past the last unique element.
4. **Custom Predicate**: You can use a custom comparison function to define what constitutes a duplicate.
   ```cpp
   unique(v.begin(), v.end(), [](int a, int b){ return a == b; });
	```
5. **Complexity**: The complexity is O(n), where n is the number of elements in the range.
6. **Use Cases**:
    - Cleaning up sorted data from repeated values
    - Removing duplicates after merging multiple collections
    - To get distinct elements in a range, sort the range first then apply `unique()`