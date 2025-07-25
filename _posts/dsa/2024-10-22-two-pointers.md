---
title: Two Pointers
date: 2024-10-22 8:55:00 +0530
categories: [DSA, Two Pointers]
tags: [two pointers, subarrays, sliding window, greedy, optimization]
math: true
mermaid: true
pin: false
---

## Two Pointers 
__Two pointers technique__ is a powerful approach used to solve problems that involve searching, sorting, or traversing sequences, typically arrays or lists.

The idea is to maintain two indices (or "pointers") that move through the array or sequence from either the same or different directions, depending on the nature of the problem. This method helps in reducing the time complexity of an algorithm by eliminating nested loops or redundant comparisons.

Most of the problems of [Binary Search Fundamentals]({% post_url 2024-10-09-binary-search-fundamentals %}) on every Start can be optimised using two pointers.

## Frameworks and Forms in Two Pointers 
![FrameworksandFormsTwoPointers.jpeg](/assets/img/dsa/FrameworksandFormsTwoPointers.jpeg)
1. __Opposite Ends__  
   One pointer starts from the beginning, and the other starts from the end. The pointers move towards each other, often meeting in the middle.
   These mainly involves classical problems, which you should know before hand.
   _Example_ : Finding pairs in a sorted array that sum to a given target.
2. __[Two Pointers (Same Direction)]({% post_url 2024-10-23-two-pointers-same-direction %})__ 
   Both pointers start from the beginning and move forward at different speeds.
   You try to maintain some sort of window over here.
   _Example_ : Sliding window problems or finding the longest subarray that satisfies certain conditions.

