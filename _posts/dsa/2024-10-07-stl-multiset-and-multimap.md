---
layout: post
title: "Multiset and Multimap"
date: 2024-10-07
categories: [DSA, STL]
math: true
tags: [STL, C++, multiset, multimap]
---

## Multiset and Multimap
Multiset and Multimap are associative containers that are similar to set and map, respectively, but they allow duplicate keys. 
This means that multiple elements in these containers can have the same key.

__Real-life Example__
Consider a scenario where you need to store the ages of individuals, but some individuals might have the same age. A multiset or multimap would be suitable choices for these tasks because:
- _Duplicate Elements_: A multiset allows storing multiple occurrences of the same element (e.g., multiple individuals with the same age, meaning you can store the same age multiple times).
- _Duplicate Keys_: A multimap allows storing multiple key-value pairs with the same key (e.g., Multiple individuals associated with the same age, meaning you can store the same keys (age) with different values).
- _Efficient Storage_: These containers efficiently manage elements with the same key, making them useful in situations where duplicates are expected.

__Example Code__
```cpp
#include <iostream>
#include <set>
#include <map>
using namespace std;

int main() {
    // Example of multiset
    // Declaration and Initialization
    // Time Complexity: O(n log n) for initialization (where n is the number of elements in the initializer list)
    multiset<int> agesSet = {25, 30, 22, 25, 30};

    // Inserting an element
    // Time Complexity: O(log n) for insert (assuming balanced tree)
    agesSet.insert(25);

    // Count occurrences
    // Time Complexity: O(log n) for count (assuming balanced tree)
    int count = agesSet.count(25);
    cout << "Occurrences of age 25: " << count << endl;

    // Displaying the multiset
    // Time Complexity: O(n) for iterating through the multiset (where n is the number of elements)
    cout << "Ages Set: ";
    for (int age : agesSet) {
        cout << age << " ";
    }
    cout << endl;

    // Example of multimap
    // Declaration and Initialization
    // Time Complexity: O(n log n) for initialization (where n is the number of elements in the initializer list)
    multimap<string, int> agesMap = { {"Alice", 25}, {"Bob", 30}, {"Alice", 22}, {"Bob", 25} };

    // Inserting a key-value pair
    // Time Complexity: O(log n) for insert (assuming balanced tree)
    agesMap.insert(make_pair("Alice", 28));

	// Removing single (1st) occurrence of "Alice" from map
	auto it = agesMap.find("Alice");
	if(it != agesMap.end()) agesMap.erase(it);

	// Removing all occurrences of "Alice" from map
	agesMap.erase("Alice")

    // Displaying the multimap
    // Time Complexity: O(n) for iterating through the multimap (where n is the number of elements)
    cout << "Ages Map: ";
    for (auto it = agesMap.begin(); it != agesMap.end(); ++it)
    {
        cout << it->first << ": " << it->second << " | ";
    }
    cout << endl;

    return 0;
}
```

## Key Characteristics of Multiset and Multimap
1. __Multiset__
    - __Duplicates Allowed__: A multiset allows multiple occurrences of the same element (e.g., multiple values can be the same).
    - __Sorted Order__: Elements in a multiset are stored in a sorted order according to the specified comparator (default is less-than).
    - __No Key-Value Pairs__: A multiset only stores values and does not associate keys with those values.
    - __Dynamic Size__: The size of a multiset can grow or shrink as elements are added or removed.
2. __Multimap__
    - __Duplicate Keys Allowed__: A multimap allows multiple key-value pairs with the same key, meaning multiple values can be associated with a single key.
    - __Ordered by Key__: Elements in a multimap are sorted by keys, allowing for efficient retrieval based on the key.
    - __Key-Value Association__: Each element consists of a key and a value, providing a direct association between them.
    - __Dynamic Size__: Similar to multisets, multimaps can dynamically adjust their size.

## Important Modifiers of Containers Multiset and Multimap
1. __Multiset__
    - `insert()`: Adds an element to the multiset, allowing duplicate values.
    - `erase()`: Removes a single occurrence of an element from the multiset.
    - `clear()`: Removes all elements from the multiset.
    - `count()`: Returns the number of occurrences of a specific element in the multiset.
    - `find()`: Finds the first occurrence of an element in the multiset.
2. **Multimap**
    - `insert()`: Adds a new key-value pair to the multimap; duplicate keys are allowed.
    - `erase()`: Removes all occurrences of a specific key from the multimap.
    - `clear()`: Removes all key-value pairs from the multimap.
    - `equal_range()`: Returns a range of elements matching a specific key, allowing access to all values associated with that key.
    - `find()`: Finds the first occurrenc__of a specific key in the multimap.

## Underlying Container of Multiset and Multimap
__Multisets__ are typically implemented as **Red-Black Trees** (a type of balanced binary search tree), which ensures that insertion, deletion, and search operations have $O(\log n)$ time complexity.

Like multisets, __Multimaps__ are also implemented using **Red-Black Trees**, providing the same efficient performance characteristics for inserting, deleting, and finding key-value pairs.

## Applications of Multiset and Multimap
1. __Multiset Applications__
    - __Counting Frequencies__: Useful for counting occurrences of elements, such as word frequencies in a document.
    - __Data Analysis__: Used in statistical analysis to maintain a collection of values with their frequencies.
    - __Histogram Representation__: Multisets can efficiently represent histograms, where the values represent data points, and their counts represent frequency.
    - __Event Tracking__: Useful in applications that need to track events and their occurrences.
    - __Sorting with Duplicates__: Multisets can be used when you want to maintain a sorted list with duplicate values.
2. __Multimap Applications__
    - __Database Indexing__: Useful for indexing database entries where multiple values can be associated with the same key (like multiple phone numbers for a contact).
    - __Configuration Management__: Can store settings where keys may have multiple values (like environment variables).
    - __Event Handling Systems__: Can map events to multiple handlers, allowing one event to trigger multiple actions.
    - __Graph Representations__: Multimaps can represent graphs where keys are nodes, and values are edges connecting those nodes.
    - __Key-Value Store__: Useful for applications where multiple values need to be associated with a single key for quick retrieval.