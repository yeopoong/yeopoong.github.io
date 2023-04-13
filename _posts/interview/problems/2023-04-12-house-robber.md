---
layout: post
published: true
title: "198. House Robber"
categories: interview
tags: problems array dynamic-programming
---

> 각 주택의 금액을 나타내는 정수 배열 nums가 주어지면, 경찰에 알리지 않고 오늘 밤 훔칠 수 있는 최대 금액을 반환

- [198. House Robber](https://leetcode.com/problems/house-robber)

```java
class Solution {
    // Dynamic Programming
    public int rob(int[] nums) {
        int a = 0, b = 0;
        int t;
        
        // recurrence relation(점화식): f(k) = max(f(k-2) + num(k), f(k-1))
        // a, b = b, max(a + i, b)
        // 점화식을 가지고 값을 치환하면서 최종 결과까지의 값을 구해 나간다. 
        for (int i : nums) {
            // (현재값 + 전전값) 과 이전값 중에서 더 큰값이 최대값
            t = Math.max(a + i, b);
            a = b;
            b = t;
            /*
            t = a;
            a = b;
            b = Math.max(i + t, b);
            */
        }
        
        return b;
    }
}
```