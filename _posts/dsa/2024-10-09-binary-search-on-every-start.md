---
title: Binary Search on Every Start
date: 2024-10-09 10:30:00 +0530
categories: [DSA, Binary Search]
tags: [binary search, bs on every start, sliding window, prefix sum, upper bound]
math: true
mermaid: true
pin: false
---

## Framework for BS on Every Start 
This framework is essentially the same as the BS on Ans framework, but applied at every starting position.

This form of BS is generally applicable for problem types such as :
- Finding the minimum or maximum length subarray that meets certain criteria
- Determining the number of subarrays possible based on specific criteria


## Example-1 : Consecutive One
__Problem Link__ : [Consecutive One](https://maang.in/problems/Consecutive-one-44)

__Approach - 1 (Prefix & Partial Sums)__
Whenever you've to keep track of a window that how many elements are there and all, then you should think in direction of Prefix sums.

1. Invert the inputs, so that we can calculates number of `0`'s directly by building Prefix sum array
2. Apply BS on Ans to get maximum length subarray possible with at most `k` flips
3. Check(X) : Can we make `<= X` length subarray of all `1`'s, with `<= k` flips
   (Just check can we make any 1 of subarray among all of length `X` converted to all `1`'s in `<= k` flips)
   Because if we can make `X` length subarray with `k` flips, then we can also make `<= X` length subarray with `<= k` flips
   Use Partial sum to calculate number of `0`'s in any window `L` to `R`
4. If number of `0`'s are `<= k`, then we can flip the whole array to `1`'s

__Code - 1__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// Can we make X length subarray of all 1's, with <= k flips (any 1 among all)
bool check(int X, int a[], int k, int n) {
    int cnt_0=0;
    for(int L=0; L+X-1<n; L++) {    // O(N-X+1) -> total number of windows of length X 
        int R = L+X-1;
        cnt_0 = (L) ? a[R] - a[L-1] : a[R];
        
        // Any 1 among all subarrays of length X
        if(cnt_0 <= k) return true;    
    }
    return false;
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n];
    for(int i=0; i<n; i++) {
        int x;
        cin >> x;
        a[i] = !x;    // (or a[i] = 1-a[i]) We can directly count 0's using prefix sum 
    }

    // Build prefix sum (p[i] gives number of 0s from start to ith index)
    for(int i=1; i<n; i++) a[i] += a[i-1];

    // Apply BS on Ans to get maximum length subarray possible with at most k flips
    int ans=0;
    int lo=0, hi=n;
    while(lo <= hi) {    // O(NlogN)
        int mid = lo + ((hi-lo) >> 1);
        if(check(mid, a, k, n)) {
            ans = mid;
            lo = mid+1;
        } else hi = mid-1;
    }
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--) 
    solve();
}
```
TC : $O(N \log N)$

---
__Approach - 2 (Sliding Window)__
Similar to Approach-1, just instead of building prefix sum and using partial sum to calculate number of `0`'s in a range `L` to `R`, maintain a fixed size sliding window (of length `X`) to keep track of number of `0`'s in that particular window 

__Code - 2__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// Can we make X length subarray of all 1's, with <= k flips (any 1 among all)
bool check(int X, int a[], int k, int n) {
    int cnt_0=0;

    // Sliding window to count 0s in 1st window of size X
    for(int i=0; i<X; i++) cnt_0 += (a[i] == 0);

    // Check if we can convert this 1st window into all 1s by <= K flips
    if(cnt_0 <= k) return true;

    // Slide the window across the array 
    // Can we convert any 1 among further X sized subarrays to all 1's, with <= k flips
    for(int i=X; i<n; i++) {
        cnt_0 += (a[i] == 0);    // Add the new element
        cnt_0 -= (a[i-X] == 0);    // Remove the starting element of the window

        // Any 1 among all subarrays of length X
        if(cnt_0 <= k) return true;
    }
    return false;
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n];
    for(int i=0; i<n; i++) cin >> a[i];

    // Apply BS on Ans to get maximum length subarray possible with at most k flips
    int ans=0;
    int lo=0, hi=n;
    while(lo <= hi) {   // O(NlogN)
        int mid = lo + ((hi-lo) >> 1);
        if(check(mid, a, k, n)) {
            ans = mid;
            lo = mid+1;
        } else hi = mid-1;
    }
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--)
    solve();
}
```
TC : $O(N \log N)$ 

