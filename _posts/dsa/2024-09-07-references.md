---
title: "References"
date: 2024-09-07 10:50:00 +0530
categories: [DSA, C++ Basics]
tags: [cpp, references, basics]
math: true
---

## References 
In C++, __References__ provide an alternative name or alias for existing variable. 
A reference is not a separate object, but another name for the same memory location.

References are often used in function parameters to allow functions to modify the arguments passed to them.

Also known as __Aliases__.

## Key Points about References
1. __Declaration__ : A reference is declared using the `&` symbol.
   ```cpp
	int a = 10;
	int &ref = a;   // 'ref' is a reference to 'a'
	```
1. __No Re-Assignment__ : Once a reference is assigned to a variable, it cannot be changed to refer to another variable.
   ```cpp
   int b = 20;
   ref = b;    // This does'nt change reference; instead, it assigns value of 'b' to 'a'
	```
1. __Must be Initialised__ : References must be initialised at the time of declaration. You can't create an uninitialised reference.
   ```cpp
   (int &) ref;    // Invalid, must initialize a reference
	```
1. __Usage in Functions__ : One of the main uses of references is in function parameters, allowing functions to modify the arguments passed to them without copying them.
   ```cpp
   void modify(int &x) {
	   x = 100;
   }

	int num = 10;
	modify(num);    // 'num' becomes 100 because 'x' is a reference to 'num'
	```
1. __Const References__ : A reference can be declared as `const`, meaning that it cannot be used to modify the referenced variable.
   ```cpp
   void print(const int &x) {
	   cout << x;
   }
	```

__NOTE__ :
`&` on LHS of `=` is actually for __References__
`&` on RHS of `=` is actually __[[Pointers#Key Concepts of Pointers | Address-of]]__ operator in __Pointers__

## Difference from Pointers 
- __References__ must always be initialised, while __pointers__ can be `nullptr`.
- __References__ cannot be reassigned to refer to another object, while __pointers__ can be changed to point to different objects.
- Accessing a __reference__ is syntactically similar to accessing the variable itself, while __pointers__ require dereferencing (`*`).