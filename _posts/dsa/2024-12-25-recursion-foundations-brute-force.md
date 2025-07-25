---
title: Recursion Foundations & Brute Force
date: 2024-12-25 8:00:00 +0530
categories: [DSA, Recursion & Backtracking]
tags: [recursion, brute force, backtracking, gcd, tower of hanoi, recursion tree]
math: true
mermaid: true
pin: false
---

## Basic Terminologies
**Recursion** is a programming concept where a function calls itself in order to solve a problem. It breaks down a problem into smaller, more manageable subproblems until it reaches a base case.

**Example of Recursion solution**
Find GCD of 2 numbers `a` and `b`
Use *Euclidean Algorithm*, which states that if `a = (b * q) + r`, then gcd(a, b) $\equiv$ gcd(b, r)
```cpp
gcd(int a, int b) {
	if(b == 0) {
		return a;
	}
	
	return gcd(b, a%b);
}
```

**Backtracking**, on the other hand, is a problem-solving technique that uses recursion in a brute-force manner. It tries all possible solutions to a problem, but it eliminates solutions that don’t work by "backtracking" to a previous step.

**Brute force** is a simple problem-solving paradigm where you exhaustively try all possible solutions. It's typically used for problems that don't have efficient algorithms, or in cases where the problem is relatively simple or implementation-heavy.

**Example of Brute Force solution**
Find no. of subarrays with sum equal to X
```cpp
int cnt = 0;

// Try all subarrays
for(int st=0; st<n; st++) {
	for(int en=st; en<n; en++) {
		int sum = 0;
		for(int i=st; i<=en; i++) {
			sum += arr[i];
		}
		if(sum == X) cnt++;
	}
}

return cnt;
```

## Problem - 1
Find all possibilities of two 5-digit numbers `abcde` & `fghij` such that it satisfies following conditions :
1. Given `N`, `fghij` completely divides `abcde` & gives `N` as the quotient, i.e. $$\frac{a\,b\,c\,d\,e}{f\,g\,h\,i\,j} = N$$
2. All digits of both numbers should be distinct 

Leading 0 is allowed
Constraints : $(1 \leq N \leq 80)$

**Approach - 1**
```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n = 62;
	string s = "0123456789";
	do {
		int num = stoi(s.substr(0,5));
		int den = stoi(s.substr(5,5));
		if(num == n * den) {
			cout << num << " " << den << '\n';
		}
	} while(next_permutation(s.begin(), s.end()));
}
```
TC : $O(10 \times 10!)$ (Just passed)

**Approach - 2**
Don't use condition `while(x != 0)` as it wouldn't count leading 0
```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n = 62;
	
	for(int abcde=01234; abcde<=98765; abcde++) {
	    if(abcde%n != 0) continue;
	    
	    int fghij = abcde/n;
	    set<int> st;    // To store distinct digits among both numbers
	    
	    int x = abcde;
	    for(int i=0; i<5; i++) {
	        st.insert(x%10);
	        x /= 10;
	    }
	    x = fghij;
	    for(int i=0; i<5; i++) {
	        st.insert(x%10);
	        x /= 10;
	    }
	    
	    if(st.size() == 10) {
	        cout << abcde << " " << fghij << '\n';
	    }
	}
	
	return 0;
}
```
Still Brute Force, but TC is faster than Approach-1

