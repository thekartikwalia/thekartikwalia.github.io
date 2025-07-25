---
title: Factorial
date: 2024-09-19 8:00:00 +0530
categories: [DSA, Combinatorics]
tags: [factorial, permutations, combinatorics, modulo arithmetic]
math: true
pin: false
---

## Factorial of a Number  $(n!)$
It tells how many ways are there to arrange 'n' stuffs in an ordered manner
It is given by, $$n! = n \times (n-1) \times (n-2) \times \cdots \times 1$$

## Program for calculating Factorial 
Calculate the factorial of a number. Print answer after taking it's modulus with $10^{9} + 7$

```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 
int mod = 1e9 + 7;

int fact(int x) {
	int ans = 1;
	for(int i=2; i<=x; i++) {
		ans = (ans * i) % mod;
	}
	return ans;
}

signed main() {
	int x;
	cin >> x;
	cout << fact(x) << '\n';

	return 0;
}
```
__Note__ : No need to apply mod to `ans` at the end, because at each iteration it is getting modded