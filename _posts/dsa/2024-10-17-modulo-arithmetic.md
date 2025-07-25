---
title: "Modulo Arithmetic"
date: 2024-10-17 10:25:00 +0530
categories: [DSA, Modular Arithmetic]
tags: [modulo, math, number-theory]
math: true
---

## Modulo Arithmetic
__Modulo Arithmetic__ is a fundamental mathematical concept with diverse applications. It finds significance in computer science, cryptography, number theory, and various fields. One primary reason for its utility is its ability to handle remainders efficiently. When dealing with cyclic patterns or repetitive structures, Modulo Arithmetic simplifies calculations and offers a concise representation of relationships.

__What is the problem with Java and C++ in terms of Datatypes ?__
Java and C++ have fixed-size data types for integers. For instance, in Java, the 'int' datatype is a 32-bit signed integer, and in C++, 'int' may vary but is typically 32 bits. This limitation poses a challenge when dealing with large numbers, as overflow can occur when the result exceeds the maximum representable value. Modulo Arithmetic provides a solution by allowing computations within a specific range, preventing overflow issues.

__How problem setters tackle this ?__
Problem setters often utilize modulo arithmetic to constrain the output within a manageable range. By setting a modulo base (a modulus), they ensure that the result remains within a specified boundary, avoiding overflow problems. This approach is common in competitive programming and algorithmic contests, where precision and efficiency are crucial.

__What is Modulo Arithmetic ?__
Modulo Arithmetic, also known as clock arithmetic, is a mathematical operation that returns the remainder when one number is divided by another. In modular arithmetic, the numbers "wrap around" upon reaching a certain value, forming a cyclic pattern. The result of a modulo operation is always non-negative and less than the divisor.

__Notations of Modulo Arithmetic__
The notation used for modulo arithmetic is often expressed as `( a mod m )`, where:
- ( a ) is the dividend or the number being operated upon,
- ( m ) is the modulus or the divisor.

This operation returns the remainder when ( a ) is divided by ( m ).

## The need of Modulo Arithmetic 
Since, too large numbers like $100\,!$ can't be stored, thatswhy people move into a realm of remainder. 

Thatswhy, sometimes different coding platforms ask you to return `ans % p` instead of directly returning ans, where p is any random number. They do so to shorten the range of answer in $[0, p-1]$.

__Example__ 
A set S contains 'n' elements. If A and B are subsets of set S, then find number of different combinations of A & B generated such that $A \cap B = \emptyset$.
Since, each element in Set S has 3 options: either go to A, or to B, or no where. So, the total number of different combinations of A & B would be $3 ^ {n}$. But the problem is $3 ^ {n}$ becomes large very very fast, so instead of printing $3 ^ {n}$ you'll be asked to print $3 ^ {n} \, \% \, (10 ^ {9} + 7)$.

## Examples of problems where you'll be asked about Modulo Arithmetic
1. __Hashing and String Matching__
   Problems involving string hashing often use modulo arithmetic to prevent overflow and ensure unique hash values for different strings.
2. __Combinatorics and Counting Problems__
   Combinatorial problems, such as counting arrangements or permutations, often require modulo arithmetic to handle large numbers efficiently.
3. __Graph Theory__
   Algorithms that involve traversing graphs, finding paths, or calculating distances may benefit from modulo arithmetic to keep intermediate results manageable.
4. __Dynamic Programming__
   Some dynamic programming problems involve calculating large values that can be constrained using modulo arithmetic.

## Significance of using  $10 ^ {9} + 7$ as Modulus
1. __Need for a Prime Modulus__
   Prime moduli are chosen to ensure unique remainders, which is crucial for various algorithms and data structures. It's the 1st Prime number after $10 ^{9}$ (Convention). 
2. __Avoiding Collisions__
   Using a prime modulus helps in avoiding collisions (which can occur when two different inputs yield the same remainder) and ensures that the results of modulo operations are unique. This is crucial in scenarios like hashing, where collisions can lead to incorrect outcomes.
