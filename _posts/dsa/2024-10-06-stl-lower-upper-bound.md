---
title: "lower_bound() and upper_bound()"
date: 2024-10-06 11:00:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, binary-search]
math: true
---

## lower_bound() and upper_bound()
In C++ STL, `lower_bound` and `upper_bound` are 2 functions used to find elements or positions in sorted sequences (like `arrays`, `vectors`, or other sorted containers). Both functions are part of the `<algorithm>` header and are commonly used with containers that support __random access iterators__.

## lower_bound()
The `lower_bound()` function returns an iterator pointing to the __first element__ in the range that is __not less than__ the specified value (i.e., it is greater than or equal to the given value).

__Syntax__ :
```cpp
RandomIt lower_bound(RandomIt first, RandomIt last, const T& value);
```
- _first_ : Iterator pointing to the start of the range 
- _last_ : Iterator pointing to the end of the range (the position one past the last element)
- _value_ : The value to search for 

__Example__ :
```cpp
int main() {
	vector<int> v = {1, 3, ,3, 7, 9};
	auto it = lower_bound(v.begin(), v.end(), 3);

	// Print index and value of the lower bound 
	cout << "LB of 3 is at index: " << it - v.begin() << ", value: " << *it << endl;
	// Output: LB of 3 is at index: 1, value: 3

	return 0;
}
```
In this example, `lower_bound` returns the iterator to the 1st occurrence of 3, or the position where 3 would be inserted it it's not present.

__Characteristics of `lower_bound`__ :
- _Time Complexity_ : $O(logN)$, where N is number of elements between `first` and `last` (binary search)
- If the value is not present, it returns an iterator to the position where the value would be inserted to maintain the sorted order
- It's index gives you the number of elements less than the specified value
- If lower bound doesn't exist, then it returns `v.end()` or `arr + n`, which gives us index as n (i.e. size)

## upper_bound()
The `upper_bound()` function returns an iterator pointing to the __first element__ in the range that is __greater than__ the specified value.

__Syntax__ :
```cpp
RandomIt upper_bound(RandomIt first, RandomIt last, const T& value);
```
- _first_ : Iterator pointing to the start of the range 
- _last_ : Iterator pointing to the end of the range (the position one past the last element)
- _value_ : The value to search for 

__Example__ :
```cpp
int main() {
	vector<int> v = {1, 3, ,3, 7, 9};
	auto it = upper_bound(v.begin(), v.end(), 3);

	// Print index and value of the lower bound 
	cout << "UB of 3 is at index: " << it - v.begin() << ", value: " << *it << endl;
	// Output: UB of 3 is at index: 1, value: 3

	return 0;
}
```
In this example, `upper_bound` returns the iterator to the 1st element greater than 3, which is 7.

__Characteristics of `upper_bound`__ :
- _Time Complexity_ : $O(logN)$, where N is number of elements between `first` and `last` (binary search)
- If the value is not present, it returns an iterator to the position where a larger value would occur in the sorted order
- It's index gives you the number of elements less than or equal to the specified value
- If upper bound doesn't exist, then it returns `v.end()` or `arr + n`, which gives us index as n (i.e. size)

## Key Differences between `lower_bound()` and `upper_bound()`
- `lower_bound` returns the iterator to the 1st element that is __greater than or equal__ to the value 
- `upper_bound` returns the iterator to the 1st element that is __strictly greater__ than the value

__NOTE__ : Both functions assume that the range `[first, last)` is sorted