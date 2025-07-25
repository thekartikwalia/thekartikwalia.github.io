---
title: Interval DP (Form 4)
date: 2024-01-15 10:00:00 +0530
categories: [DSA, Dynamic Programming]
tags: [interval dp, lr dp, dp on segments, matrix chain multiplication, rod cutting]
math: true
mermaid: true
pin: false
---

## Form 4 - Interval DP or LR DP
### **Transition**

$$DP(L, R, X) \rightarrow Y$$

It returns optimal value of $Y$ for segment $A[L \dots R]$

### **Identifying LR DP Problems**

1. *Merging & Array Shrinking*  
    Tasks that involve **combining elements and reducing the size of the array** naturally fit into the Left-Right (LR) DP framework.  
    Example: Merging matrices in matrix chain multiplication, merging palindromic substrings, or reducing an array by combining adjacent elements with specific costs.
    
2. *Bracket Placement*  
    Problems that require determining the **optimal order of merging by strategically placing brackets** also fall under LR DP.  
    Example: Determining the minimum number of scalar multiplications in matrix chain multiplication or finding the optimal way to parenthesize expressions.
    

### **Thinking about Transitions in LR DP**

- When you have to **delete a segment, array, or club elements in a subarray**, think about **where the first or last element** of the subarray will belong.
- **Key Idea**: Focus on the **role of the first or last element** in the merge:
    - Which subarray will it be a part of?
    - How will the merging depend on this element?
- Iterate on that element to **design the transition**. This approach ensures that every possible scenario for merging or breaking the subarray is considered.

In **Form-4**, it’s helpful to think from the end. By considering how the final merge will occur and how the last two subarrays combine, transitions become easier to write. Understanding that the final merge combines two smaller subarrays helps structure the DP solution effectively.

By combining these ideas, you can model tasks like **optimal merging**, **bracket placement**, and **cost minimization** effectively using Interval DP.

### **Form-2 vs Form-4**

When trying to identify whether a problem falls under **Form-2** or **Form-4**, the key distinction lies in the final merge step and the structure of the problem.

**Form-2** is typically used when the goal is to break a problem into smaller subproblems without requiring a final merge step. This form focuses on recursively dividing a problem into subarrays or smaller tasks. The emphasis is on solving the problem by breaking it down, rather than on how to combine the results of those subproblems afterward.

**Form-4**, on the other hand, is suited for problems where multiple merges occur, and the results of these subproblems must eventually be combined into the final solution. These problems often involve **nested merges**, such as merging matrices, elements with specific costs, or segments of an array. The key idea in Form-4 is that after dividing the problem into smaller parts, we need to merge or combine these parts in a way that affects the overall result, such as minimizing costs or maximizing some value.

### **When to choose Form-4 ?**

**Form-4** is more suitable when there is a need to repeatedly merge elements or subarrays, especially when the total number of operations grows high (e.g., $N^2$ or $N^3$). If the problem has large constraints (such as $N=500$ or $N=100$), this is a strong indication that **Form-4** should be considered, as it naturally leads to quadratic or cubic time complexity. Form-4 is ideal when there's a **final merge step**, and merging happens in multiple stages or across nested subarrays.

In contrast, **Form-2** is not about final merges but focuses on splitting a problem into smaller subproblems that can be solved independently without combining them afterward.

---

## Example-1 : Rod Cutting
You are given a rod of length `n`, and you want to cut it into smaller segments at specified positions to minimise the total cost of cutting. The cost of each cut is equal to the length of the rod being cut at that time.

You are provided an array of integers, `x`, which contains the positions along the rod where cuts can be made. The task is to determine the minimum total cost required to perform all the necessary cuts.

**Code**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
int x[1001];
int dp[1001][1001];

