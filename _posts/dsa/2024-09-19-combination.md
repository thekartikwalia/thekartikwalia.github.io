---
title: Combination
date: 2024-09-19 23:00:00 +0530
categories: [DSA, Combinatorics]
tags: [nCr, combinations, binomial coefficients, factorial, modular inverse, pascal triangle]
math: true
pin: false
---

## n Choose r $({}^{n}\text{C}_{r})$
It represents number of ways of combinatorially choosing 'r' items out of a total of 'n' items

It is given by, 

$${}^{n}\text{C}_r = \frac{n!}{r! \times (n-r)!}$$

## Exploring the Logic behind  ${}^{n}\text{C}_{r}$ 
There are 'n' positions & 'n' items 
No. of ways to arrange these 'n' items in 'n' positions is $n!$ ways
The thing is we want to choose 'r' items, so the process we set is that we'll always choose the first 'r' items in that arrangement
So we're saying that we'll put 'n' items, and after that will choose out first 'r' items from the arrangement
All arrangement of first 'r' elements are gonna give the same choices of elements picked (because we're choosing a set not a permutation), so we divide the result by $r!$
Similarly, all arrangements of items from (r+1) to n are gonna give the same choices of elements picked, so we also divide the result by $(n - r)!$
Hence, above formula is combinatorially correct

__Note__ : When intra-arrangement between a set of 'x' items doesn't matters, then in such case we divide the ans by $x!$

## Reason behind ${}^{n}\text{C}_{r}$ being an integer
Number of ways of selecting something can never be a fraction, it has to be a integer only.
So, we can say that 

$$\frac{n!}{r! \times (n-r)!} \in I$$

Upon opening factorial, we get  

$$\frac{n \times (n-1) \times \cdots \times (n-r+1) \times (n-r) \times \cdots \times 1}{r! \times (n-r)!} \in I$$

$$\frac{n \times (n-1) \times \cdots \times (n-r+1)}{r!} \in I$$

## Divisibility of Product of Consecutive Integers
From previous reasoning behind ${}^{n}\text{C}_{r}$ being an integer, you can say that 
> " Product of any 'r' consecutive numbers is always divisible by $r!$ "

Source : [Link](https://proofwiki.org/wiki/Divisibility_of_Product_of_Consecutive_Integers) 

## Programs for calculating ${}^{n}\text{C}_{r}$
__Approach - 1__ :
Instead of dividing by denominator, use concept of [[Inverses]], along with [[Factorial]] & [[Binary Exponentiation]]
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

int inverse(int x) {
	return binpow(x, mod-2);
}

int fact(int x) { 
	int ans = 1; 
	for(int i=2; i<=x; i++) { 
		ans = (ans * i) % mod;
	} 
	return ans; 
}

int ncr(int n, int r) {    // O(n + r)
	int num = fact(n);
	int den = (fact(r) * fact(n-r)) % mod;
	return (num * inverse(den)) % mod;
}
```
TC : $O(n+r)$

---
__Approach - 2__ : What if $n \leq 10^{9}$ and $r \leq 20$
Previous code won't work as fact(n) would get very large (will loop till $10^{9}$)

Just use basic observations along with the concept of [[Inverses]] & [[Binary Exponentiation]]
```cpp 
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

int binpow(int a, int b) {
	if(b == 0) return 1;
	
	if(b % 2 == 1) return (a * binpow(a, b-1)) % mod;
	else {
		int x = binpow(a, b/2);
		return (x * x) % mod;
	}
}

int inverse(int x) {
	return binpow(x, mod-2);
}

int single_ncr(int n, int r) {    // O(r)
	int num = 1, den = 1;
	for(int i=1; i<=r; i++) {
		num = (num * (n-i+1)) % mod;
		den = (den * i) % mod;
	}
	return (num * inverse(den)) % mod;
}
```
TC : $O(r)$
Infact you could also loop 'i' till `min(r, n-r)`, that will still work. You wanna cancel out larger one and loop for smaller one, among $r!$ & $(n-r)!$. In such case, TC would be $O(min(r, \,n-r))$
Technically, this code is always better to use than code in __Approach - 1__

---
__Approach - 3__ : What if you have to calculate exact value of ${}^{n}\text{C}_{r}$ with $n \leq 40$ and $r \leq n$
We know that, till 40 we can save all factorials as long long, more than that it will overflow

Use basic observations, instead of taking inverse & multiplying, we just divide it then and there only
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

int basic_ncr(int n, int r) {
	int ans = 1;
	for(int i=1; i<=r; i++) {
		ans = ans * (n-i+1);
		ans = ans / i;
	}
	return ans;
}
```
This code only works for $n \leq 40$ 
Due to __[[Combination#Divisibility of Product of Consecutive Integers| Divisibility of Product of Consecutive Integers]]__, `ans = ans / i` would never give floor of division 

---
__Approach - 4__ : Calculate ${}^{n}\text{C}_{r}$ modulo $10^{9}$, with $n \leq 1000$ and $r \leq n$
Since mod is not a prime number, [Inverses]({% post_url 2024-10-17-inverses %}) wouldn't always exist 
So we can't perform division (but we can perform addition irrespective of whether modulo is prime or not)
So we can't go for the code in __Approach - 2__ 

Use the formula, 

$${}^{n-1}\text{C}_{r} + {}^{n-1}\text{C}_{r-1} = {}^{n}\text{C}_{r}$$

Out of 'n' items, 
If you took 1st item, then choose (r-1) items from remaining (n-1) items
If you don't took 1st item, then choose (r) items from remaining (n-1) items

This formula leads to the formation of __Pascal's triangle__, use the triangle to find $${}^{n}\text{C}_{r}$ modulo $10^{9}$$
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9;

int ncr[1001][1001];    // Stores Pascal's triangle
int ncr_random_modulo(int n, int r) {
	ncr[0][0] = 1;    // There's only 1 way of choosing 0 items from 0 items

	// Calculate iCj, and form Pascal's triangle
	for(int i=1; i<n; i++) {
		for(int j=0; j<=i; j++) {
			if(j == 0) ncr[i][j] = ncr[i-1][j] % mod;
			else ncr[i][j] = (ncr[i-1][j-1] + ncr[i-1][j]) % mod;
		}
	}
	return ncr[n][r];
}
```

---
__Approach - 5__ : There are given 'q' queries & you've to calculate ${}^{n}\text{C}_{r}$ modulo $10^{9}$ with $n, q, r \leq 10^{6}$
'q' queries means you've to calculate 'q' different  ${}^{n}\text{C}_{r}$ values

We will precompute [[Factorial | Factorials]] till a certain limit and then proceed similar to how we did in __Approach - 1__
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

int binpow(int a, int b) {
	if(b == 0) return 1;
	if(b % 2 == 1) return (a * binpow(a, b-1)) % mod;
	else {
		int x = binpow(a, b/2);
		return (x * x) % mod;
	}
}

int inverse(int x) {    // O(log(mod))
	return binpow(x, mod-2);
}

int fact[1000100];
int precompute() {
	fact[0] = 1;
	for(int i=0; i<=1000000; i++) {
		fact[i] = (fact[i-1] * i) % mod;
	}
}

int ncr_fact(int n, int r) {    // O(log(mod))
	int num = fact[n];
	int den = (fact[n-r] * fact[r]) % mod;
	return (num * inverse(den)) % mod;
}

signed main() {
	precompute();
	int q;
	cin >> q;

	while(q--) {
		int n, r;
		cin >> n >> r;
		cout << ncr_fact(n, r) << '\n';
	}
	
	return 0;
}
```
This is the __most common method__ used for finding ${}^{n}\text{C}_r$
TC (per query) : $O(\log (\text{mod}))$

---
__Approach - 6__ : Can we do a bit faster than $O(\log (\text{mod}))$ ?
Inverse calculation is a little costly, so we will precompute [[Inverses]] of [[Factorial | Factorials]] as well
For precomputing Inverses of factorial, $$\frac{1}{(i-1)!} = i \times \frac{1}{i!} \implies {((i-1)!)}^{-1} = i \times {(i!)}^{-1}$$
So what we will do is instead of calculating ${}^{n}\text{C}_r$ as, $${}^{n}\text{C}_r = \frac{n!}{r! \times (n-r)!}$$
We will calculate ${}^{n}\text{C}_r$ as, $${}^{n}\text{C}_r = n! \times (r!)^{-1} \times ((n-r)!)^{-1}$$
And each of these factorial inverses would have been precomputed 
Now, every query suddenly is of $O(1)$
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long
int mod = 1e9 + 7;

int binpow(int a, int b) {
	if(b == 0) return 1;
	if(b % 2 == 1) return (a * binpow(a, b-1)) % mod;
	else {
		int x = binpow(a, b/2);
		return (x * x) % mod;
	}
}

int inverse(int x) {    // O(log(mod))
	return binpow(x, mod-2);
}

int fact[1000100];
int invfact[1000100];
int precompute_for_faster() {    // O(n) + O(log(mod)) + O(n) ~ O(n + log(mod))
	fact[0] = 1;
	for(int i=0; i<=1000000; i++) {
		fact[i] = (fact[i-1] * i) % mod;
	}
	invfact[1000000] = inverse(fact[1000000]);
	for(int i=1000000; i>=1; i--) {
		invfact[i-1] = (invfact[i] * i) % mod;
	}
}

int ncr_fact_faster(int n, int r) {    // O(1)
	int num = fact[n];
	int den = (invfact[n-r] * invfact[r]) % mod;
	return (num * den) % mod;    // den is already inverted
}

signed main() {
	precompute_for_faster();
	int q;
	cin >> q;

	while(q--) {
		int n, r;
		cin >> n >> r;
		cout << ncr_fact_faster(n, r) << '\n';
	}
	
	return 0;
}
```
This code will only works till $n, q, r \leq 10^{6}$, you cannot precompute factorial if it's $10^{9}$
TC : $O(1)$
TC of Precomputation : $O(n + \log(\text{mod}))$

## Most Extreme Problem about calculating ${}^{n}\text{C}_{r}$ 
__Problem Link__ : [Long Sandwich](https://www.codechef.com/problems/SANDWICH)
