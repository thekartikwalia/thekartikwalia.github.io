---
title: "2D Prefix Sums"
date: 2024-10-18 10:00:00 +0530
categories: [DSA]
tags: [prefix-sum, 2d-arrays, range-query, cpp]
math: true
---

## 2D Prefix Sum 
__2D Prefix sum__ is a technique used to efficiently calculate the sum of elements in a given range of a 2D array. The idea is to precompute and store cumulative sums up to each element in the array. This precomputation allows us to answer range sum queries in constant time.

## Algorithm 
1. __Initialization__
    - Start with a 2D array `Arr` of size `n x m`.
    - Create an auxiliary 2D array `P` of the same size to store the prefix sum.
2. __Compute Prefix Sum__
   
   ![2D Prefix Sum Build.jpeg](/assets/img/dsa/2d-prefix-sum-build.jpeg)
   
    - For each element `Arr[i][j]`, compute the sum of all elements in the rectangle from `(0, 0)` to `(i, j)`. This sum is stored in `P[i][j]`.
    - The Prefix Sum is build in Row-major order (i.e. firstly row is iterated, then column).
    - The formula for computing the prefix sum is :
      ```cpp
	  P[i][j] = Arr[i][j] + P[i-1][j] + P[i][j-1] - P[i-1][j-1]
		```
      where `P[i][j]` is the prefix sum up to element `Arr[i][j]`.
3. __Answering Queries__
   
   ![2D Prefix Sum Calculation.jpeg](/assets/img/dsa/2d-prefix-sum-calculation.jpeg)
   
   To find the sum of values in a rectangle defined by `(U, L)` (Top Left Corner) and `(D, R)` (Bottom Right Corner), use the formula :
	```cpp
	Sum = P[D][R] - P[D][L-1] - P[U-1][R] + P[U-1][L-1]
	```
	This formula takes advantage of the precomputed prefix sums to answer queries in constant time.

## Problem - 1 : 2D Range Sum Query
You are given a 2D matrix `Arr` of dimensions `n x m`, where each cell contains a numerical value. The objective is to efficiently answer a series of queries related to the sum of values within specified rectangles.

__Queries__
There are Q queries of the form `?LRUD`, where each query is defined by four parameters :
- `L` (Left) : The leftmost column index.
- `R` (Right) : The rightmost column index.
- `U` (Up) : The topmost row index.
- `D` (Down) : The bottommost row index.

These parameters denote the corners of a rectangle within the matrix, with the top-left corner being `(U, L)` and the bottom-right corner being `(D, R)`.

__Objective__
For each query, calculate and output the sum of values within the specified rectangle, i.e., the sum of values for cells with indices `(i, j)` where `U <= i <= D` and `L <= j <= R`.

__Code__
```cpp
#include <iostream>
#include <vector>

using namespace std;

const int MAXN = 1000; // Assuming a maximum size for the 2D array

int Arr[MAXN][MAXN];
int P[MAXN][MAXN];

void computePrefixSum(int n, int m) {
    // Calculate the prefix sum using the given formula
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            P[i][j] = Arr[i][j];
            if (i > 0) P[i][j] += P[i - 1][j];
            if (j > 0) P[i][j] += P[i][j - 1];
            if (i > 0 && j > 0) P[i][j] -= P[i - 1][j - 1];
        }
    }
}

int queryRectangleSum(int U, int L, int D, int R) {
    // Calculate the sum of values in the specified rectangle
    int ans = P[D][R];
    if (L > 0) ans -= P[D][L - 1];
    if (U > 0) ans -= P[U - 1][R];
    if (U > 0 && L > 0) ans += P[U - 1][L - 1];
    return ans;
}

int main() {
    int n, m; // Dimensions of the 2D array
    cout << "Enter the number of rows and columns: ";
    cin >> n >> m;

    // Input the values in each cell of the 2D array
    cout << "Enter the values of the 2D array:" << endl;
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < m; ++j)
            cin >> Arr[i][j];

    // Compute the prefix sum
    computePrefixSum(n, m);

    int Q; // Number of queries
    cout << "Enter the number of queries: ";
    cin >> Q;

    // Process each query
    for (int q = 0; q < Q; ++q) {
        int U, L, D, R; // Coordinates of the rectangle
        cout << "Enter query " << q + 1 << " (U L D R): ";
        cin >> U >> L >> D >> R;

        // Get the sum of values in the specified rectangle
        int result = queryRectangleSum(U, L, D, R);
        cout << "Sum in the rectangle: " << result << endl;
    }

    return 0;
}
```
__Time Complexity__
- _Building 2D Prefix Sum Array_ : For each element in the (n*m) matrix, we perform constant time computations to build the prefix sum array. Hence, the overall time complexity for building the prefix sum array is $O(NM)$.
- _Answering Queries_ : Once the prefix sum array is built, answering each query requires constant time operations. Therefore, the time complexity for answering (Q) queries is $O(Q)$.

The overall time complexity for both building the prefix sum array and answering queries is $O(NM + Q)$, which is more accurate.