---
layout: post
published: true
title: "213. House Robber II"
categories: interview
tags: medium dynamic-programming
---

> 각 주택의 금액을 나타내는 정수 배열 nums가 주어지면, 경찰에 알리지 않고 오늘 밤 훔칠 수 있는 최대 금액을 반환

[213. House Robber II](https://leetcode.com/problems/house-robber-ii/)

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        
        // 1,2,3,1 : 1,2,3 / 2,3,1
        // 시작과 끝자리를 동시에 선택할 수 없다.
        return Math.max(rob(nums, 0, nums.length - 2), rob(nums, 1, nums.length - 1));
    }
    
    private int rob(int[] nums, int lo, int hi) {
        int a = 0, b = 0;
        int t;
        
        // 점화식(recurrence relation): f(k) = max(f(k-2) + num(k), f(k-1))
        // a, b = b, max(i + a, b)
        for (int i = lo; i <= hi; i++) {
            t = Math.max(a + nums[i], b);
            a = b;
            b = t; 
        }
        
        return b;
    }
}
```