**NOTE**
What did we change in both of these strategies (Approach - 1 and Approach - 2) ?
This is something called the [Point of Pivot]({% post_url 2024-12-25-recursion-foundations-brute-force %}#point-of-pivot).
In *Approach - 1,* we considered the *2nd restriction* as the point of pivot.
In the *Approach - 2*, it was exactly the reverse — we considered the *1st restriction* as the point of pivot.

**Approach - 3** 
We can also use bitmasking
For any given digit, set the corresponding bit in the number
Finally, the pre-mask for the first 10 digits (0-9) should be equal to the number

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n = 62;
	
	for(int abcde=01234; abcde<=98765; abcde++) {
	    if(abcde%n != 0) continue;
	    
	    int fghij = abcde/n;
	    
	    int pre_mask = 0;
	    int x = abcde;
	    for(int i=0; i<5; i++) {
	        pre_mask |= (1<<(x%10));
	        x /= 10;
	    }
	    x = fghij;
	    for(int i=0; i<5; i++) {
	        pre_mask |= (1<<(x%10));
	        x /= 10;
	    }
	    
	    if(pre_mask == ((1<<10)-1)) {
	        cout << abcde << " " << fghij << '\n';
	    }
	}
	
	return 0;
}
```

## Point of Pivot
**Point of Pivot** refers to the equation from which we generate all possible options, typically the equation where we run the loop. The key is to choose the **Point of Pivot** with fewer options to optimize the process.

**Generation Strategy** :  
For generating solutions, always opt for the tighter equation. 
For example, in the 2nd approach, there are approximately $3.2 \times 10^6$ possible outcomes ($10!$ possibilities), whereas in the 1st approach, there are only $10^5$ possibilities. We generate solutions using the equation with fewer possibilities and later check the other cases.

In most problems in **DSA** (Data Structures and Algorithms) or **Competitive Programming (CP)**, we select a **Point of Pivot** around which we structure our iteration strategy.

## Recursion
Think of recursion as designing a unit that calls smaller instances of itself. It asks each instance to solve a smaller subproblem, and once all the values come back, it merges them and returns the final result.

Whenever you need to decode a recursion, what you draw is called a **Recursion Tree**.

**3 Levels of understanding Recursion** :
1. *Leap of Faith* 
   In most cases, we're gonna solve questions using [[Backtracking Framework#LCCM Framework for Backtracking|LCCM Framework]] only 
2. *Recursion Tree (or Dependency Tree)*
   From the Recursion Tree, you can compute the value yourself.
   In fact, this is exactly what the code is doing.
   The code cannot proceed in both directions simultaneously. 
   It first makes the left call, waits for it to complete, and then makes the right call.
   It runs sequentially from left to right, calculating whatever appears first.
   
   ![Recursion Tree.jpeg](/assets/img/dsa/Recursion%20Tree.jpeg)
3. *Recursion Stack (or Recursion Simulation)*
   What does the computer do ?
   Whenever it needs something new, a function is called. The program pauses at that point, moves to a new stack frame, and completes the operation.
   This is how the Recursion Stack works.
   When a function returns, its stack frame is deleted.
   These stack frames are created in between each recursive call.
   In recursion tree, DFS (Depth First Search) is being used to create these stacks.
   
   ![Recursion Stack.jpeg](/assets/img/dsa/Recursion%20Stack.jpeg)

**NOTE**
Have you ever encountered a "Stack Limit Exceeded" error (Runtime Error) ? 
This happens when the function has been called so many times that new stack frames keep getting created, eventually running out of memory.

**NOTE**
- Global variables can be accessed by all stack frames.
- A global variable is generally shared across all levels of recursion, and you can access it from any recursion level.
- By default, global variables are initialised to 0.

## Problem - 2
[Tower of Hanoi](https://www.mathsisfun.com/games/towerofhanoi.html) - Moving all disks from `A` to `C`

**Approach**
The idea for solving this problem is:
1. Before moving the yellow disk to C, I first need to move all the disks above it to `B`.
2. Then, I move the yellow disk to `C`.
3. Finally, I move all the disks from `B` to `C`.

*Steps* :
- Transfer the `X-1` smallest disks from `A` to `B`, using `C` as an auxiliary peg.
- Move the largest disk from `A` to `C`.
- Transfer the `X-1` disks from `B` to `C`, using `A` as an auxiliary peg.

All of these steps will be done recursively, so I’ll create a *recursive function* to implement this
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

void tower_hanoi(int x, int source, int target, int aux) {
    tower_hanoi(x-1, source, aux, target);
    cout << "Move disc " << x << " from " << source << " to " << target << '\n';
    tower_hanoi(x-1, aux, target, source);
}

void solve() {
	// Move 4 disks from peg 1 to peg 3
    tower_hanoi(4, 1, 3, 2);
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    cin >> n;
    for(int i=0; i<n; i++) {
        int x;
        cin >> x;
        available.insert(x);
    }
    
    solve();
    return 0;
}
```
You can verify the solution by simulating the printed output in the game.
## Exercise
```cpp
#include<bits/stdc++.h>
using namespace std;

int ans = 0;

int rec(int x) {
    if(x <= 3) return x;
    ans += rec(x-2);
    return rec(x-1) + rec(x-3);
}

int main() {
	cout << rec(6) << '\n';
	cout << ans << '\n';
	
	return 0;
}
```
Understand how this recursive function works and what the code is doing by using the [Code Execution Visualizer](https://pythontutor.com/render.html#mode=edit).
