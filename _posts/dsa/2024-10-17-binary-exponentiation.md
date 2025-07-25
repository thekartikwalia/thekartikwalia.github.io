---
title: "Binary Exponentiation"
date: 2024-10-17 10:30:00 +05:30
categories: [DSA, Modular Arithmetic]
tags: [exponentiation, modulo, math, number-theory]
math: true
---

## Binary Exponentiation 
It's a Algorithm that calculates $a ^ {b}$ in $O(\log b)$ time complexity.

__Intution__ :

$$
a^b = 
\begin{cases} 
a^{b-1} \times a & \text{if } b \text{ is odd} \\[10pt]
a^{b/2} \times a^{b/2} & \text{if } b \text{ is even}
\end{cases}
$$

It's like mostly at every step we're doubling the power, infact in every 2 steps it will get half for sure 

In 2 steps you're getting half, so in $2 \times \log b$ steps you will get to 1
Hence, it's time complexity is $O(\log b)$

__Code__ :
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

int binpow(int a, int b) {
	// Base case
	if(b == 0) return 1;

	if(b % 2 == 1) return (a * binpow(a, b-1)) % mod;
	else {
		int x = binpow(a, b/2);
		return (x * x) % mod; 
	}
}

signed main() {
	int a, b;
	cin >> a >> b;

	int ans = binpow(a, b);
	cout << (ans%mod + mod) % mod << '\n';

	return 0;
}
```

__Note__ : 
If there's modulo, we add modulo
Else, we don't add modulo

