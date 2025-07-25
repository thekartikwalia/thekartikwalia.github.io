---
title: "Set Precision in C++"
date: 2024-09-06 10:20:00 +0530
categories: [DSA, C++ Basics]
tags: [cpp, precision, basics]
math: true
---

## Setting Precision in C++
In C++, setting precision for floating-point numbers can be done using various manipulators available in the `<iomap>` header. This includes <span class="cyan-blue-highlight-text">setprecision</span>, <span class="cyan-blue-highlight-text">fixed</span>,  and <span class="cyan-blue-highlight-text">scientific</span> for formatting numbers when outputting to streams like `std::cout`.

## Without Fixed-Point Notation 
When using <span class="cyan-blue-highlight-text">setprecision</span> without <span class="cyan-blue-highlight-text">fixed</span>, the precision refers to the total number of digits displayed, not just those after the decimal point.
```cpp
#include <iostream>
#include <iomanip>

int main() {
	double number = 123.456789;
	// Set precision to 5 digits in total 
	std::cout << std::setprecision(5) << number << std::endl;    // o/p: 123.46  
	// Output might be in scientific notation for large numbers
	
	return 0;
}
```

## With Fixed-Point Notation 
Combining <span class="cyan-blue-highlight-text">setprecision</span> and <span class="cyan-blue-highlight-text">fixed</span> changes the behavior, so the precision strictly refers to the number of digits after the decimal point, and numbers are displayed in fixed-point notation.
```cpp
#include <iostream>
#include <iomanip>

int main() {
	double number = 123.456789;
	// Set precision to 2 digits after the decimal point, with fixed-point notation
	std::cout << std::fixed << std::setprecision(2) << number << std::endl;    
	// o/p: 123.46
	
	return 0;
}
```

These examples illustrate how to control the precision of floating-point numbers in C++, with and without fixed-point notation. `std::fixed` enforces the fixed-point notation, showing numbers in a standard decimal format. Without  `std::fixed`, `std::setprecision` controls the total number of significant digits, which may trigger scientific notation for very large or very small numbers.