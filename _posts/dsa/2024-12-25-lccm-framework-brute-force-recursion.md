---
title: LCCM Framework & Brute Force Recursion
date: 2024-12-25 10:10:00 +0530
categories: [DSA, Recursion & Backtracking]
tags: [recursion, backtracking, brute force, lccm, framework, subsets, permutations]
math: true
mermaid: true
pin: false
---

## LCCM Framework for Backtracking
To write an efficient Backtracking code, there are only 4 key steps you need to follow :
1. **Level** – A way to iterate over the entire solution space efficiently
2. **Choice** – For each level, determine the possible moves to reach the next level
3. **Check** – For each choice, validate if current partial solution is valid according to problem's constraints
4. **Move** – If the choice is valid, evaluate the branch by using **[Recursion]({% post_url 2024-12-25-recursion-foundations-brute-force %}#recursion)**

```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long 

void rec(int level) {
    // *** Pruning (Optional) ***
    // If there are conditions to stop recursion early based on the problem, 
    // you can add them here to avoid unnecessary computation.
    
    // *** Base Case ***
    // Define the stopping condition for recursion.
    if (/* base condition */) {
        // Perform validation to check if the current state is a valid solution.
        if (check()) { 
            // If valid, process the solution (e.g., count, store, or print it).
        }
        return;  // End this recursion branch.
    }
    
    // *** Recursive Case ***
    // Iterate through all possible choices at the current level.
    for (int ch = 0; ch < choices; ch++) {
        // *** Check ***
        // Verify if the current choice is valid based on the problem's constraints.
        if (check(ch)) {
            // *** Move ***
            // Apply the current choice to the state (place modifications).
            /* place modifications */ 
            
            // *** Recurse ***
            // Move to the next level in the solution space.
            rec(level + 1);
            
            // *** Unplace ***
            // Undo modifications made to shared datastructure during place to backtrack.
            /* unplace modifications */
        }
    }
}

void solve() {
    rec(0);
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); 
    cout.tie(0);
    
    solve();
    return 0;
}
```
**STATE**
In general, **state** means the *current configuration* or *status* of all the elements involved in the problem at a particular point in time. It is essentially a snapshot of all the relevant information about the problem's progress.

States can be made very efficient by choosing the right representation of the system's configuration. This can significantly reduce the complexity of exploring the solution space.

**Meaning of Recurrence**
You’ve already made decisions for levels up to `level-1`. 
Now, you need to make decisions for the current level and all the subsequent levels.

**NOTE**
There are 2 types of checks in Backtracking :
1. *Check valid in base case* – check the validity of the solution at the base case of the recursion
2. *Check at every choice* – check if a particular choice is allowed before making that choice

**NOTE**
Before the base case, we may sometimes add *pruning code*.
*Pruning* helps in optimisation by cutting down unnecessary branches, but it never reduces the time complexity (TC).

**NOTE**
There are always at least 2 data structures :
1. One for storing all the answers (to accumulate results)
2. One for saving the current state during the process

**NOTE**
In *counting problems* using *backtracking* or *recursion*, whenever you reach the *base case* :
- If it's a *valid state*, always return 1 (indicating a valid solution).
- If it's an *invalid state*, return 0 (indicating an invalid solution).

## Problem - 1
Generate all N length balanced parenthesis with maximum depth equal to K 

**Approach - 1**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n, k;
vector<string> all_pers;
string curr_per;

// Is current string balanced with max depth = k ?
bool check() {
    int depth = 0, max_depth = 0;
    for(auto it:curr_per) {
        if(it == '(') depth++;
        else {
            depth--;
            if(depth < 0) return false;
        }
        max_depth = max(max_depth, depth);
    }
    
    return (depth == 0 && max_depth == k);
}

void rec(int level) {    // level -> index
    // Base case 
    if(level == n) {
        if(check()) {    // Check 
            all_pers.push_back(curr_per);
        }
        return;
    }
    
    // Recursive case 
    // Explore all choices (choice -> '(' or ')')
    // Choice 1 - Open '('
    if(1) {    // Check per choice
        // Move
        curr_per += '(';    // Place
        rec(level + 1);    // Next recursive call
        curr_per.pop_back();    // Unplace
    }
    // Choice 2 - Open ')'
    if(1) {    // Check per choice
        // Move
        curr_per += ')';    // Place
        rec(level + 1);    // Next recursive call
        curr_per.pop_back();    // Unplace
    }
}

void solve() {
    rec(0);
    
    for(auto it:all_pers) cout << it << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    cin >> n >> k;
    
    solve();
    return 0;
}
```
TC : $O(N \times 2^N)$

**Approach - 2**
If *Approach - 1* doesn't seem efficient, we can add more parameters to recursive function to optimize it.
For example, if we are repeatedly calculating the `max_depth` at every step, but if I keep track of it as a parameter, I can avoid recomputing it each time and check it more efficiently.
If I pass both `depth` and `max depth` as parameters within the recursion itself, then I can directly use these values in conditions, without the need for additional checks or recalculations.
For instance, I could write a condition like this, 
If at the end, `max depth == k` and `depth == 0`, then accept the solution.
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n, k;
vector<string> all_pers;
string curr_per;

void rec(int level, int depth = 0, int max_depth = 0) {    // level -> index
    // Pruning 
    if(depth < 0 || max_depth > k) return;
    
    // Base case 
    if(level == n) {
        if(depth == 0 && max_depth == k) {    // Check 
            all_pers.push_back(curr_per);
        }
        return;
    }
    
    // Recursive case 
    // Explore all choices (choice -> '(' or ')')
    // Choice 1 - Open '('
    if(1) {    // Check per choice
        // Move
        curr_per += '(';    // Place
        rec(level + 1, depth + 1, max(max_depth, depth + 1));    // Next recursive call
        curr_per.pop_back();    // Unplace
    }
    // Choice 2 - Open ')'
    if(1) {    // Check per choice
        // Move
        curr_per += ')';    // Place
        rec(level + 1, depth - 1, max(max_depth, depth - 1));    // Next recursive call
        curr_per.pop_back();    // Unplace
    }
}

void solve() {
    rec(0);
    
    for(auto it:all_pers) cout << it << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    cin >> n >> k;
    
    solve();
    return 0;
}
```
There's no need to check the validity of `depth + 1` or `depth - 1` manually, because pruning will handle that for us.

Will this ever explore an invalid case too much?
As soon as a case becomes invalid, the code will immediately return (due to pruning). So, that invalid path will never be explored further.

The code is small because no separate check  is needed.
Additionally, the exploration is reduced, and the solution is found much faster.

## Problem - 2
Generate all permutations of a number having distinct digits

**Code**
Any element that has been used from the set will no longer be available for the next level
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
vector<vector<int>> all_pers;
vector<int> curr_per;
set<int> available;

void rec(int level) {    // level -> index
    // Base case 
    if(level == n) {
        if(1) {    // Check
            all_pers.push_back(curr_per);
        }
       return;
    }
    
    // Recursive case 
    // Explore all choices (choice -> elements which haven't been used yet)
    set<int> temp = available;
    for(auto v:temp) {
        if(1) {    // Check per choice
            // Move 
            curr_per.push_back(v);    // Place
            available.erase(v); 
            rec(level + 1);    // Next recursive call
            available.insert(v);    // Unplace
            curr_per.pop_back();
        }
    }
}

void solve() {
    rec(0);
    
    cout << all_pers.size() << '\n';    // Number of permutations 
    for(auto v:all_pers) {
        for(auto x:v) {
            cout << x << " ";
        }
        cout << '\n';
    }
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
I generally try not to use the same set for iteration that I'm modifying. 
I never erase elements from it. Instead, I just create another copy of the set for iteration.

## Problem - 3
Print all subsequences or subsets of an array, not subarrays (which are continuous portions)
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
vector<int> arr;
vector<int> curr;

void rec(int level) {    // level -> index
    // Base case
    if(level == n) {
        if(1) {    // Check
            for(auto it:curr) cout << it << " ";
            cout << '\n';
        }
        return;
    }
    
    // Recursive case
    // Explore all choices (choice -> take/not take the element)
    // Choice 1 - Not take 
    if(1) {    // Check per choice
        // Move
        rec(level + 1);    // Next recursive call
    }
    // Choice 2 - Take 
    if(1) {    // Check per choice
        // Move
        curr.push_back(arr[level]);    // Place
        rec(level + 1);    // Next recursive call
        curr.pop_back();    // Unplace
    }
}

void solve() {
    rec(0);
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    cin >> n;
    arr.resize(n);    // 0-based
    for(int i=0; i<n; i++) {
        cin >> arr[i];
    }
    
    solve();
    return 0;
}
```
TC : $O(N \times 2^N)$  
