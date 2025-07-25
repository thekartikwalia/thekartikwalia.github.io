---
title: "min_element() and max_element()"
date: 2024-10-06 14:00:00 +0530
categories: [DSA]
tags: [cpp, stl, algorithms, minmax, iterator]
math: true
---

## min_element() and max_element()
In C++ STL, `min_element` and `max_element` are functions that are used to find the __minimum__ and __maximum elements__, respectively, in a given range of elements (like arrays, vectors, or lists). Both functions are part of the `<algorithm>` header.

__Key Points__ 
- Both functions work with any container that provides forward iterators, such as `vector`, `list`, or `arrays`
- They both operate in $O(N)$ time complexity
- Custom comparators can be used to define how elements should be compared

## min_element()
__Function Prototype__
```cpp
template<class ForwardIt> ForwardIt min_element(ForwardIt first, ForwardIt last);
```
- _first_ : An iterator pointing to the first element of the range
- _last_ : An iterator pointing to one past the last element of the range

__Return Value__
- Returns an iterator pointing to the smallest element in the specified range
- If the range is empty, it returns `last`

## max_element()
__Function Prototype__
```cpp
`template<class ForwardIt> ForwardIt max_element(ForwardIt first, ForwardIt last);`
```
- _first_ : An iterator pointing to the first element of the range
- _last_ : An iterator pointing to one past the last element of the range

__Return Value__
- Returns an iterator pointing to the largest element in the specified range
- If the range is empty, it returns `last`

## Example with Custom Comparators 
Both functions can also accept a custom comparator to determine how to compare the elements
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;

int main() {
    vector<int> numbers = {-5, 3, -8, 1, 4};

    // Finding the minimum element based on absolute values
    auto min_it = min_element(numbers.begin(), numbers.end(), [](int a, int b) { 
	    return abs(a) < abs(b); 
	});

    if (min_it != numbers.end()) {
        cout << "The minimum element based on absolute value is: " << *min_it << endl;
    }

    // Finding the maximum element based on absolute values
    auto max_it = max_element(numbers.begin(), numbers.end(), [](int a, int b) { 
	    return abs(a) < abs(b); 
	});

    if (max_it != numbers.end()) {
        cout << "The maximum element based on absolute value is: " << *max_it << endl;
    }

    return 0;
}
```
Output 
```cpp
The minimum element based on absolute value is: 1
The maximum element based on absolute value is: -8
```

__NOTE__
1. For `min_element`, 
   By using `abs(a) < abs(b)`, you are asking the function to return the element for which the absolute value is the smallest. Hence, it correctly identifies the minimum based on absolute values.
2. For `max_element`, 
   Again, using `abs(a) < abs(b)` is logical in this context. It means that if the absolute value of `a` is less than that of `b`, then `a` should be considered "less" than `b` in terms of absolute value. Thus, the function will return the element that has the greatest absolute value as the maximum.

__Why Not `abs(a) > abs(b)` for `max_element`?__
If you were to use `abs(a) > abs(b)` for `max_element`, it would cause the function to behave incorrectly. Specifically, it would end up returning the **minimum** absolute value instead of the maximum because you would be saying that an element is "greater" when its absolute value is greater.