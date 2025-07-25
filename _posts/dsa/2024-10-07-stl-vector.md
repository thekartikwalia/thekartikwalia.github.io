---
layout: post
title: "Vector"
date: 2024-10-07
categories: [DSA, STL]
tags: [STL, C++, vector]
math: true
---

## Vector
A __vector__ is a dynamic array that can resize itself automatically when elements are added or removed. It is part of the sequence container category and is widely used due to its flexibility, efficiency, and simplicity, and it provides random access to its elements.

__Real-Life Example__
Let's consider a scenario where you want to store and manage a list of students' scores in a course. A vector would be an excellent choice for this task because:
- _Dynamic Sizing_: As students enroll or withdraw from the course, the vector can automatically adjust its size to accommodate the changing number of scores.
- _Efficient Access_: Vector provides constant time complexity for random access, making it efficient to retrieve a specific student's score.


__Example Code__
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
	// Various Initialization Methods
    vector<int> grades;
    vector<int> grades(n);    // all entries '0'
    vector<int> grades(n, x);    // all enteries 'x'

    // Adding grades to the vector
    grades.push_back(85);
    grades.push_back(90);
    grades.push_back(78);
    grades.push_back(92);

    // Accessing and printing grades
    cout << "Grades: ";
    for (int i = 0; i < grades.size(); i++) {
        cout << grades[i] << " ";
    }
    cout << endl;

    // Removing the last grade
    grades.pop_back();

    // Printing updated grades
    cout << "Updated Grades: ";
    for (int grade : grades) {
        cout << grade << " ";
    }
    cout << endl;

    return 0;
}
```

## Key Characteristics of Vector 
- __Dynamic Size__: Vectors can grow and shrink in size as elements are added or removed.
- __Random Access__: They allow constant-time access to elements using the subscript operator (`[]`).
- __Contiguous Memory__: Elements are stored in contiguous memory locations, which makes them cache-friendly and allows for efficient iteration.
- __Support for Iterators__: Vectors support iterators, enabling easy traversal and manipulation of elements.


## Important Modifiers of Containers Vector 
- `assign()`: Time Complexity - O(n), where n is the number of elements assigned.
- `push_back()`: Amortized Time Complexity - O(1) (constant time on average), though individual insertions might take O(n) in the worst case when resizing the vector.
- `pop_back()`: Time Complexity - O(1), constant time.
- `insert(position, value)`: Time Complexity - O(n), where n is the number of elements inserted. Inserting in the middle or at the beginning requires shifting elements.
- `erase(position)`: Time Complexity - O(n), where n is the number of elements erased. Erasing in the middle or at the beginning also requires shifting elements.
- `swap()`: Time Complexity - O(1), constant time. Swapping involves changing internal pointers, not actual element movement.
- `clear()`: Time Complexity - O(n), where n is the number of elements in the vector. This function removes all elements and may involve deallocating memory.
- `emplace()`: Time Complexity - O(n), where n is the number of elements after the insertion point. Elements after the insertion point may need to be shifted.
- `emplace_back()`: Amortized Time Complexity - O(1) (constant time on average), though individual insertions might take O(n) in the worst case when resizing the vector.
- `resize(new_size)`: Changes the size of the vector to `new_size`.
- `reserve(new_capacity)`: Reserves space for at least `new_capacity` elements, improving performance when you know in advance how many elements will be added.

__NOTE__ 
```cpp
vector<int> a;
cout << a.size()-1 << '\n';
// 18446744073709551615 for 64-bit
// 4294967295 for 32-bit
```
Output is not -1 because `a.size()` returns 0, but the type of 0 is unsigned integer. So when you subtract 1 from unsigned it becomes all 1's (there's no negative in case of datatypes which are unsigned), and it becomes a very large number.

_Possible Fixes_ :
- It's a good practice to keep `a.size()` type casted to integers
- It's a good practice to never subtract anything from `a.size()`

## Underlying Container of Vector
Vectors are implemented as dynamic arrays, which means they manage their own memory and can resize themselves as needed. When the size exceeds the current capacity, a new larger array is allocated, and the existing elements are copied to this new array.

## Applications of Vector
1. __Dynamic Arrays__: Vectors are widely used to implement dynamic arrays where the number of elements is not known beforehand.
2. __Data Storage__: They are useful for storing collections of data, such as lists of records or a series of measurements.
3. __Matrix Representation__: Vectors can be used to represent matrices in multi-dimensional arrays by using vectors of vectors.
4. __Sorting and Searching__: Vectors provide an easy way to perform sorting and searching operations due to their random access capabilities.
