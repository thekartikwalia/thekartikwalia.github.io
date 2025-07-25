---
title: Kth Solution
date: 2024-12-25 11:00:00 +0530
categories: [DSA, Recursion & Backtracking]
tags: [kth solution, recursion, tower of hanoi, recurrence]
math: true
mermaid: true
pin: false
---

## Kth Solution
Finding the **Kth solution** to a problem can be viewed as a **recurring problem** in itself.

**How to handle the Kth solution ?**
Handling the *Kth solution* is a very generic approach, and it typically involves a recursive process.
1. **Problem Setup**  
    Suppose you are tasked with solving an instance of a problem with *X items*. Let’s assume that the *Kth move* or *Kth solution* lies within this instance.
2. **Recursive Breakdown**  
    Within this instance, there are multiple possible moves or subproblems. 
    The *Kth solution* can lie within any of these subproblems.
3. **Counting the Moves**  
    To find the *Kth solution*, you need to track how many moves are being made in each recursive call. This helps determine whether the *Kth solution* is within the current recursive instance or if you need to explore other recursive branches.
4. **Optimizing the Search for Kth Solution**  
   If the operation involves multiple processes or steps (e.g., first process, second process, third process), and if you can decide which branch to explore based on these processes, you can quickly determine the *Kth solution* without exploring all branches. 
   By deciding in advance which branch will lead to the *Kth solution*, you can avoid unnecessary calculations and directly jump to the right branch, making the search faster.

**NOTE**
We don’t use the [[Backtracking Framework#LCCM Framework for Backtracking|LCCM Framework]] for finding the *Kth solution*, because it's a *recursion problem*, not a *backtracking problem*.

## Problem - 1
Find Kth Solution of [Tower of Hanoi](https://www.mathsisfun.com/games/towerofhanoi.html)

**Approach**
To determine the *Kth solution*, I need to see how many moves are made in each recursive call. I can count that fairly quickly because, in the *Tower of Hanoi*, there’s a known recurrence relation:
$$T(n) = 2 T(n−1) + 1$$
This recurrence leads to the solution :
$$T(n) = 2^n − 1$$

In the *Tower of Hanoi*, if we have `N` disks and need to move them from peg `A` to peg `B`, it will take exactly *$2^N - 1$* moves, which comes directly from solving the recurrence.
```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long 

void kth_move(int disc, int source, int target, int aux, int k) {
    // Move disc-1 disks from source to aux -> (2^(disc-1)) - 1
    if(k <= ((1<<(disc-1))-1)) {
        kth_move(disc-1, source, aux, target, k);
    }
    // Move 1 disc from source to target -> 1
    else if(k == (1<<(disc-1))) {
        cout << "Moving disc " << disc << " from " << source << " to " << target << '\n';
        return;
    }
    // Move disk-1 disks from aux to target -> (2^(disc-1)) - 1
    else {
        kth_move(disc-1, aux, target, source, k-(1<<(disc-1)));
    }
}

void solve() {
    for(int i=1; i<=7; i++) {
        kth_move(3, 1, 3, 2, i);
    }
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); 
    cout.tie(0);
    
    solve();
    return 0;
}
```
Additionally, this recurrence works in *linear time* because the solution involves simple conditional checks (either `if`, `else if`, or `else`), which aren’t exponential in nature.

Therefore, the recurrence *$T(n) = 2 T(n−1) + 1$* leads directly to the next smaller subproblem.

This makes the problem *linear* with respect to the number of disks `N`, rather than exponential.