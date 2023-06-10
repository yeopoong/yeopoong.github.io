---
layout: post
published: true
title: "918. Maximum Sum Circular Subarray"
categories: interview
tags: array
---

> 길이가 n인 순환 정수 배열 nums가 주어지면 비어 있지 않은 nums 하위 배열의 가능한 최대 합계를 반환

[918. Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/)

```java
class Solution {
    
    // 최대 합계 원형 하위 배열
    public int maxSubarraySumCircular(int[] nums) {
        int totalSum = 0;
        int curSum1 = 0, curSum2 = 0;
        int maxSum = Integer.MIN_VALUE, minSum = Integer.MAX_VALUE;
        
        for (int a : nums) {
            totalSum += a;
            
            curSum1 += a;
            maxSum = Math.max(curSum1, maxSum);
            if (curSum1 < 0) curSum1 = 0;
            
            curSum2 += a;
            minSum = Math.min(curSum2, minSum);
            if (curSum2 > 0) curSum2 = 0;
        }
        
        if (maxSum < 0) return maxSum;
        
        return Math.max(maxSum, totalSum - minSum);
    }
}
```
