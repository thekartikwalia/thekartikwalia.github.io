---
title: Binary Search Fundamentals
date: 2024-10-09 8:00:00 +0530
categories: [DSA, Binary Search]
tags: [binary search, lower bound, search space, template]
math: true
mermaid: true
pin: false
---

## Binary Search in Action
__Binary search__ is a powerful algorithm used to efficiently locate a specific value within a sorted collection of data. This search technique significantly reduces the number of comparisons needed compared to linear search, making it particularly useful for large datasets. Let's delve into binary search through a real-life example and explore a simple implementation in C++.

__Real-Life Example: Phone Book__
Imagine you have a phone book sorted alphabetically by last name. If you were searching for a person named "John Doe," a binary search would allow you to quickly pinpoint the correct entry. Here's how it works:
1. Start in the middle of the phone book.
2. Compare the last name of the person in the middle with "Doe."
3. If the last name matches, you've found the entry. If "Doe" comes before the middle entry alphabetically, repeat the process in the left half; otherwise, search the right half.
4. Continue narrowing down the search until you find "John Doe" or determine that he's not in the phone book.

## Frameworks and Forms in Binary Search
We will study several frameworks and forms in Binary Search.

![FrameworkAndFormsBS.png](/assets/img/dsa/FrameworkAndFormsBS.png)

Before delving into the intricacies of binary search, it's crucial to grasp three fundamental terms used in our Binary Search Template. These terms lay the groundwork for a clearer understanding of the algorithm:
1. __Search Space__ : The search space represents the realm of potential answers to the problem at hand. Denoted by [l, h], where 'l' signifies the low index, and 'h' signifies the high index. The search space progressively narrows down through iterations, leading to the identification of the desired solution.
2. __Mid index__ : In each iteration, the algorithm calculates the mid index of the current search space. The formula employed is `mid = l + (h - l) / 2`. This formula is preferred over the direct use of `mid = (l + h) / 2` to mitigate the risk of integer overflow. The mid index serves as a pivotal point, guiding the search towards the optimal solution.
3. __ans__ : The 'ans' variable plays a crucial role in storing the best answer obtained thus far during the binary search process. As the algorithm progresses, 'ans' captures and retains the most viable solution, ensuring that the final outcome is both accurate and efficient. Initially, the value can vary problem to problem but generally is -1, meaning no answer found yet.

## Example-1 : The Fundamental Problem
You are given an array of size n containing {0,1} where elements are in non-decreasing order. Implement a C++ program to find the index of the first occurrence of the value '1' in the array.

__Test Case__ :
```cpp
n = 9
arr = [0, 0, 1, 1, 1, 1, 1, 1, 1]
```

1. __Initial Values__
	- `l` is the starting index of the array, initially set to 0.
	- `h` is the ending index of the array, initially set to n - 1 (where n is the size of the array).
	- `ans` is initialized to -1.
2. __Iteration 1__
	- `mid` is calculated as the middle index between l and h.
	- `arr[mid]` is checked. If it's equal to 1, we update ans to the current mid and move the search to the left half by setting `h = mid - 1`. If it's not equal to 1, we move to the right half by setting `l = mid + 1`. Remember, we will exclude the mid from our search space because we already checked whether it's a better answer or not.
3. __Iteration 2__
	- The search space is narrowed down based on the result from Iteration 1.
	- The process repeats until `l` becomes greater than `h`, indicating the end of the search.
4. __Final Result__
	- The value of `ans` represents the index of the first occurrence of '1' in the array.

__Code__ :
```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
int arr[100100];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    int lo = 0, hi = n - 1, ans = -1;

    while (lo <= hi) {
        int mid = lo + ((hi - lo) / 2);    // lo + ((hi - lo) >> 1)

        if (arr[mid] == 1) {
            ans = mid;
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }

    cout << "Final result: " << ans << endl;
    return 0;
}
```
Time complexity is O(log N), where N is the size of the array. This is because in each iteration, the search space is effectively halved.

Now, we keep the template the same, just add a check function and manipulate it for a given problem and try to convert it into the above solved fundamental problem.

__NOTE__ : In case of all 0's the default value of `ans` is returned.

## Example-2 : Implementing Lower Bound
We know the lower bound of x, which means finding the first index such that the element at that index is `>= x`.

__Test Case__ :
```cpp
arr = [1, 5, 6, 8, 8, 10, 11, 11, 12] and x = 11
```
Here, the value at index 6 is the first element greater than or equal to x (11). Prior to that index, all elements are smaller; hence, they are assigned the value 0. After that index, all elements are greater than or equal to x, so they are assigned the value 1. Now, the task is to find the first index containing the element 1.

__Note__ : We do not convert it into a 0-1 array; we simply assume that this assignment is taking place.

__Code__ :
```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
int arr[100100];
int x;

int check(int mid) {
    return (arr[mid] >= x);
}

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    int lo = 0, hi = n - 1, ans = -1;
    while (lo <= hi) {
        int mid = lo + ((hi - lo) >> 1); 
        if (check(mid)) {
            ans = mid;
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }

    cout << ans << endl;
}
```

Here also, the time complexity is O(log N), where N is the size of the array. This is because in each iteration, the search space is effectively halved. check() function just taking O(1).

__Explanation__ :
- The `check` function takes an index `mid` as an argument.
- It compares the element at index `mid` in the array (`arr[mid]`) with the target value `x`.
- If `arr[mid]` is greater than or equal to `x`, the function returns 1, indicating that the current middle element is a potential candidate for the lower bound.
- If `arr[mid]` is less than `x`, the function returns 0, indicating that the lower bound must be in the right half of the current search interval.

__Similarly, we manipulate the check function and convert the problems into a 0-1 array problem.__

![BS Magic.jpeg](/assets/img/dsa/BS%20Magic.jpeg)