int rec(int L, int R) {
    // Pruning: Skip invalid cases (already handled by constraints in the loop)
    // Base case: If only one segment between L and R, no cost for cutting
    if(L + 1 == R) {
        return 0;
    }
    
    // Cache check
    if(dp[L][R] != -1) {
        return dp[L][R];
    }
    
    // Transition: Minimize the cost by trying all possible partitions
    int ans = 1e9;
    for(int k = L + 1; k <= R - 1; k++) {
        ans = min(ans, (x[R] - x[L]) + rec(L, k) + rec(k, R));
    }
    
    // Save and return
    return (dp[L][R] = ans);
}

void solve() {
    cin >> n;
    for(int i = 1; i <= n; i++) {
        cin >> x[i];
    }
    x[0] = 0;    // Initialize the start of the rod to 0 for easier calculations
    memset(dp, -1, sizeof(dp));  // Mark all dp states as uncomputed
    
    // Recurrence Meaning:
    // rec(L, R): Minimum total cost of cutting the portion of the rod from L to R
    cout << rec(0, n) << '\n';    // Solve for the entire rod from 0 to n
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    solve();
    return 0;
}
```
TC : $O(N^3)$

*Follow up Problem* : Can you solve it better than $O(N^3)$ ?

---

## Example-2 : Matrix Chain Multiplication
You are given `n` matrices, where the dimensions of the $i^{th}$ matrix are $x[i] \times y[i]$. Your task is to find the most efficient way to multiply these matrices together such that the total number of scalar multiplications is minimised.

**Code**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
int x[101], y[101];
int dp[101][101];

int rec(int L, int R) {
	// Pruning: Skip invalid cases (already handled by constraints in the loop)
    // Base case: If there's only one matrix, no multiplication is needed
    if(L == R) {
        return 0;
    }
    
    // Cache check
    if(dp[L][R] != -1) {
        return dp[L][R];
    }
    
    // Transition: Try all possible places to split the matrices between L and R
    int ans = 1e9;
    for(int mid=L; mid<=R-1; mid++) {
        // Recursively calculate the cost for multiplying the two parts
        int cost_mul = x[L] * y[mid] * y[R];    // Cost of multiplying resultant matrices from L to mid, and from mid+1 to R
        ans = min(ans, rec(L, mid) + rec(mid+1, R) + cost_mul);
    }
    
    // Save and return
    return dp[L][R] = ans;
}

void solve() {
    cin >> n;
    for(int i = 1; i <= n; i++) {
        cin >> x[i] >> y[i];
    }
    
    memset(dp, -1, sizeof(dp));
    
    // Minimum cost to multiply all matrices from 1 to n
    cout << rec(1, n) << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    solve();
    return 0;
}
```
TC : $O(N^3)$

*Input & Output*
```cpp
// Input
3
10 30
30 5
5 60

// Output
4500
```

### *Follow up Problem* : Print order of multiplying these matrices

**Approach**

For every matrix, there will be a certain number of brackets placed on the left and right of it, depending on how the multiplication is split. To determine this, we use a `back` array, which stores the optimal splitting point for every subproblem `[L, R]`. This splitting point tells us where to divide the sequence of matrices to achieve the minimum cost.

After calculating the minimum cost using dynamic programming, we recursively use the `back` array to generate the bracket positions.

**Code**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
int x[101], y[101];

int dp[101][101];
int back[101][101];
int rec(int L, int R) {
	// Pruning: Skip invalid cases (already handled by constraints in the loop)
    // Base case: If there's only one matrix, no multiplication is needed
    if(L == R) {
        return 0;
    }
    
    // Cache check
    if(dp[L][R] != -1) {
        return dp[L][R];
    }
    
    // Rransition: Try all possible places to split the matrices between L and R
    int ans = 1e9;
    for(int mid=L; mid<=R-1; mid++) {
        // Recursively calculate the cost for multiplying the two parts
        int cost_mul = x[L] * y[mid] * y[R];    // Cost of multiplying resultant matrices from L to mid, and from mid+1 to R
        if((rec(L, mid) + rec(mid + 1, R) + cost_mul) < ans) {
            // If we found a better solution, then in back[L][R] we store that where should we break [L...R]
            ans = rec(L, mid) + rec(mid + 1, R) + cost_mul;
            back[L][R] = mid;
        }
    }
    
    // Save and return
    return dp[L][R] = ans;
}