2. __Multiplicative Inverse__
   Having a prime modulus ensures the existence of a [[Inverses#Condition for Inverse existence | Multiplicative Inverse]]  for every non-zero element in the modulus field.
3. __Compatibility with 32-bit Integers__
   (10^9 + 7) is chosen to fit comfortably within a 32-bit signed integer, preventing overflow issues in common programming languages.
4. __Addition fits in `int` range__ 
   Because on choosing $10 ^ {9} + 7$ as modulus,  sum of 2 remainders just fits in <span class="cyan-blue-highlight-text">int</span> range ($2.1 \times 10^{9}$).
   r1 & r2 both could range from $[0, 10^{9} + 6]$
   So, their sum would range from $[0, 2 \times 10^{9} + 12]$ and the last value <span class="cyan-blue-highlight-text">int</span> can store is $2.1 \times 10^{9}$
5. __Product fits in `long long` range__ 
   Because on choosing $10 ^ {9} + 7$ as modulus,  product of 2 remainders fits in <span class="cyan-blue-highlight-text">long long</span> range ($9 \times 10^{18}$).

__NOTE__
While (10^9 + 9) can also be used as a prime modulus, (10^9 + 7) is generally favored. This preference stems from the fact that (10^9 + 7) is the first prime number greater than (10^9). There is no strict rule preventing the use of other primes, and the choice between them is a matter of general practice within the programming community. Programmers often lean towards (10^9 + 7) due to its widespread adoption and favorable properties in modulo arithmetic. Ultimately, the selection depends on personal preference or specific problem requirements.

## Understanding Modulo Arithmetic
This operation involves determining the remainder when one number is divided by another, yielding results within a specific range.
- __Cyclic Patterns__
  One of the key applications of modulo arithmetic is in managing cyclic patterns. It provides an elegant way to navigate through repetitive sequences, often encountered in various mathematical and computational contexts.
- __Range Wrapping__
  Modulo arithmetic is adept at handling scenarios where values need to wrap around a predefined range. This is particularly valuable in cases where a continuous sequence reaches a limit and starts a new, creating a cyclical behavior.

__How Modulo Works ?__
- When you perform (a mod m), you are essentially finding the remainder when (a) is divided by (m).
- The result is always non-negative and less than (m).
- If (a) is divisible evenly by (m), the result is 0.
- For example, (17 mod 5) is 2 because when 17 is divided by 5, the remainder is 2.

__NOTE__
In C++, the sign of the result for the modulo operation is determined by the sign of the dividend (the numerator). The sign of the result is the same as the sign of the dividend. Therefore, in the case of (-12 % 5), the result would be -2, not 3 as you might expect from the mathematical definition. 

## Rules of Modulo Arithmetic
To ensure that intermediate values remains small, Modulo Arithmetic follow some set of rules :
1. $(a + b)\mod c \,\equiv\, ((a \mod c) + (b \mod c))\mod c$
2. $(a \times b)\mod c \,\equiv\, ((a \mod c) \times (b \mod c))\mod c$
3. $(a - b)\mod c \,\equiv\, ((a \mod c) - (b \mod c))\mod c$
4. $(a \div b)\mod c \,\equiv\, (a \mod c) \times (b^{-1} \mod c)$
5. $a ^ {b}\mod c \,\equiv\, (a \mod c)^{b}\mod c$
6. $((a \times b) \times c) \mod p \,\equiv\, (((a \times b) \mod p) \times c) \mod p$

__Note__ : If you take modulus of 2 numbers, then both of their remainders would be around at maximum of $10^{9}$, and if you multiply both of them then the result would be around $10^{18}$ which will not fit in the integer range. So whenever something around multiplication comes, you have to use <span class="cyan-blue-highlight-text">long long</span> datatype.

## Division under Modulo 
When dividing under modulo, it's crucial to understand that directly using the division operator might not yield the correct result, especially when the modulus (m) is involved. This is because modular division doesn't always behave like regular division.

__Why Dividing Directly is Wrong ?__
In modular arithmetic, the concept of division is often replaced by finding the modular [[Inverses]]. 
The modular inverse of a number a with respect to a modulus m is another number b such that (a × b) mod m=1. Not all numbers have a modular inverse, and it's particularly essential when working with division under modulo to ensure a valid inverse exists.

__How People Handle It ?__
To handle division under modulo, people often use the concept of modular inverses. Instead of dividing by a number, b, they multiply by the modular inverse of b modulo m. This ensures that the result remains within the desired range.

__How to Manually Find Inverses ?__
To manually find the modular inverse of a modulo m, you need to find a number b such that a×b≡1 (mod m). This is often achieved using the Extended Euclidean Algorithm or other algorithms designed for this purpose. For example, finding the modular inverse of 5 modulo 11: 
$$5 \times 9 \equiv 1 \mod 11$$
So, 9 is the modular inverse of 5 modulo 11, as 5×9 ≡ 1 (mod 11)

## Example - 1 
It is currently 7:00 PM. What time (in AM or PM) will it be in 1000 hours ?

Time "repeats" every 24 hours, so we work with modulo 24
$$1000 \equiv 16 + (24 \times 41) \equiv 16 \text{ \,\,\,(mod 24)}$$
Since the time in 1000 hours is equivalent to time in 16 hours
So 1000 hours forward from 7:00 PM is like 16 hours forward from 7:00 PM
Therefore, it'll be 11:00 AM in 1000 hours.

## Example - 2
Calculate the value of expression $(a + b - c \times e ^ {d} + f) \mod (10^{9} + 7)$
It's given that all values of all variables is less than $10^{9}$

Add brackets,  $((a + (b - (c \times (e ^ {d})))) + f) \mod (10^{9} + 7)$

If the intermediate values are negative, then that's not wrong, it's just that we should've printed their positive counter part. 
For example, let's consider expression $$(3 \times -4)\mod 5$$
If it stayed as it is, $$(3 \times -4)\mod 5 \implies -12 \mod 5 = -2$$
If we've maded it correct, $$(3 \times -4)\mod 5 \implies (3 \times 1)\mod 5 = 3$$
They're still both are the same thing, you just not have corrected -2 to be 3 in realm of (mod 5)
-2 and 3 are same thing in realm of (mod 5). So, it's just about correcting the final value, if you let the intermediate value be negative and still not overflow, then that's fine. 

So, to get the positive counter part, while printing do $(ans \mod m + m)\mod m$

```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

signed main() {
	int a, b, c, d, e, f;
	cin >> a >> b >> c >> d >> e >> f;

	int ans = 1;
	for(int i=0; i<d; i++) {
		ans = (ans * e) % mod;
	}

	ans = (c * ans) % mod;
	ans = (b - ans) % mod; // ans may become negative here
	ans = (a + ans) % mod;
	ans = (ans + f) % mod;

	cout << (ans%mod + mod) % mod << '\n';

	return 0;
}
```