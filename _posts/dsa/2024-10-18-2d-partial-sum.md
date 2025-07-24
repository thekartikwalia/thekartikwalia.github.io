---
title: "2D Partial Sums"
date: 2024-10-18 11:30:00 +0530
categories: [DSA]
tags: [partial-sum, 2d-arrays, range-update, cpp]
math: true
---

## 2D Partial Sum
__2D Partial sum__ involves calculating the sum of elements within a rectangular submatrix in a 2D matrix. It is useful in various applications including image processing, dynamic programming, and computational geometry.

## Example - 1 : Rectangle Sum Query
Given a 2D matrix `Arr[][]` initially filled with 0 in each cell.
There are Q queries of the form :
- `+ LRUD X`: Add X to the cell values in the rectangle formed by `U <= i <= D` and `L <= j <= R`.
- Here, i represents the index of the row and j represents the index of the column.

__Calculation for `+LRUDX`__

![2D Partial Sum.jpeg](/assets/img/dsa/2d-partial-sum.jpeg)
- For the query `+LRUDX`, the following adjustments are made to the prefix sum array :
    - `P[U][L] += X`
    - `P[U][R+1] -= X`
    - `P[D+1][L] -= X`
    - `P[D+1][R+1] += X`
- This operation is akin to the calculation of the final prefix sum as we do in 2D-prefix sum.


__Code__ 
```cpp
// Function to perform the query operation
void processQuery(int U, int D, int L, int R, int X) {
    Arr[U][L] += X;
    Arr[U][R+1] -= X;
    Arr[D+1][L] -= X;
    Arr[D+1][R+1] += X;
}

// After that we will do 2D prefix sum as we did earlier
```

__Time Complexity__
- The time complexity of the solution is $O(Q + NM)$ where Q is the number of queries and NM is the size of the 2D matrix.
- Each query operation takes constant time, and the final calculation of the prefix sum also takes linear time.
- This approach efficiently handles queries to update the values of cells within a specified rectangular region.