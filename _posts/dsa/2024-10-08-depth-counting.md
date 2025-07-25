---
layout: post
title: "Depth Counting & Next Greater Element"
date: 2024-10-08
categories: [DSA]
math: true
tags: [stack, parentheses, NGE, monotonic-stack, segment-tree, precompute]
---

## Depth Counting 
Depth Counting in C++ generally refers to tracking the level of "nesting" or "depth" while traversing or parsing a structure, such as tree, graph, or string.

In case of Balanced Parentheses, depth counting helps us track the maximum depth of nested parentheses. This is particularly useful when we want to ensure that parentheses are balanced and properly nested in expressions.

## Balanced Parentheses (Variation-1 : Single Type of Parentheses)
Balanced Parentheses means that : 
-  Every opening parenthesis `(` has a corresponding closing parenthesis `)`
- The parentheses are correctly nested, i.e., for every opening parenthesis `(`, the first unmatched closing parenthesis `)` must match it

__Dry Run__

![Balanced Parentheses.jpeg](/assets/img/dsa/Balanced%20Parentheses.jpeg)

__Solution__
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	string s;
	cin >> s;

	bool isBalanced = 1;
	int depth = 0;    // Keeps track of how many unclosed opening parenthese are there 
	for(auto ch:s) {
		if(ch == '(') {
			depth++;
		} else {
			depth--;
		}

		// If at any point depth becomes -ve
		// It means that no. of closing parentheses > no. of opening parentheses
		if(depth < 0) {
			isBalanced = 0;
			break;
		}
	}

	// If depth > 0, unclosed opening parentheses are remaining 
	if(depth) isBalanced = 0;

	if(isBalanced) cout << "Balanced" << '\n';
	else cout << "Not Balanced" << '\n';

	return 0;
}
```
TC : $O(N)$
SC : $O(1)$


## Balanced Parentheses (Variation-2 : Multiple Types of Parentheses)
__Problem Link__ : [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

__Platform__ : #Platform-LeetCode 

__Difficulty__ : #Difficulty-Easy

Can't be solved using 3 variables, for understanding dry run `{ [ ( ] ) } ( )` which isn't balanced

Closing of parenthesis should be done in exactly the reverse of order in which they appeared i.e. current Closing bracket should match the last unclosed Opening bracket

```cpp
class Solution { 
public: 
	bool isValid(string s) { 
		unordered_map<char, int> hash; // {parenthesis, mapped_number} 
		hash['('] = 1; 
		hash['['] = 2; 
		hash['{'] = 3; 
		hash[')'] = -1; 
		hash[']'] = -2; 
		hash['}'] = -3; 
		
		stack<int> st; // Stores mapped_number 
		bool isBalanced = 1; 
		
		for(auto ch:s) { 
			if(hash[ch] > 0) { 
				st.push(hash[ch]); 
			} else { 
				// Parentheses matching logic
				if(!st.empty() && hash[ch] + st.top() == 0) { 
					st.pop(); 
				} else return false; 
			} 
		} 

		// If stack isn't empty, that means some opening parentheses are still unclosed
		return (isBalanced && st.empty()); 
	} 
};
```
TC : $O(N)$
SC : $O(N)$
Keeping map makes it easier to add new brackets without the need of manipulating the main code

## Balanced Parentheses (Variation-3 : Query) \[CHALLENGE PROBLEM]
You would be give a string `s` of size `N` containing `(` and `)`. You would be then given `q` queries in form of `? L R`, and you have to tell whether the substring from `L` to `R` is balanced or not.

__Rephrasing the question to a bit easier version__
Count the number of substrings that are balanced. 

__1st variation__ Solve it for $N \leq 10^3$
__2nd variation__ Solve it for $N \leq 10^5$

__HINT__ : Try drawing the depth values in form of mountain structures 

For Query, L to R you might need some data structure, known as Segment Tree

## Next Greater Element (NGE)
For every index you've to find the next index where the value is greater than the value at current index
NGE\[i] $\rightarrow$ index of next greater element
Like NGE for `{5, 4, 2, 1, 3}` would be `{5, 5, 4, 4, 5}`
In case NGE of an element doesn't exist, then take size of array as NGE of that element

If a certain thing depends on things after it, then we process right to left (like `NGE[i]` always depends on elements present at right of `i`). Processing from right to left will help us build some more information by the time we reach a particular index & then we can use that information to calculate it faster, because $O(N)$ for whole array is like $O(1)$ per index.

__Approach-1__

Using Monotonic Stack (inserting in strictly decreasing order)
- Start traversing from right to left
- Kill all elements from stack which are smaller than currently encountered element 
- If after all killings, if alive element(s) are left in stack, then it's the NGE, otherwise NGE doesn't exist
- Push the currently encountered element in the stack

__Dry Run__

![Nge-1.jpeg](/assets/img/dsa/Nge-1.jpeg)

__Solution__
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n;
	cin >> n;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	int nge[n];
	stack<int> alive;    // Stores indexes of elements that are alive (haven't killed yet)

	for(int i=n-1; i>=0; i--) {
		// Maintain the decreasing order of stack by killing smaller elements 
		while(!alive.empty() && arr[alive.top()] <= arr[i]) {
			alive.pop();    // Runs for N times
		}
		
		// If after all killings, something is alive, means it's my next greater
		// Else next greater doesn't exists, so assign size of array as next greater
		if(!alive.empty()) nge[i] = alive.top();
		else nge[i] = n;

		// Make the current element as alive 
		alive.push(i);
	}

	// Print the nge 
	for(int i=0; i<n; i++) cout << nge[i] << " ";

	return 0;
}
```
TC : $O(N)$ $\,\,\,\,\text{(Amortised Time Complexity)}$
SC : $O(N)$

---
__Approach-2__

Without using any extra space
- Start traversing from right to left
- By default, take next index as nge i.e. `nge[i] = i+1`
- Till the nge exists & value we assigned to it is wrong, then assign next greater of nge as current nge i.e. `nge[i] = nge[nge[i]]`

If you're not greater than me, then i'll check with your's next greater element & so on
Because if you can't be my next greater, then any element between you and your next greater can't be my answer (because they'll are smaller than you), that's why i directly jump to your next greater element

The hopping going on here, is similar to killing of smaller elements like we were doing in Approach-1 

__Dry Run__

![Nge-2.jpeg](/assets/img/dsa/Nge-2.jpeg)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n;
	cin >> n;

	int arr[n];
	for(int i=0; i<n; i++) cin >> arr[i];

	int nge[n];

	for(int i=n-1; i>=0; i--) {
		// By default, take nwext index as nge
		nge[i] = i+1;

		// Till the nge exists & it's assigned value is wrong,
		// Keep on assigning next greater of nge as current nge (HOPPING)
		while(nge[i] != n && arr[i] >= arr[nge[i]]) {
			nge[i] = nge[nge[i]];
		}
	}

	// Print the nge 
	for(int i=0; i<n; i++) cout << nge[i] << " ";

	return 0;
}
```

TC : $O(N)$ $\,\,\,\,\text{(Amortised Time Complexity)}$
SC : $O(1)$