---
title: "2D Arrays: Form, Traversing, Declaring and Passing"
date: 2024-09-10 10:00:00 +0530
categories: [DSA, Arrays]
tags: [cpp, arrays, 2d-array, pointers]
math: true
---

## General form of declaring N-dimensional arrays 
Arrays allow you to store multiple values in a single variable. In programming, an array is like a container that holds a bunch of related items.

The syntax for a 1-D array is pretty simple:
```cpp
int arr[n];
```
Here, `n` is size of the array, <span class="cyan-blue-highlight-text">int</span> is the data type of the array, and `arr` is the name of the array. This means that the array can hold `n` values of the <span class="cyan-blue-highlight-text">int</span> data type.

But what about 2-D arrays? The syntax is a little different:
```cpp
int arr[n][m];
```

Here, `n` and `m` are the sizes of the array. In a 2-D array, the first index represents the row number and the second index represents the column number. This is called __row-major order__.

And what about arrays with more dimensions? The syntax looks like this:
```cpp
int arr[n1][n2][n3]...[nm];
```
This means that the array has `n1` items in the first dimension, `n2` items in the second dimensions, and so on, up to `nm` items in the mth dimension. The more dimensions an array has, the more data it can store.

So whether you're working with a 1-D array, a 2-D array, or an array with even more dimensions, udnerstanding the syntax is important for storing and manipulating your data. With arrays, you can store and organize large ammounts of data in a way that makes sense for your program.

## Accessing and Traversing 2-D Array Elements 
Sample program for demonstration how to traverse and access each element of a 2-D array.
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n, m;
	cin >> n >> m;    // n as # of rows and m as # of cols
	int arr[n][m];

	// Taking the input in 2-D array
	for(int i=0; i<n; i++) {
		for(int j=0; j<m; j++) {
			cin >> arr[i][j];
		}
	}

	// Printing the content of 2-D array with their index 
	for(int i=0; i<n; i++) {
		for(int j=0; j<m; j++) {
			cout << arr[i][j];
			cout << "(" << i << "," << j << ")" << " ";
		}
		cout << '\n';
	}

	return 0;
}
```
In this program, we first take input from the user for the number of row and columns of the 2-D array. Then, we use nested for loops to take input for each element of the 2-D array.

After taking input, we print the contents of the 2-D array along with their respective indices using another set of nested for loops. This helps us visualize the positions of each element in the array.

## Different ways to create a 2-D array
__Method 1__:
You can create a 2-D array with a fixed size using the following syntax:
```cpp
int arr[n][m];
```
---
__Method 2__:
This method involves initializing the array with data. You can create a 2-D array and initialize it's values using the following example:
{% raw %}
```cpp
int arr[][4] = {{312, 247, 311, 193},
                {311, 242, 738, 917},
                {941, 252, 549, 595}};
```
{% endraw %}

---
__Method 3__:
This method involves dynamic allocation of memory for the 2-D array. You can create a 2-D array with dynamic memory allocation using the following syntax:
```cpp
int **arr;
arr = new int *[n];

for(int i=0; i<n; i++) {
	arr[i] = new int [m];
}
```
To create a 2-D array, you need to think of it as an array where the elements are of type array. So you make the array as `int** arr = new int* [5]`, this will create a dynamic array of length 5 where element type is an array of int. Next, you loop for 5 times and give each element of the `arr` array to hold a dynamic array of type `int` and length 5.

---
__Method 4__:
This is similar to 3rd method, but instead of using a pointer to a pointer, we use an array of pointers. You can create a 2-D array with dynamic memory allocation using the syntax:
```cpp
int *arr[n];

for(int i=0; i<n; i++) {
	arr[i] = new int [m];
}
```
You create an array of length 5 and element type of int as `int a[5]`. In Method 4, `int* a[5]` basically creates an array of length 5 where the elements are of type `int*` meaning elements are dynamic array with type int. Loop for 5 times and give each element of the `a` array to hold a dynamic array of type int and length 5. The difference between Method 3 and 4 will be that the outer array in Method 3 is also __dynamic__ while in Method 4 it is not.

__Note__ : In function declarations, you can omit the bounds specification for the first dimension of a multidimensional array.

## Passing a 2-D array to a function in C++
In C++, passing a 2-D array to a function can be done in multiple ways. 
Here are a few examples:
```cpp
const int n = 5;
const int m = 4;

void func_name(int a[n][m]) {
	// your code 
}

void func_name(int a[][5]) {
	// you code
}

void func_name(int *a[5]) {
	// your code 
}

void func_name(int **a) {
	// you code
}
```
__Note__ : `int arr[5][]` isn't allowed because compiler cannot calculate the correct memory location of `arr[i][j]` without knowing the number of columns `m`. The first dimension `n` can be omitted because, in C++, arrays decay into pointers, so the size of first dimension is not needed at compile time.

## Why `int arr[][m]` works but `int arr[n][]` doesn't ?
When an array is passed to a function, we are actually sending the pointer to 1st element of the array i.e. similar to sending `&arr[0][0]`. Compiler doesn't have any information regarding dimensions of the array, or total number of elements in the array. Also even though the array is 2-D, it is actually stored in memory as contiguous blocks like `arr[0][0], arr[0][1], ..., arr[0][n-1], arr[1][0], arr[1][1], ..., arr[m-1][n-1]`. 

To find the data at memory location `arr[i][j]` the number of rows(`m`) doesn't need to be passed explicitly because it doesn't affect how the array is indexed. The pointer only needs to know how many columns(`n`) are in each row to compute the offset.

For example, in `arr[10][10]` we want to access `arr[2][1]` i.e. 2nd column of 3rd row. As you know that each row consists of 10 columns, then your's is stored at $2 \times 10 \text{ block} + 2 \text{ block}$ i.e. 22nd block.

__Note__ : You can't have gone to 22nd block if you didn't knew the number of columns (i.e. 10)

