---
layout: post
title: "Budget Problem Variations"
date: 2024-10-08
categories: [DSA]
math: true
tags: [prefixSum, precomputation, greedy, binary search]
---

## Budget Problem (Variation-1: Single Budget)
You're given an array A of size N, where `A[i]` denotes the cost of ith item. And you're also given a budget B, you've to tell how many maximum number of items could you buy with given budget.

Sort the array A and keep buying the smallest item until budget B is reached (*Greedy*)
```cpp
int main() {
	int n;
	cin >> n;

	vector<int> arr(n);
	for(int i=0; i<n; i++) cin >> arr[i];
	sort(arr.begin(), arr.end());    // Sort items by prices

	int b;
	cin >> b;
	
	int cnt = 0;
	for(int i=0; i<n; i++) {
		if(arr[i] <= b) {
			cnt++;
			b -= arr[i];
		} else break;
	}
	cout << cnt << '\n';
	
	return 0;
}
```
## Budget Problem (Variation-2: Budget Queries)
You're given an array A of size N, where `A[i]` denotes the cost of `i`th item. And you're also given M queries with budget B, and for each query you've to tell how many maximum number of items could you buy with given budget. ($N \leq 10^{5} \text{ and } M \leq 10^{5}$)

__Approach-1__
Brute Force, just loop over the previous Approach (discussed above)
```cpp
int main() {
	int n;
	cin >> n;

	vector<int> arr(n);
	for(int i=0; i<n; i++) cin >> arr[i];
	sort(arr.begin(), arr.end());    // Sort items by prices

	int m;
	cin >> m;

	while(m--) {
		int b;
		cin >> b;
	
		int cnt = 0;
		for(int i=0; i<n; i++) {
			if(arr[i] <= b) {
				cnt++;
				b -= arr[i];
			} else break;
		}
		cout << cnt << '\n';
	}
	
	return 0;
}
```
TC : $O(M \times N + N\log N)$
This TC comes out to be $O(10^{10})$ which will never pass for 1 sec time limit

---
__Approach-2__
After sorting, build prefixSum array
Since we want the maximum number of items we can buy with given budget, so it's simply the number of entries in prefixSum which are less than or equal to given budget

Since prefixSum is built after sorting the array, so prefixSum is itself sorted 
Hence, we can apply upper bound to calculate number of entries less than or equal to budget 

__Dry Run__

![Dry run (Budget Variation-2).jpeg](/assets/img/dsa/Dry%20run%20(Budget%20Variation-2).jpeg)

__Code__
```cpp
int main() {
	int n;
	cin >> n;

	vector<int> arr(n);
	for(int i=0; i<n; i++) cin >> arr[i];
	sort(arr.begin(), arr.end());    // Sort items by prices

	// Build prefixSum 
	vector<int> preSum(n);
	for(int i=0; i<n; i++) {
		preSum[i] = arr[i];
		if(i) preSum[i] += preSum[i-1];
	}

	int m;
	cin >> m;
	while(m--) {
		int b;
		cin >> b;

		int cnt = upper_bound(preSum.begin(), preSum.end(), b) - preSum.begin();
		cout << cnt << '\n';
	}

	return 0;
}
```
TC : $O(N + M + N\log N)$
This TC comes out to be lesser than $O(10^{8})$ which will always pass for 1 sec time limit

__NOTE__ : For questions having queries, we generally prefer _Precomputation_