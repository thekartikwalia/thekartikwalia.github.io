---
title: "Functions"
date: 2024-09-06 10:00:00 +0530
categories: [DSA]
tags: [cpp, functions, basics]
---

## All about Functions and Examples 
A functions is a set of statements that take inputs, perform some specific computation, and produce output.

The idea is to out commonly or repeatedly done tasks together and create a function so that instead of writing the same code again and again for different inputs, we can call the function. the syntax for a function is as follows:
```cpp
<return-type> <function-name> (<set-of-arguments>) {
	// block of statments 
}
```
Functions solves 2 major problems of a program: 
1. Repetition of code
2. Non-maintainable

## More about functions:
1. A function gets called when the function name is followed by opening and closing parenthesis '()'.
2. A function is defined when the function name is followed by a pair of braces '{}' in which 1 or more statements may be present.
3. Any function can be called from any other function, including `main()`.
4. A function can be called any number of times.
5. The order in which functions are defined and the order in which they're called need not necessarily be the same.
6. A function can call itself, a process known as 'recursion'.
7. There are 2 types of functions: user-defined functions and library functions.

## Function definition:
A function definition consist of the whole description and code of a function, including it's inputs and outputs. It consists of 2 parts: a function header and a function body. The general syntax is:
```cpp
<return-type> func_name(type1 arg1, type2 arg2, ...) {
    // Local variable declarations
    // Statements 
    return expression;
}
```

## Function calling:
To execute a function, it needs to be invoked or called. Functions can be called from the `main()` function and other functions. The called function must be declared or defined before calling the function to avoid compile-time errors. Parameters can be passed within the parenthesis.

The general syntax of a function call is:
```cpp
func_name(arg1, arg2, ...);
```

## Default Arguments:
Default argument values can be provided either in the declaration or definition and represent the default value of a function argument. All default arguments must appear at the end (towards right).

Example:
```cpp
#include <bits/stdc++.h>
using namespace std;

int add(int x, int y=0) {
	return x + y;
}

int main() {
	cout << add(2) << '\n';    // Output: 2
	cout << add(3, 5) << '\n';    // Output: 8
	
	return 0;
}
```
Default arguments allow a function to be called with fewer arguments than it is defined with.
<br><br>
__Note__ : Correct sequence in defining and using a function in C++ can be as follows:
- Declare the function, call it and then define it. (like we define after int main())
- Declare the function, define it and then call it.