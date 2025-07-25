---
title: "More about Data Types"
date: 2024-09-04 10:00:00 +0530
categories: [DSA]
tags: [cpp, data-types, basics]
math: true
---

## More about Data Types

Data types are used to determine the type and size of data associated with variables.
C++ is a statically types language, in it, we have to declare variables before using them. 
The size of data type is machine-dependent. 
```
<datatype> <name of variable>;
```
Example:
```cpp
int x;
```
x is a variable of type int and can store integers and require specific bytes of memory.
```cpp
char c;
```
c is a variable of type char and can store characters and require specific bytes of memory.

## There are two types of data types
1. __Primitive data types__: These are basic data types that are used to represent single values. Primitive data types are predefined.
   
   The following are different primitive data types :
   - <span class="cyan-blue-highlight-text">int</span> : The int data type is a 32-bit (4 bytes) integer having values from $- \, 2^{31}$ to $2^{31}-1$.
   - <span class="cyan-blue-highlight-text">char</span> : The char data type is a single 8-bit ASCII character having values from 0 to $2^{8}-1$.
   - <span class="cyan-blue-highlight-text">float</span> : The float data type is a single-precision 32-bit (4-bytes) floating point.
   - <span class="cyan-blue-highlight-text">double</span> : The double data type is a double-precision 64-bit (8-bytes) floating point.
   - <span class="cyan-blue-highlight-text">bool</span> : The bool data type can only contain two values: __true__ and __false__. It's size is 1 byte.
   - <span class="cyan-blue-highlight-text">void</span> : A variable cannot be defined for the void datatype. The void data type shows that it cannot contain anything. However, a function that is declared of the void type doesn't return anything. 
   - <span class="cyan-blue-highlight-text">wchar_t</span> : Wide character data type is also a character data type, but this data type has a size greater than the normal 8-bit data type. It's generally 2 or 4 bytes long.
    
    ![Primitive Data Types.jpeg](/assets/img/dsa/primitive-data-types.jpeg)
    
2. __Non-Primitive data types__: These are made up of Primitive data types. These are not defined by the C++ programming language but are created by the user like arrays and strings.
3. __User-Defined data types__: Struct, Union, Enum.

## Data type Modifiers
These modifiers are used to increase or decrease the effective range of certain data types.
The 4 data types modifiers are - <span class="cyan-blue-highlight-text">long</span>, <span class="cyan-blue-highlight-text">short</span>, <span class="cyan-blue-highlight-text">signed</span>, <span class="cyan-blue-highlight-text">unsigned</span>.

![Data Type Modifiers](/assets/img/dsa/data-type-modifiers.jpeg)

There are several main data types that are used: 32-bit and 64-bit integers, floating-point numbers, booleans, characters, and strings.

## 32-bit and 64-bit integers
The 32-bit integer supports values between $- \, 2,147,483,648$ and $2,147,483,647$, which is roughly equal to $\pm \, 2\times 10^{9}$. If the input, output, or any intermediate values used in calculations exceed the range of 32-bit integer, then a 64-bit integer must be used. The range of the 64-bit integer is between $- \, 9,223,372,036,854,775,808$ and $9,223,372,036,854,775,807$ which is roughly equal to $\pm \, 9\times 10^{18}$. Contest problems are usually set such that the 64-bit integer is sufficient.
```cpp
int a, b;    // These are 2 inputs that are <= 10^9
cin >> a >> b;    // Take those 2 numbers

cout << a+b << "\n";    // Print their sum, '\n' to go to next line.
cout << 1LL*a*b;
// a*b would be an int and with the range it might overflow, so multiplying it by 1LL (which is long long), will typecast it to long long.
// The order of evaluation will be (1LL*a)*b
```
__Note__ : If it's not, the problem will ask for the answer modulo m, instead of the answer itself, where m is prime. In this case, make sure to use 64-bit integers, and take the remainder of x module m after every step using `x %= m`.

## Floating-point numbers
Floating-point numbers are used to store decimal values. It is important to know that floating-point numbers are not exact because the binary architecture of computers can only store decimals to a certain precision. hence, we should always expect that floating-point numbers are slightly off. Contest problems will accommodate this by either asking for the greatest integer less than 10k times the value or will mark as correct any output that is within a certain error range of the judge's answer.

## Double
This type represents decimal numbers. The difference between these types is similar to that of int and long long. Doubles can represent more decimal numbers than floats. Long double is even more powerful (but note that this more power comes at a cost of memory. So try to use that should do the work). If memory is not going to be a crunch, use a long double for the most precise answer. Floating point numbers do not store as they look. 2 same numbers can be stored differently.
```cpp
double x;
cin >> x;
cout << fixed << setprecision(2);
/* FIXED -> means everything next happens for the floating point part only.
setprecision(2) -> Now on, every print will happen with roundoff to 2 decimal places. */

cout << x << '\n';
```

## Boolean variables
Boolean variables have 2 possible states: __true__ and __false__. We'll usually use booleans to mark whether a certain process is done, and arrays of booleans to mark which components of an algorithm have finished.
```cpp
bool temp = -1;    // 0 means false, anything else means true. It will be stored as 0/1.
cout << temp << '\n';    // will print 1, as True's output is 1, False output is 0.
```

## Character variables
Character variables represent a single Unicode character. They're returned when you access the character at a certain index within a string. Characters are represented using the ASCII standard, which assigns each character to a corresponding integer; this allows us to do arithmetic with them.
```cpp
cout << ('f' - 'a');    // will print 5
```
Characters typically require 1 byte of memory space and range from -128 to 127 or 0 t0 255
```cpp
char a, b;
cin >> a >> b;
cout << (int)a << '\n';    // Print's the ASCII value of the character.
cout << (b >= 'a' && b <= 'z') << '\n';    // Checks if the character is lowercase.
```