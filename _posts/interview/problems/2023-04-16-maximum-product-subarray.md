---
layout: post
published: true
title: "152. Maximum Product Subarray"
categories: interview
tags: maximum array dynamic-programming
---

> 가장 큰 곱을 갖는 하위 배열을 찾고 그 곱을 반환

- [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

```java
class Solution {
    
    // Brute Forse
    // T: O(n^2)
    public int maxProduct(int[] nums) {
        int res = nums[0];

        for (int i = 0; i < nums.length; i++) {
            int accu = 1;
            for (int j = i; j < nums.length; j++) {
                accu *= nums[j];
                res = Math.max(res, accu);
            }
        }
        
        return res;
    }
}
```

```java
class Solution {
    
    // Dynamic Programming
    // T: O(n)
    public int maxProduct(int[] nums) {
        int res = nums[0];

        int max = 1, min = 1;

        for (int n : nums) {
            int tmp = max * n;
            
            max = Math.max(n, Math.max(tmp, min * n));
            min = Math.min(n, Math.min(tmp, min * n));
            
            res = Math.max(res, max);
        }
        
        return res;
    }
}
```