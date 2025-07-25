---
title: Two Pointers (Same Direction)
date: 2024-10-23 23:10:00 +0530
categories: [DSA, Two Pointers]
tags: [two pointers, sliding window, subarrays, prefix sum, distinct elements]
math: true
mermaid: true
pin: false
---

## Two Pointers (Same Direction)
Both pointers start from the beginning and move forward at different speeds.
You try to maintain some sort of window over here.

_Example_ : Sliding window problems or finding the longest subarray that satisfies certain conditions.

__NOTE__ : Sliding Window means Fixed sized window, where as Two Pointers (same direction) is a more generic Variable sized window 

## Condition for deciding whether it's a Two Pointer problem 
If \[L, R] satisfies the criteria, then \[L+1, R] should also satisfy the criteria, i.e.
Criteria on \[L, R] $\implies$ Criteria on \[L+1, R]
If above condition is True, then it's definitely a Two Pointer problem

In General, it's used to solve problems in which we need to find Longest or Shortest or Count number of Subarrays.

## Framework for Two Pointers 
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

void solve() {
	int n;
	cin >> n;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	// head and tail
	int tail=0, head=-1;

	// data structure for the window 

	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while(/* there is a next element to eat and we can eat it */) {
			head++;
			// include element at head in the data structure
		}

		// update the answer for current start

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// change data structure because of removing tail element
			tail++;
		}
	}
}
signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```

__NOTE__ 
Whenever we see a __while loop inside another while loop__, the key thing to notice is whether the __head__ pointer is being reset repeatedly or if it is globally shared.

If the head is shared, it can only move forward a total of __N__ times (where N is the size of the input). In such cases, we calculate the __total cost__ instead of just the cost for one step. This is because if the head moves forward by a large amount in one step, it will move less in other iterations.

This concept is known as __Amortization__.

__Time Complexity (Amortized)__

$$O(N * (H + A + T))$$

where,
H $\rightarrow$ One head step
A $\rightarrow$ Answer update
T $\rightarrow$ One tail step

__NOTE__ 
Remember that the condition `head = tail - 1` is used as the __RESET__ condition, indicating an empty subarray or window. This approach is useful for handling problems where a 0-sized or empty subarray can be considered a valid solution. In such cases, it's not necessary to always take a subarray of at least size 1.

For better understanding of __RESET__ condition, dry run __Problem - 2__ with  `a = [0, 0, 0, 1, 1]` & `k = 0`

## Problem - 1 : Finding Longest Subarray  based on a Criteria
Find the Longest subarray containing only 1's if at most k positional flips are allowed
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

void solve() {
	int n, k;
	cin >> n >> k;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	// head and tail
	int tail=0, head=-1;

	// data structure for the window 
	int cnt_zero=0;

	int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (arr[head+1] == 1 || cnt_zero < k)) {
			head++;
			// include element at head in the data structure
			if(arr[head] == 0) cnt_zero++;
		}

		// update the answer for current start
		ans = max(ans, head-tail+1);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// change data structure because of removing tail element
			if(arr[tail] == 0) cnt_zero--;

			tail++;
		}
	}
}
signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```
TC : $O(N)$

## Problem - 2 : Counting all Subarrays  based on a Criteria
Find the number of subarrays having number of distinct elements less than or equal to k

Firstly check the condition, Criteria(L, R) $\implies$ Criteria(L+1, R)
If there are $\leq$ k distinct elements in range \[L, R], then we can definitely say that number of distinct elements in range \[L+1, R] is also $\leq$ k. Since the condition is satisfied, hence it's a Two Pointer problem.
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

void solve() {
	int n;
	cin >> n;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	// head and tail
	int tail=0, head=-1;

	// data structure for the window 
	map<int, int> freq;
	int cnt_distinct=0;

	int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (cnt_distinct < k || freq[a[head+1]] != 0)) {
			head++;
			// insert ds(head)
			if(freq[a[head]] == 0) {
				cnt_distinct++;
			}
			freq[a[head]]++;
		}

		// update the answer for current start
		ans += (head-tail+1);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// erase from ds(tail)
			freq[a[tail]]--;
			if(freq[a[tail]] == 0) {
				cnt_distinct--;
			}
			tail++;
		}
	}
	cout << ans << '\n';
}
signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```
TC : $O(N \log N)$

__NOTE__ 
The portion `freq[a[head+1]] != 0` inside 2nd while loop increases the size of map if this element wasn't present in map previously. So if you had used the logic of size instead of maintaining `cnt_distinct` variable, then you shouldn't access `freq[a[head+1]]` inside while loop, instead use `find()` function.

__TC Reduction Idea for Special Cases__
If it'll be given in the question that A\[i] $\leq 10 ^ {6}$, then instead of maintaining map we can maintain an large sized frequency array (that too globally). If the value which we are accessing in map is less than $10^{6}$, then we can access it in an array as well. This is a very common trick used to reduce time complexity, as accessing in array takes $O(1)$ where as accessing in map takes $O(\log N)$

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// data structure for the window 
int freq[1000100];
int cnt_distinct=0;
	
void solve() {
	int n, k;
	cin >> n >> k;

	int a[n];
	for(int i=0; i<n; i++) cin >> a[i];

	// head and tail
	int tail=0, head=-1;

	int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (cnt_distinct < k || freq[a[head+1]] != 0)) {
			head++;
			// insert ds(head)
			if(freq[a[head]] == 0) {
				cnt_distinct++;
			}
			freq[a[head]]++;
		}

		// update the answer for current start
		ans += (head-tail+1);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// erase from ds(tail)
			freq[a[tail]]--;
			if(freq[a[tail]] == 0) {
				cnt_distinct--;
			}
			tail++;
		}
	}
	cout << ans << '\n';
}

signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```
TC : $O(N)$

