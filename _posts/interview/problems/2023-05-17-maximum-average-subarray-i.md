---
layout: post
published: true
title: "643. Maximum Average Subarray I"
categories: interview
tags: problems array two-pointers
---

> 길이가 k와 같고 평균값이 최대인 연속된 하위 배열을 찾아 이 값을 반환

- [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)

```java
class Solution {
    
    // 최대 평균 하위 배열
    // T: O(n)
    public double findMaxAverage(int[] nums, int k) {
        double sum = 0;
        
        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }
        
        double res = sum;
        
        for (int i = k; i < nums.length; i++) {
            sum += nums[i] - nums[i-k];
            res = Math.max(res, sum);
        }
        
        return res / k;
    }
}
```