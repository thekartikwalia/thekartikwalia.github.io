---
title: Binary Search on Answer
date: 2024-10-09 9:30:00 +0530
categories: [DSA, Binary Search]
tags: [binary search, bs on answer, optimisation, search space, check function]
math: true
mermaid: true
pin: false
---

## Framework for BS on Ans
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long;
bool check(int X, int a[]) {
	// returns true/false based on various conditional checks according to question
}
void solve() {
	int n;
	cin >> n;

	int a[n];
	for(int i=0; i<n; i++) cin >> a[i];

	int lo, hi;
	int ans;
	while(lo <= hi) {
		int mid = lo + ((hi-lo) >> 1);
		if(check(mid, a)) {
			ans = mid;
			hi = mid-1;
		} else lo = mid+1;
	}
	cout << ans << '\n';
}
signed main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int _t; cin >> _t; while(_t--)
	solve();
}
```
This form of BS is generally applicable for problem types such as :
- Minimising the maximum possible value
- Maximising the minimum possible value

TC : O(Search Space) * O(Check function)

## Example-1 : Famous Painter Partition 
__Problem Link__ : [Famous Painter Partition](https://maang.in/problems/Famous-Painter-Partition-Problem-472)

__Approach__

![[Painter Partition Approach.jpeg]]

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long

// Check whether I can complete the wall paintaing with <= k painters, in time lesser than or equal to time X
bool check(int X, int k, vector<int> arr) {
    int time_left = X;
    int painter_cnt = 1;
    for(auto time:arr) {
        if(time > X) return false;

        if(time_left >= time) time_left -= time;
        else {
            painter_cnt++;
            time_left = X-time;
        }
    }
    
    return (painter_cnt <= k);
}

void solve() {
    int n, k;
    cin >> n >> k;

    int lo=0, hi=0;
    vector<int> arr(n);
    for(int i=0; i<n; i++) {
        cin >> arr[i];

        lo = max(lo, arr[i]);
        hi += arr[i];
    }

    int ans=hi;
    while(lo <= hi) {
        int mid = lo + ((hi - lo) >> 1);
        if(check(mid, k, arr)) {
            ans = mid;
            hi = mid-1;
        } else lo = mid+1;
    }

    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--) 
    solve();
}
```
TC : $O \left( N \cdot \log \left( \sum T_i \right) \right)$
## Example-2 : Minimise Max Diff
__Problem Link__ : [Minimise Max Diff](https://maang.in/problems/Minimise-Max-Diff-46)

__Approach__

![Minimize Max Diff Approach.jpeg](/assets/img/dsa/Minimize%20Max%20Diff%20Approach.jpeg)

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;

// Can we attain Maximum Separation <= X, by placing <= K points 
bool check(int X, int a[], int k, int n) {
    int pt_cnt = 0;
    for(int i=1; i<n; i++) {
        // No of points to be placed in a neighbouring distance d,
        // such that maximum neighbouring distance is <= X,
        // is given by ceil(d/X) - 1
        int d = a[i] - a[i-1];
        int ceil_d_by_x = (d+X-1) / X;
        pt_cnt += (ceil_d_by_x - 1); 
    }
    return pt_cnt <= k;
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n];
    for(int i=0; i<n; i++) cin >> a[i];

    sort(a, a+n);    // To find 

    int lo=0, hi=0;
    for(int i=1; i<n; i++) hi = max(hi, a[i] - a[i-1]);
    int ans=-1;    // Default 
    while(lo <= hi) {
        int mid = lo + ((hi - lo)/2);
        if(mid && check(mid, a, k, n)) {
            ans = mid;
            hi = mid-1;
        } else lo = mid+1;
    }    
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    
    int _t; cin >> _t; while(_t--) 
    solve();
}
```
TC : $O(N \cdot \log (\text{ Max Neighbouring Distance }))$

__NOTE__ : 
- No of points to be placed in a neighbouring distance `d`, such that maximum neighbouring distance is `<= X`, is given by `ceil(d/X) - 1`
  For better understanding, dry run cases where `d % X == 0` and `d % X != 0`
- Ceil of `N/D` is calculated by expression `(N+D-1) / D`

## Example-3 : Kth Sum Value 
__Problem Link__ : [Kth Sum Value](https://maang.in/problems/Kth-Sum-Value-102)

__Approach__
Since $N\leq 10^{6}$  and $M\leq 10^{6}$, so we can't create array C in real life and sort it up

![[Kth Sum Value Approach.jpeg]]

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

void swap_and_resize(vector<int> &A, vector<int> &B) {
    vector<int> temp = A;
    A = B;
    B = temp;
}

// Can we form sum <= X, with pairs >= k
bool check(int X, vector<int> &A, vector<int> &B, int k) {
    int pair_cnt = 0;
    for(int b:B) {
        int val = X-b;    // b+a <= X, so a <= X-b
        // For each b, find number of elements in A which are <= (X-b)
        auto ub_ind = upper_bound(A.begin(), A.end(), val) - A.begin();
        pair_cnt += ub_ind;
    }
    return pair_cnt >= k;
}

void solve() {
    int n, m, k;
    cin >> n >> m >> k;
    
    vector<int> A(n), B(m);
    int A_min = 1e5, A_max = -1, B_min = 1e5, B_max = -1;
    for(int i=0; i<n; i++) {
        cin >> A[i];
        A_min = min(A_min, A[i]);
        A_max = max(A_max, A[i]);
    }
    for(int i=0; i<m; i++) {
        cin >> B[i];
        B_min = min(B_min, B[i]);
        B_max = max(B_max, B[i]);
    }

    // Keeping A > B
    // So that we always iterate on smaller one, and apply BS on larger one
    if(n < m) swap_and_resize(A, B);
    sort(A.begin(), A.end());    // Sort to apply lower bound

    int lo=A_min+B_min, hi=A_max+B_max;
    int ans=lo;
    while(lo <= hi) {
        // Finding first occurence of 1 (0000011111111)
        int mid = lo + ((hi-lo) >> 1);
        if(check(mid, A, B, k)) {
            ans = mid;
            hi = mid-1;
        } else lo = mid+1;
    }
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--) 
    solve();
}
```