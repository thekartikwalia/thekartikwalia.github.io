---
title: "next_permutation()"
date: 2024-10-06 10:45:00 +0530
categories: [DSA, STL]
tags: [cpp, stl, algorithms, permutations, leetcode]
math: true
---

## next_permutation()
In C++ STL, `next_permutation()` is a function that rearranges the elements in a range to the __next lexicographical permutation___ (or order) of those elements. If the current arrangement is the largest possible permutation, it rearranges the elements to the __smallest permutation__ (sorted in ascending order).

__Function Prototype__
```cpp
bool next_permutation(BidirectionalIt first, BidirectionalIt last);
```
- _first_ : Iterator pointing to the first element of the range 
- _last_ : Iterator pointing to one past the last element of the range 

__Return value__
- Returns `true` if the function was able to rearrange the elements into the next permutation 
- Returns `false` if the function could not find a next permutation (i.e., if the current arrangement is the largest permutation possible)

__NOTE__ : There exists 1 more similar STL algorithm, `prev_permutation()`

## Key Points about `next_permutation()`
1. __Lexicographical Order__ : The function generates permutations in lexicographical (dictionary) order
2. __Efficient Generation__ : It efficiently generates the next permutation without generating all permutations at once, making it useful for algorithms requiring incremental permutations
3. __Sorting__ : If the range is sorted in descending order (the largest lexicographical permutation), `next_permutation()` will sort the range in ascending order, returning `false`

## Examples 
__`next_permutation()` with Strings__
```cpp
#include <algorithm>
#include <string>
using namespace std;

int main() {
    string s = "abc";

    do {
        cout << s << endl;
    } while (next_permutation(s.begin(), s.end()));

    return 0;
}
```
Output 
```cpp
abc
acb
bac
bca
cab
cba
```
After the last permutation (`cba`), the function returns `false` because there are no more possible permutations.

---
__Sorting (Largest Permutation)__
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3}; // Starting with the smallest permutation
    
    // Print all permutations until reaching the largest
    do {
        for (int x : v) {
            cout << x << " ";
        }
        cout << endl;
    } while (next_permutation(v.begin(), v.end()));
    
    // At the end of loop, next_permutation got called on {3, 2, 1}
    cout << "After reaching largest permutation: ";
    for (int x : v) {
        cout << x << " ";
    }
    cout << endl;
    
    return 0;
}
```
Output
```cpp
1 2 3 
1 3 2 
2 1 3 
2 3 1 
3 1 2 
3 2 1 
After reaching largest permutation: 1 2 3 
```
The `do-while` loop executes once before checking the condition. This means that if the last permutation is printed, the vector will be rearranged to the smallest permutation on the next call of `next_permutation()` inside the loop, leading to `123`, and then `132`.

## Practical Applications
1. __Generating Permutations__ : `next_permutation()` is widely used when you need to generate permutations in lexicographical order
2. __Solving Puzzles/Problems__ : It can be used to solve combinatorial problems that require exploring all possible orders of elements
3. __Brute Force Solution__ : Useful in brute force algorithms that need to try all possible arrangements of elements, such as solving permutation-based puzzles or optimisation problems

## Self Implementation of `next_permutation()`
__Problem Link__ : [31. Next Permutation](https://leetcode.com/problems/next-permutation/description/)

---
__Approach-1__
Generate all possible permutations using Recursion, then sort them in increasing order & return the next index
```cpp
class Solution {
public:
    void generatePermutations(vector<int> &nums, vector<vector<int>> &permutations, int ind) {
        if(ind == nums.size()) {
            permutations.push_back(nums);
            return;
        }

        for(int i=ind; i<nums.size(); i++) {

            // Avoid duplicate permutations when elements repeats 
            // For better understanding, dry run {1, 1, 2, 3}
            if(i == ind || (i != ind && nums[ind] != nums[i])) {
                swap(nums[ind], nums[i]);
                generatePermutations(nums, permutations, ind+1);
                swap(nums[ind], nums[i]);
            }
        }
    }

    void nextPermutation(vector<int>& nums) {
        vector<vector<int>> permutations;

        // Generate all permutations in sorted order
        generatePermutations(nums, permutations, 0);
        sort(permutations.begin(), permutations.end());

        for(auto it:permutations) {
            for(auto p:it) cout << p << " ";
            cout << endl;
        }

        // Linear Search to find where does 'nums' lie
        int n = permutations.size(), ind;
        for(int i=0; i<n; i++) {
            if(permutations[i] == nums) {
                ind = i;
                break;
            }
        }

        // Next index permutation will be answer
        // If next index doesn't exist, then 1st will be answer
        nums = permutations[(ind+1) % permutations.size()];
    }
};
```
TC : $O(n!) + O(n! * \log(n!)) + O(n!)$
SC : $O(n! * n)$

---
__Approach-2__
Observations,
1. Next elements of a dictionary tend to have longer prefix match

Algorithm
1. Try getting longest prefix match possible, by finding the break point (increasing 0 to i+1 & decreasing from i+1 to n-1)
2. Once you figure out break point, after the longest prefix try putting someone at i who is slightly greater than current guy 
3. Fill the remaining portion i+1 to n-1 as small as possible, by filling in sorted order
   Eg : {2, 1, 5, 4, 3, 0, 0}
      `i` will be pointing to value 5
      {2, 3, _, _, _, _, _}
      {2, 3, 0, 0, 1, 4, 5}

4. {1, 2, 3, 4, 5} dip right before the last element, so we know dip highest could be found at (n-2)th index
5. {5, 4, 3, 2, 1} whole decreasing, so no dip (as it's the last permutation)

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();

        // Find the dipIndex
        int dipIndex = -1;
        for(int i=n-2; i>=0; i--) {
            if(nums[i] < nums[i+1]) {
                dipIndex = i;
                break;
            }
        }

        // If there's no dip, then it would be lexicographically the biggest permutation, so return smallest one
        if(dipIndex == -1) {
            reverse(nums.begin(), nums.end());
            return;
        }

        // Find someone ahead which is slightly greater than element at dipIndex 
        // Since right portion is decreasing & we need smallest, so start traversing from back
        for(int i=n-1; i>=0; i--) {
            if(nums[i] > nums[dipIndex]) {
                swap(nums[i], nums[dipIndex]);    // Swapping let's [i+1 ... n-1] stay in decreasing order 
                break;
            }
        }

        // Fill the remaining portion as small as possible, by filling it in sorted order 
        // Since that part is decreasing, so we just reverse it
        reverse(nums.begin() + dipIndex+1, nums.end());
    }
};
```
TC : $O(N)$
SC : $O(1)$    $\,\,\,\,(\text{Modifying the given array})$