---
title: "Array Pointers"
date: 2024-09-11 10:00:00 +0530
categories: [DSA]
tags: [cpp, pointers, arrays]
math: true
---

## Array Pointers 
Array pointers, also known as __pointers to arrays__, are pointers that point to the memory location of an array. Understanding how arrays and pointers interact in C++ is essential for handling arrays efficiently, especially when dealing with large amounts of data. 

## Key Concepts of Array Pointers 
1. __Array to Pointer Relationship__
   In C++, the name of an array acts as a pointer to the first element of the array. 
   This means that if you have an array say `arr`, then the name `arr` is essentially a constant pointer to the 1st element (`&arr[0]`).
   ```cpp
   int arr[5] = {10, 20, 30, 40, 50};
   int* ptr = arr;    // ptr points to arr[0] 
	```
1. __Accessing Array Elements with Pointers__
   You can access elements of array using [[Pointers#Key Concepts of Pointers | Pointer Arithmetic]]. Since the array name is a pointer to the 1st element, you can increment or decrement the pointer to move through the array.
   ```cpp
   int arr[3] = {1, 2, 3};
   int* ptr = arr;

   cout << *ptr << endl;    // Output: 1 (arr[0])
   cout << *(ptr + 1) << endl;    // Output: 2 (arr[1])
   cout << *(ptr + 2) << endl;    // Output: 3 (arr[2])
	```
1. __Pointer to an Array__ 
   A pointer could also point to the entire array rather than just a single element. To declare a pointer to an array, you need to specify the size of the array. 
   ```cpp
   int arr[5] = {10, 20, 30, 40, 50};
   int (*ptr)[5] = &arr;    // ptr is a pointer to the entire array
	```
	Here, `ptr` is a pointer to an array of 5 integers. To access elements of the array using this pointer, you can dereference it.
	```cpp
	cout << (*ptr)[0] << endl;    // Output: 10
	cout << (*ptr)[1] << endl;    // Output: 20
	```

## Difference between Array Pointer & Pointer to Array
- __Array Pointer (Pointer to the 1st element of an array)__ :
  Declaring `int* ptr = arr;` means `ptr` points to the 1st element of the array. 
  [[Pointers#Key Concepts of Pointers|Pointer Arithmetic]] (`ptr + 1`, `ptr + 2`, etc.) will allow you to access subsequent elements.
- __Pointer to the entire array__ :
  Declaring `int (*ptr)[5] = &arr;` means `ptr` points to the whole array, and dereferencing `(*ptr)` gives you access to the array. Here, [[Pointers#Key Concepts of Pointers|Pointer Arithmetic]] will move the pointer across entire arrays (if there were more arrays).

## Mechanics of Array Pointers in C++
```cpp
int arr[] = {2, 3, 5, 7, 11};
cout << *arr << '\n';    // Prints 2
cout << *(arr + 1) << '\n';    // Prints 3
cout << 2[arr] << '\n';    // Prints 5
```
Behind the scenes, C++ also decodes `arr[i]` as `*(arr + i)`

__Note__ : C++ also decodes `i[arr]` as `*(i + arr)` 
Hence, `arr[i]` $\equiv$ `i[arr]` $\equiv$ `*(arr + i)` which is fairly weird