---
__Approach - 3 (BS on Every Start)__
1. For each starting point L, determine the furthest point R where the subarray remains a "monotone space" (1111100000 i.e. we've to find last occurrence of 1)
2. For each L, there exists a monotone space on its right
3. A subarray is valid if it contains <= K zeros
4. Use binary search to find the maximum valid endpoint R (the point just before the (K+1)th zero)
5. Ensure the number of zeros in the subarray (L, R) is <= K
6. For each starting point, find the longest possible subarray and keep track of the maximum length across all starting points

__Code - 3__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// Can current range [st, end] be converted to all 1s by <= K flips
bool check(int st, int end, int a[], int k) {    // O(1) -> bcoz we've prefix sums
    int cnt_0 = a[end] - ((st) ? a[st-1] : 0);    // Partial sum
    return cnt_0 <= k;
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n];
    for(int i=0; i<n; i++) {
        int x;
        cin >> x;
        a[i] = 1-x;    // (or a[i] = !x) We can directly count 0's using prefix sum 
    }

    // Build prefix sum (p[i] gives number of 0s from start to ith index)
    for(int i=1; i<n; i++) a[i] += a[i-1];

    // Apply BS on Every start to get maximum length subarray possible with at most k flips
    // For each starting point, findlongest possible subarray and 
    // keep track of the maximum length across all starting points
    int ans=0;
    for(int st=0; st<n; st++) {    // O(NlogN)
        int lo=st, hi=n-1;
        int end=st-1;    // If all are 000000 (k can be 0 as well), then length of subarray should be equal to 0
        while(lo <= hi) {
            int mid = lo + ((hi-lo) >> 1);
            if(check(st, mid, a, k)) {
                end = mid;
                lo = mid+1;
            } else hi = mid-1;
        }
        int len = end-st+1;
        ans = max(ans, len);
    }
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--)
    solve();
}
```
TC : $O(N \log N)$

## Example-2 : No of subarrays you can make all `1`'s by `<= k` flips
Above question can be boiled down to the question, 
Find number of subarrays which contains `<= k` `0`'s 

__Approach__
1. For each starting point L, determine the furthest point R where the subarray remains a "monotone space" (1111100000 i.e. we've to find last occurrence of 1)
2. For each L, there exists a monotone space on its right
3. A subarray is valid if it contains <= K zeros
4. Use binary search to find the maximum valid endpoint R (the point just before the (K+1)th zero)
5. Ensure the number of zeros in the subarray (L, R) is <= K
6. For each starting point, find the longest possible valid subarray. The end of this longest subarray defines number of valid subarrays starting from this starting point, calculated as `(end - start + 1)`

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

// Can current range [st, end] be converted to all 1s by <= K flips
bool check(int st, int end, int a[], int k) {    // O(1) -> bcoz we've prefix sums
    int cnt_0 = a[end] - ((st) ? a[st-1] : 0);    // Partial sum
    return cnt_0 <= k;
}

void solve() {
    int n, k;
    cin >> n >> k;

    int a[n];
    for(int i=0; i<n; i++) {
        int x;
        cin >> x;
        a[i] = 1-x;    // (or a[i] = !x) We can directly count 0's using prefix sum 
    }

    // Build prefix sum (p[i] gives number of 0s from start to ith index)
    for(int i=1; i<n; i++) a[i] += a[i-1];

    // Apply BS on Every start to get maximum length subarray possible with at most k flips
    // For each starting point, findlongest possible subarray and 
    // keep track of the maximum length across all starting points
    int ans=0;
    for(int st=0; st<n; st++) {    // O(NlogN)
        int lo=st, hi=n-1;
        int end=st-1;    // If all are 000000 (k can be 0 as well), then no of subarrays should be equal to 0
        while(lo <= hi) {
            int mid = lo + ((hi-lo) >> 1);
            if(check(st, mid, a, k)) {
                end = mid;
                lo = mid+1;
            } else hi = mid-1;
        }
        int cnt_subarrays = end-st+1;    // Subarrays with start as st & end in (st, end] 
        ans += cnt_subarrays;
    }
    cout << ans << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    int _t; cin >> _t; while(_t--)
    solve();
}
```
TC : $O(N \log N)$

## Practice Problem : No of subarrays with distinct elements `<= k`
__Approach__

__Code__

## Example-3 : Good Pairs AZ101
__Problem Link__ : [Good Pairs AZ101](https://maang.in/problems/Good-Pairs-AZ101-377)

__Approach__
The given inequality $(A_i + A_j) > (B_i + B_j)$ is same as $(A_i - B_i) + (A_j - B_j) > 0$
Let $C_i = A_i - B_i$, you just need to find pairs such that $C_i + C_j > 0$

Store all values of $A_i - B_i$ in a vector and sort it. A question might arise that how can we sort the vector since the constraint $i < j$ is clearly mentioned. When we want to find pairs in a vector such that their sum is greater than 0, we can use the fact that addition is a commutative operation, which means the order in which we add the elements doesn't matter.

At no point during this process do we need to worry about losing track of original indices of the elements, because we can always interchange the indices of any two elements in a pair. For example, if we find a pair `(i,j)` where $i > j$, we can simply swap i and j to get the pair `(j,i)`. This means that even if we sort the vector, we can still consider all possible pairs and find the ones that satisfy condition $C_i + C_j > 0$.

Store all the values of $A_i - B_i$ in a vector $C$ and sort it. Since $C_j > -C_i$, we can use `upper_bound()` for finding the value of such pairs. For each start index in $C_i$, we need to find a smallest index `j` ahead of `i` whose value is just greater than $-C_i$, so that it results in a `sum > 0`. And if we're able to find out such a index, then all indexes after it would result in sum values greater than 0.  So if `end` stores that index `j`, then number of pairs that can be formed is calculated by `(n-1) - end + 1`

__Code__
```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long

void solve() {
    int n;
    cin >> n;

    int a[n], b[n];
    for(int i=0; i<n; i++) cin >> a[i];
    for(int i=0; i<n; i++) cin >> b[i];

    int c[n];
    for(int i=0; i<n; i++) c[i] = a[i]-b[i];
    sort(c, c+n);

    int cnt_good=0;
    for(int st=0; st<n; st++) {
        int end = upper_bound(c+st+1, c+n, -c[st]) - (c);
        cnt_good += ((n-1) - end + 1);
    }
    cout << cnt_good << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int _t; cin >> _t; while(_t--)
    solve();
}
```
TC : $O(N \log N)$