// Store opening and closing brackets for every matrix
int op_b[101];
int cl_b[101];
void generate(int L, int R) {
    if(L == R) {
        return;
    }
    
    // If we're merging [L...R], then we've to put open before L and close after R
    op_b[L]++;
    cl_b[R]++;
    
    int mid = back[L][R];
    generate(L, mid);
    generate(mid+1, R);
}

void solve() {
    cin >> n;
    for(int i = 1; i <= n; i++) {
        cin >> x[i] >> y[i];
    }
    
    memset(dp, -1, sizeof(dp));
    
    // Minimum cost to multiply all matrices from 1 to n
    cout << rec(1, n) << '\n';
    
    // Print order in which we've to multiply matrices
    generate(1, n);
    for(int i=1; i<=n; i++) {
        for(int x=0; x<op_b[i]; x++) cout << "(";
        cout << " " << i << " ";
        for(int x=0; x<cl_b[i]; x++) cout << ")";
    }
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    solve();
    return 0;
}
```

*Input & Output*
```cpp
// Input
3
10 30
30 5
5 60

// Output
4500 
(( 1 2 ) 3 )
```

---

## Example-3 : Palindrome Partitioning II
Find the minimum number of break points to partition the string into palindromic substrings.

**Approach**

First, preprocess the range `[L...R]` to check if it is a palindrome in constant time (`O(1)`) using dynamic programming. The preprocessing step has a complexity of `O(N^2)`. After preprocessing, querying whether a range is a palindrome becomes efficient.

Instead of directly solving the problem with a heavier complexity (Form-4), we simplify the approach by designing transitions based on the last subpart (Form-2). This means calculating the minimum cuts for the prefix `[1...i]` by iterating over all possible points `j`, where the substring `[j+1...i]` is a palindrome.

**Code**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long 

int n;
string s;

int dp_1[1010][1010];
int rec_1(int L, int R) {
    // pruning
    // base case: single-character or empty strings are palindromes
    if(L >= R) {
        return 1;
    }
    
    // cache check
    if(dp_1[L][R] != -1) {
        return dp_1[L][R];
    }
    
    // transition
    int ans = 0;
    // use 0-based indexing for string `s` bcoz L & R are passed as 1-based indices
    if((s[L-1] == s[R-1]) && rec_1(L+1, R-1)) {
        ans = 1;
    }
    
    // save and return
    return (dp_1[L][R] = ans);
}

int dp_2[1010];
int rec_2(int i) {
    // pruning
    // base case: rec_2(0) = -1 to handle the extra cut at the start of the string
    // To make ans = 1 + rec_2(0) = 0, as in that case we didn't add any cut
    if(i == 0) {
        return -1;
    }
    
    // cache check
    if(dp_2[i] != -1) {
        return dp_2[i];
    }
    
    // transition
    int ans = 1e9;
    for(int j=0; j<i; j++) {
        // check if the substring [j+1...i] is a palindrome
        if(rec_1(j+1, i)) {
            ans = min(ans, 1 + rec_2(j));
        }
    }
    
    // save and return
    return (dp_2[i] = ans);
}

void solve() {
    cin >> n;
    cin >> s;
    
    memset(dp_1, -1, sizeof(dp_1));    // dp_1 for checking palindromes
    memset(dp_2, -1, sizeof(dp_2));    // dp_2 for minimum cuts
    
    // Recurrence Meaning:
    // rec_1(L, R): Returns whether the range [L...R] is a palindrome or not
    // rec_2(i): Minimum # of cuts required to partition [1...i] into palindromes
    cout << rec_2(n) << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    solve();
    return 0;
}
```
Even without memoisation `rec_1(L, R)` is $O(R-L)$, as at each step it gets reduced by 2
Since, we could make `rec_1(L, R)` $O(1)$, that's why `rec_2(x)` resulted in $O(N^2)$

TC : $O(N^2)$

