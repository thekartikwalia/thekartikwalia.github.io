---
layout: post
title: "Priority Queue"
date: 2024-10-07
categories: [DSA, STL]
math: true
tags: [STL, C++, priority_queue]
---

## Priority Queue
priority_queue is an implementation of a priority queue, which is a data structure that stores elements in a way such that the element with the highest priority is served before other elements with lower priority. 
It is implemented as a heap and is part of the queue container adapters in the STL.

__Real-life Example__
Consider a scenario where tasks are assigned to a group of workers, and each task has a priority associated with it. A priority_queue would be a suitable choice for managing these tasks because:
- _Priority Handling_: The priority queue ensures that the task with the highest priority is processed first, simulating the real-world scenario where higher-priority tasks should be addressed before lower-priority ones.
- _Efficient Access_: The highest-priority task can be accessed efficiently, making it suitable for scenarios where quick access to the most critical element is crucial.

__Example Code__
```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int main() {
    // Declaration and Initialization
    // Time Complexity: O(n log n) for initialization (where n is the number of elements)
    vector<int> initList = {3, 1, 4, 1, 5, 9, 2, 6};
    priority_queue<int> taskPriorityQueue(initList.begin(), initList.end());

    // Adding a task
    // Time Complexity: O(log n) for push (assuming a binary heap)
    taskPriorityQueue.push(7);

    // Accessing the highest-priority task
    // Time Complexity: O(1) for top (since the highest-priority element is always at the top)
    int highestPriority = taskPriorityQueue.top();
    cout << "Highest Priority Task: " << highestPriority << endl;

    // Processing the highest-priority task
    // Time Complexity: O(log n) for pop (assuming a binary heap)
    taskPriorityQueue.pop();

    // Displaying the remaining tasks
    cout << "Remaining Tasks: ";
    
    // Looping through the priority queue
    while (!taskPriorityQueue.empty())
    {
        // Accessing the highest-priority element
        // Time Complexity: O(1) for top (since the highest-priority element is always at the top)
        cout << taskPriorityQueue.top() << " ";
        
        // Removing the highest-priority element
        // Time Complexity: O(log n) for pop (assuming a binary heap)
        taskPriorityQueue.pop();
    }

    cout << endl;

    return 0;
}
```

## Key Characteristics of Priority Queue
-  __Element Access Based on Priority__: In a priority queue, elements are served based on their priority. By default, the largest element (according to the `<` operator) is considered to have the highest priority. This behavior can be modified using custom comparators.
- __Heap-Based Implementation__: Internally, the priority queue is implemented as a binary heap (max-heap by default), which ensures efficient insertion and deletion of elements while maintaining the priority order.
- __Efficient Operations__: The priority queue supports efficient insertion (`push`), retrieval of the highest-priority element (`top`), and removal of the highest-priority element (`pop`) with logarithmic time complexity (`O(log n)`) except `top`.
- __Non-Sequential Access__: Unlike regular queues or vectors, a priority queue does not allow random or sequential access to its elements. It only allows access to the top element (highest priority) at any given time.
- __Comparator Customization__: You can provide a custom comparator (for example, to create a min-heap instead of a max-heap) when initializing a priority queue.

## Important Modifiers of Containers Priority Queue
- `empty()`: Time Complexity - O(1), constant time. Indicates whether the priority queue is devoid of elements.
- `size()`: Time Complexity - O(1), constant time. Provides the count of elements present in the priority queue.
- `top()`: Time Complexity - O(1), constant time. Retrieves a reference to the highest-priority element in the queue.
- `push(g)`: Time Complexity - O(log n), where n is the number of elements in the priority queue. Appends the element 'g' to the end of the priority queue and adjusts the heap to maintain its structure.
- `pop()`: Time Complexity - O(log n), where n is the number of elements in the priority queue. Removes the foremost element from the priority queue and adjusts the heap.
- `emplace()`: Time Complexity - O(log n), where n is the number of elements in the priority queue. Inserts a new element into the priority queue, maintaining the order based on priority and adjusting the heap.

## Underlying Container of Priority Queue
The priority queue in the C++ Standard Template Library (STL) uses one of the following containers as its underlying structure:
1. `vector`: By default, `priority_queue` uses `vector` as its underlying container, which provides efficient dynamic resizing and supports the heap operations required for the priority queue.
2. `deque`: While `vector` is the default container, the priority queue can also be implemented using `deque` (double-ended queue). However, this is not typical because `vector` provides better cache locality.
3. `less<T>`: By default, the comparator used for prioritising elements is `less<T>`, which creates a max-heap. You can customise this to use `greater<T>` to create a min-heap or any other custom comparator.

## Applications of Priority Queue
1. __Task Scheduling__: Priority queues are widely used in operating systems for managing tasks with different priorities. The task with the highest priority is always processed first (e.g., job scheduling in CPU task management).
2. __Graph Algorithms__: Priority queues are essential in algorithms like Dijkstra's shortest path and Prim's Minimum Spanning Tree, where nodes with the lowest cost or priority are processed first.
3. __Event Simulation Systems__: In event-driven simulations, future events are processed based on their time of occurrence. Priority queues help in efficiently scheduling and executing events in the correct order.
4. __Real-Time Processing__: In systems requiring real-time data processing (e.g., network routers or firewalls), priority queues help prioritise packets or requests, ensuring timely responses.
5. __Huffman Coding__: The priority queue is crucial in Huffman coding (a compression algorithm) where characters are assigned variable-length codes based on their frequencies. The least frequent characters have higher priorities during the tree construction phase.