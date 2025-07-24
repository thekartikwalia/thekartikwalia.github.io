---
title: "Arithmetic Operators"
date: 2024-09-04 10:05:00 +0530
categories: [DSA]
tags: [cpp, operators, basics]
---

## Arithmetic Operators 
Operators are symbols that are used for mathematical and logical computation on operands.
```cpp
int sum = a + b;
// Here a, b, sum are operands 
// =, + are operators
```
Operators are of 3 types:
1. __Unary__ : Requires a single operand. Eg: `++x`, `x++`, etc.
2. __Binary__ : Require 2 operands. Eg: `a + b`, `a * b`, etc.
3. __Ternary__ : Require 3 operands. Eg: `a ? b : c`

__Arithmetic operators__ are operators which are used to perform arithmetic or mathematical operations. Example: +, -, *, /, %, etc.

![Arithmetic Operators.jpeg](/assets/img/dsa/arithmetic-operators.jpeg)

## Example:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
	int a = 12, b = 7;
	cout << "**-- Arithmetic operators --**" << '\n';
	cout << "The value of a + b is " << a + b << '\n';
	cout << "The value of a - b is " << a - b << '\n';
	cout << "The value of a * b is " << a * b << '\n';
	cout << "The value of a / b is " << a / b << '\n';
	cout << "The value of a % b is " << a % b << '\n';
}
```
You'll get an output something like this:
```
**-- Arithmetic operators --**
The value of a + b is 19
The value of a - b is 5
The value of a * b is 84
The value of a / b is 1
The value of a % b is 5
```
As you probably noticed, the division operator of C++ performs so-called integer division. This means the answer is rounded to an integer (towards 0).

Hence, `7 / 3 = 2`, with remainder 1, and `-7 / 3 = -2`.

__Note__ : If you run arithmetic operations program with b = 0, then it will result in a runtime error.