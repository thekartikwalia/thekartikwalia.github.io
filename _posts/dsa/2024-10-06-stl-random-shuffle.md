---
title: "random_shuffle() and shuffle()"
date: 2024-10-06 10:40:00 +0530
categories: [DSA]
tags: [cpp, stl, algorithms, randomness, shuffle]
math: true
---

## random_shuffle()
The `random_shuffle()` function in C++ was used to randomly rearrange the elements in a given range,, producing a random permutation of the elements. It was part of the `<algorithm>` header in the C++ Standard Library.

__Function Prototype__
```cpp
void random_shuffle(RandomIt first, RandomIt last);
void random_shuffle(RandomIt first, RandomIt last, RandomFunc rand);
```
- _first_ : Iterator pointing to the beginning of the range 
- _last_ : Iterator pointing to the end of the range (the position one past the last element)
- _rand_ (optional) : A function or callable object that provides random values

`random_shuffle` rearranged the elements randomly using an internal random number generator unless a custom generator was provided.

__Example__
```cpp
#include <algorithm>

int main() {
	vector<int> v = {1, 2, 3, 4, 5};

	// Shuffle the vector using random_shuffle (deprecated in C++17)
	random_shuffle(v.begin(), v.end());

	return 0;
}
```

__NOTE__
However, it's important to note that `random_shuffle` was deprecated in C++14 and removed in C++17. In modern C++ (C++11 and later), the preferred function is `shuffle`, which is more flexible and requires an explicit random number generator.

## Why `random_shuffle` was Deprecated and Removed ?
- `random_shuffle` used the `rand()` function internally, which was not a high-quality random number generator
- `rand()` has poor randomness and was implementation-dependent, which made it unsuitable for many modern applications that require good randomisation

## Modern Replacement : `shuffle()`
Instead of `random_shuffle`, you should use `shuffle`, which allows for better control over the randomness by requiring an explicit random number generator (like one from the `<random>` library).

__Function Prototype__
```cpp
template<class RandomIt, class URBG>
void shuffle(RandomIt first, RandomIt last, URBG&& g);
```
- _URBG_ : Uniform Random Bit Generator (e.g., `default_random_engine`, `mt19937`)

__Example__
```cpp
#include <random>
#include <algorithm>

int main() {
	vector<int> v = {1, 2, 3, 4, 5};

	// Initialise random number generator 
	random_device rd;
	mt19937 g(rd());

	// Shuffle the vector using shuffle (modern C++)
	shuffle(v.begin(), v.end(), g)

	return 0;
}
```

## Key Differences between `random_shuffle` and `shuffle`
- `shuffle` requires an explicit random number generator, making it more flexible and reliable for good randomness
- `random_shuffle` was tied to the poor-quality `rand()` function, which led to it's deprecation and removal