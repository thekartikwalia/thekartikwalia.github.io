---
title: Binary Search on Real Domain
date: 2024-10-09 11:45:00 +0530
categories: [DSA, Binary Search]
tags: [binary search, real domain, floating point, precision]
math: true
mermaid: true
pin: false
---

## Framework for BS on Real Domain
__Standard Framework__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 
#define ld long double
ld EPS = 1e-9;
bool check(int X, int a[]) {
	// returns true/false based on various conditional checks according to question
}
void solve() {
	int n;
	cin >> n;

	int a[n];
	for(int i=0; i<n; i++) cin >> a[i];

	ld lo=0, hi=n;
	while(abs(hi - lo) > EPS) {
		ld mid = (lo + hi) / 2;
		if(check(mid, a)) {
			hi = mid;
		} else lo = mid;
	}
	ld ans = (lo + hi) / 2;
	cout << ans << '\n';
}
signed main() { 
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0); 
	int _t; cin >> _t; while(_t--) 
	solve(); 
}
```
EPS is a very small number, which is going to be the precision we require
The most common choice for EPS is $10^{-9}$ (or you can also keep it as $10^{-12}$)
If the question asks that you've to get precision as $10^{-9}$, then keep it as $10^{-12}$ or $10^{-15}$

You should be careful about what you set as EPS
Let's suppose in question you're given that you've to round it off to 6 decimal places in that case you need to have precision of $10^{-7}$ to include the changing 5 at 7th place as it affects value at 6th place on rounding up. So having a precision of $10^{-7}$ is generally sufficient, but still ideally keep like 100 times better precision than whatever is asked. So if it's asked precision of $10^{-6}$, then you can set EPS as $10^{-8}$

If you're using `double` instead of `long double`, `double` has the precision of $10^{-15}$, so if you're having EPS something very close to $10^{-15}$, the problem that might occur is like the next step of `hi`'s and `lo`'s can never converge. There is this small problem that might happen in real domain (if you're writing code this way) is that if you set these EPS wrongly and the datatype is not `long double`, you're keeping it `double`, so if the EPS is of range $10^{-15}$, then the numbers can kind of cross the difference before they merge. So condition might never break, and you get into an infinite loop in those cases.

---
__Alternate Framework__
Still 1 more style you can follow is that you can keep a fixed number of iterations 
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 
#define ld long double
ld EPS = 1e-9;
bool check(int X, int a[]) {
	// returns true/false based on various conditional checks according to question
}
void solve() {
	int n;
	cin >> n;

	int a[n];
	for(int i=0; i<n; i++) cin >> a[i];

	ld lo=0, hi=n;
	for(int i=0; i<40; i++) {    // Keeping fixed number of iterations
		ld mid = (lo + hi) / 2;
		if(check(mid, a)) {
			hi = mid;
		} else lo = mid;
	}
	ld ans = (lo + hi) / 2;
	cout << ans << '\n';
}
signed main() { 
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0); 
	int _t; cin >> _t; while(_t--) 
	solve(); 
}
```
After 40 iterations, the search space gets divided into $2^{40}$ parts, so it's going to be sufficient enough for most of the problems. But you can increase or decrease the number of iterations based on the precision required.

Mostly 80 iterations are going to be sufficient for most of the problems

## Example-1 : Maximise the fraction
__Problem Link__ : [Maximise the fraction](https://maang.in/problems/Maximise-the-fraction-105)

__Approach__
Whenever you've to maximise something, then there's a possibility that it could be BS on Ans problem
Since we've to find maximise the ans, so Check(X) should give monotone space like 11111000000

It turns out that we can use the generic check function, so whenever you've to find a maximum then we can always design a check function like "Can we make our Ans $\geq$ X by doing whatever is asked in Question ?"

So, Check(X) : Can we make the Ans $\geq$ X by selecting K indices ?

To design this Check(X) function, put the Ans in the expression ans $\geq$ X

$$\frac{a_1 + a_2 + \cdots a_k}{b_1 + b_2 + \cdots b_k} \geq X$$

$$\sum_{i=1}^{k} \, (a_i - X \cdot b_i) \geq 0$$

Now, Check(X) : Can we get K values such that resultant value of above expression $\geq$ 0 ?
To check this what we can do is, for all the n numbers, we can create $(a_i - X \cdot b_i)$ metric
Getting the best summation $\geq$ 0 is by taking the largest `K` numbers (because the best chance of sum of `K` numbers going to become greater than 0 is when we pick the largest `K` numbers)

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 
#define ld long double
ld EPS=1e-9;  

// Can we make fractional value >= X by selecting K indices ?
// Can we get K values such that resultant value of expression >= 0 ?
bool check(ld X, int a[], int b[], int n, int k) {
    // Find sum of top K values of expression Ai-X.Bi using Priority Queue
    priority_queue<ld, vector<ld>, greater<ld>> pq;    // minHeap
    for(int i=0; i<n; i++) {
        ld val = a[i] - (X * b[i]);
        pq.push(val);
        if(pq.size() > k) pq.pop();
    }

    ld sum_topK=0.0;
    while(pq.size()) {
        sum_topK += pq.top();
        pq.pop();
    }

    return (sum_topK >= 0.0);
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n], b[n];
    int sum_a=0;
    for(int i=0; i<n; i++) {
        cin >> a[i];
        sum_a += a[i];
    }
    for(int i=0; i<n; i++) cin >> b[i];

    // BS on real domain 
    ld lo=0.0, hi=sum_a;    // Bcoz B's at minimum can be 1
    ld ans=0.0;
    while(abs(lo-hi) > EPS) {
        ld mid = (lo + hi)/2.0;
        if(check(mid, a, b, n, k)) {
            ans = mid;
            lo = mid;
        } else hi = mid;
    }
    cout << fixed << setprecision(6) << ans << '\n';
}

signed main() {
    ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int _t; cin >> _t; while(_t--) 
    solve();
}
```
You insert `N` numbers into priority queue, but you only maintain `K` numbers at any point, so Check(X) takes $O(N \log K)$

Hence, TC : $O(N \cdot \log(\sum a_i) \cdot \log K)$