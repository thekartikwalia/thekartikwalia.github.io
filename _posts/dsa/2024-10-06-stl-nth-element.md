---
title: "nth_element()"
date: 2024-10-06 11:05:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, quickselect, sorting]
math: true
---

## nth_element 
The `nth_element()` function in C++ STL partially sorts a range of elements in a way that the element at the `n`-th position is the same as it would be if the range were fully sorted. Elements before this element are less than or equal to it, and elements after are greater than or equal to it.

It actually implements the Quick Select algorithm : $O(N)$
Average Case : $O(N)$
Worst Case : $O(NlogN)$

Also it works like a partition function in Quick Sort

__Syntax__ 
```cpp
void nth_element (RandomAccessIterator first, RandomAccessIterator nth, RandomAccessIterator last);
void nth_element (RandomAccessIterator first, RandomAccessIterator nth, RandomAccessIterator last, Compare comp);
```
- _first_ : Iterator to the first element of the range.
- _nth_ : Iterator to the element that should be at the nth position after partitioning.
- _last_ : Iterator to the element one-past-the-last in the range.
- _comp_ : (Optional) Custom comparator function.


__Example__ 
```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {4, 3, 7, 1, 9, 2, 5};

    // Finding the 3rd element (index 2) as if the array were sorted
    std::nth_element(v.begin(), v.begin() + 2, v.end());

    // The element at position 2 will be the 3rd smallest element
    std::cout << "The 3rd smallest element is: " << v[2] << std::endl;

    // Output the entire vector to show partial order
    std::cout << "Vector after nth_element: ";
    for(int x : v) std::cout << x << " ";
    std::cout << std::endl;

    return 0;
}
```
Output
```
The 3rd smallest element is: 4
Vector after nth_element: 3 1 4 7 9 2 5 
```

## Key Points about `nth_element()`
1. __Partial Sorting__ : `nth_element` only guarantees that the `n`-th element is in its correct sorted position. Elements before are not fully sorted but are less than or equal to the `n`-th element, and elements after are greater than or equal to it.
2. __Time Complexity__ : O(n) on average, where n is the number of elements in the range. This is more efficient than fully sorting the range, which takes O(n log n).
3. __Uses__ : Useful for finding,
    - The k-th largest or smallest element.
    - Median or percentile elements without full sorting.
4. __Custom Comparator__ : You can define a custom comparator to alter the comparison logic. For example, for descending order, use:
   ```cpp
   nth_element(v.begin(), v.begin() + 2, v.end(), greater<int>());
	```
1. __Does Not Modify Entire Range__ : Unlike `sort()`, `nth_element` only rearranges the range partially, which can be useful when you're only interested in the k-th element or a set of top k elements.
2. __Stable Sort__ : `nth_element()` is not stable. If elements are equal, their original relative order might not be preserved.