Note that you don't need to write erase now for array, due to the existence of a separate variable `cnt_distinct`. This is the benefit of using separate variable `cnt_distinct`, as the code will get easily converted from frequency map to frequency array.

Note that it turns out that with this code you don't need to clear globally declared frequency array and variable `cnt_distinct`, due to `while(tail < n)` condition. This two pointer framework magically clears the data structure which it is using for itself.

__Variation - 1__ 
Find the number of subarrays having number of distinct elements greater than or equal to k
It can be obtained simply by,
(# of subarrays with distinct elements $\leq$ N) - (# of subarrays with distinct elements $\leq$ k-1) 
i.e. (Total # of subarrays) - (# of subarrays with distinct elements $\leq$ k-1)
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 

// Data structure for window 
int freq[1000100];
int cnt_distinct=0;

int get_subarray_distinct_lessthan(int n, int k, int a[]) {
    // head and tail
	int tail=0, head=-1;

    int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (cnt_distinct < k || freq[a[head+1]] != 0)) {
			head++;
			// insert ds(head)
			if(freq[a[head]] == 0) {
				cnt_distinct++;
			}
			freq[a[head]]++;
		}

		// update the answer for current start
		ans += (head-tail+1);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// erase from ds(tail)
			freq[a[tail]]--;
			if(freq[a[tail]] == 0) {
				cnt_distinct--;
			}
			tail++;
		}
	}
	return ans;
}

void solve() {
    int n, k;
    cin >> n >> k;
    
    int a[n];
    for(int i=0; i<n; i++) cin >> a[i];

	int total_subarrays = (n * (n+1)) / 2;    // nC2
	int less_than_k_minus_1 = get_subarray_distinct_lessthan(n, k-1, a);
    cout << (total_subarrays - less_than_k_minus_1) << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int _t; while(_t--)
    solve();
}
```

__Variation - 2__
Find the number of subarrays having number of distinct elements equal to k
It can be obtained simply by,
(# of subarrays with distinct elements $\leq$ k) - (# of subarrays with distinct elements $\leq$ k-1) 
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 

// Data structure for window 
int freq[1000100];
int cnt_distinct=0;

int get_subarray_distinct_lessthan(int n, int k, int a[]) {
    // head and tail
	int tail=0, head=-1;

    int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (cnt_distinct < k || freq[a[head+1]] != 0)) {
			head++;
			// insert ds(head)
			if(freq[a[head]] == 0) {
				cnt_distinct++;
			}
			freq[a[head]]++;
		}

		// update the answer for current start
		ans += (head-tail+1);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// erase from ds(tail)
			freq[a[tail]]--;
			if(freq[a[tail]] == 0) {
				cnt_distinct--;
			}
			tail++;
		}
	}
	return ans;
}

void solve() {
    int n, k;
    cin >> n >> k;
    
    int a[n];
    for(int i=0; i<n; i++) cin >> a[i];

	int less_than_k = get_subarray_distinct_lessthan(n, k, a);
	int less_than_k_minus_1 = get_subarray_distinct_lessthan(n, k-1, a);
    cout << (less_than_k - less_than_k_minus_1) << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int _t; while(_t--)
    solve();
}
```

__Variation - 3__
Find the sum of lengths of subarrays having number of distinct elements less than or equal to k

Sum of lengths for all subarrays starting at `tail` and ending before or at `head` is given by,

$$1 + 2 + 3 + \dots + len = \frac{(len) \cdot (len + 1)}{2}$$

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// data structure for the window 
int freq[1000100];
int cnt_distinct=0;
	
void solve() {
	int n;
	cin >> n;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	// head and tail
	int tail=0, head=-1;

	int ans=0;
	// for every start
	while(tail < n) {
		// eat as many elements as possible till it's valid
		while((head+1 < n) && (cnt_distinct < k || freq[a[head+1]] != 0)) {
			head++;
			// insert ds(head)
			if(freq[a[head]] == 0) {
				cnt_distinct++;
			}
			freq[a[head]]++;
		}

		// update the answer for current start
		int len = (head-tail+1);
		ans += ((len * (len + 1)) / 2);

		// move start one step forward
		if(tail > head) {
			// when we have 0 elements in the window
			tail++;
			head = tail-1;
		} else {
			// erase from ds(tail)
			freq[a[tail]]--;
			if(freq[a[tail]] == 0) {
				cnt_distinct--;
			}
			tail++;
		}
	}
	cout << ans << '\n';
}

signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```