---
layout: post
published: false
title: "70. Climbing Stairs"
categories: interview
tags: interview tree bfs
---

- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

```java
class Solution {
    // f(x) = f(k-2) + f(k-1): 1, 1, 2, 3, 5, 8, ...
    // a, b = b, a + b
    // DFS: Decision Tree: O(2^n)
    // DP: Memoization, Bottom-up: O(n)
    // Brute Force: O(2^n), O(n)
    public int climbStairs(int n) {
        int a = 1, b = 1;
        int t;
        
        for (int i = 0; i < n - 1; i++) {
            t = a + b;
            a = b;
            b = t;
        }
        
        return b;
    }
}
```