*Input & Output*
```cpp
// Input
11
abacacadaca

// Output
2    // "aba", "c", "acadaca"
```

---

## Example-4 : You are given N elements, in an array A. You can take any 2 consecutive elements a and b and merge them. On merging you get a single element with value `(a+b)%100` and this process costs you `a*b`. After merging you will place this element in place of those 2 elements. Find the Minimum cost to merge all the elements into a single element.

Constraints: $N <= 500$ and $A[i] <= 100$

The key observation in this problem is that once we merge a subarray `[L...R]`, the sum modulo 100 of that subarray is fixed, and this can be leveraged to efficiently calculate the merging cost. The final merged element for any range will always be the sum of that range modulo 100. This allows us to focus on minimizing the cost of merging subarrays while keeping track of the sum modulo 100.

To solve the problem using LR DP, we define a state `rec(L, R)`, representing the minimum cost to merge the segment `[L...R]` into one element.

For each subarray `[L...R]`, the final merged element is formed by merging two smaller subarrays, `[L...mid]` and `[mid+1...R]`, where `mid` is any point between `L` and `R`. By recursively computing the merge costs for the left and right subarrays, we can find the minimum cost of merging the entire range `[L...R]`. The merging cost is influenced by the sum modulo 100 of each subarray.

The approach involves iterating over all possible split points within each subarray, and using DP to store the intermediate results. By recursively solving for all possible subarrays and merging their results optimally, we can compute the minimum cost to merge the entire array.

**Code**
```cpp
#include<bits/stdc++.h>
using namespace std;

#define int long long

int n;
int A[501];

int dp[501][501];
int rec(int L, int R) {
    // pruning
    // base case: single element doesn't require any cost to merge 
    if(L == R) {
        return 0;
    }
    
    // cache check 
    if(dp[L][R] != -1) {
        return dp[L][R];
    }
    
    // transition
    int ans = 1e9;
    int tot_sum = 0;
    int left_sum = 0;
    for(int i=L; i<=R; i++) tot_sum += A[i];
    for(int mid=L; mid<R; mid++) {    // mid!=R bcoz mid+1...R needs to be valid substring
        left_sum += A[mid];
        int merge_cost = ((left_sum % 100) * ((tot_sum - left_sum) % 100));
        ans = min(ans, rec(L, mid) + rec(mid+1, R) + merge_cost);
    }
    
    // save and return
    return (dp[L][R] = ans);
}

void solve() {
    cin >> n;
    for(int i=1; i<=n; i++) cin >> A[i];
    memset(dp, -1, sizeof(dp));
    
    // Recurrence Meaning:
    // rec(L, R): Minimum cost to merge elements [L...R]
    cout << rec(1, n) << '\n';
}

signed main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    
    solve();
    return 0;
}
```
TC : $O(N^3)$

**NOTE**
This is a well-known approach in LR DP, and it follows these key steps:

1. **Fixed End Value for Ranges**: For any subarray, the final merged value is always fixed, based on the sum of the subarray modulo 100.
    
2. **Last Merge Creation**: The last merge in a subarray results from merging two elements, one from each of the two smaller subarrays. These elements combine to form the final value of the subarray.
    
3. **Value Determination**: If we know the midpoint of the subarray, we can compute the values of the two elements that were merged to form the final value. Specifically, we can find the values of $X$ and $Y$, the last two merged elements, and compute their product $X \times Y$, which contributes to the total merge cost.
    
4. **Recursive Calculation**: The DP transition is designed to calculate the minimum merge cost for a range `[L...R]`. To do this, we recursively calculate the best cost to merge subarrays `[L,mid]` and `[mid+1,R]`, and combine these results to find the minimum cost for the entire range. This recursive approach ensures that we consider all possible ways to split and merge the subarrays for the optimal solution.

*Follow up Problem* : How to find mergings that happened ?
To find the merge steps, store the optimal midmidmid for each subarray during the DP calculation. After the table is filled, backtrack from the final result using the stored midmidmid values to reconstruct the merge sequence.