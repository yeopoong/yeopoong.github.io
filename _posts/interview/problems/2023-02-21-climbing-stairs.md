---
layout: post
published: true
title: "70. Climbing Stairs"
categories: interview
tags: dynamic-programming memoization
---

> 당신은 계단을 오르고 있습니다. 정상에 도달하려면 n걸음이 걸립니다.  
> 매번 1단계 또는 2단계를 오를 수 있습니다. 얼마나 많은 독특한 방법으로 정상에 오를 수 있습니까?  

- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

```java
class Solution {
    // f(x) = f(k-2) + f(k-1): 1, 1, 2, 3, 5, 8, ...
    // a, b = b, a + b
    // 얼마나 많은 독특한 방법으로 정상에 오를 수 있습니까?
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