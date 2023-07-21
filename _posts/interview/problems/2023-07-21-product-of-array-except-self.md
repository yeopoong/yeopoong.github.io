---
layout: post
published: true
title: "238. Product of Array Except Self"
categories: interview
tags: medium prefix-sum
---

> 정수 배열 nums가 주어지면 answer[i]가 nums[i]를 제외한 nums의 모든 요소의 곱과 같은 배열을 반환

[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

```java
class Solution {
    // O(n)
    public int[] productExceptSelf(int[] nums) {
        int[] result = new int[nums.length];
        
        // Calculate lefts and store in result.
        int prefix = 1;
        for (int i = 0; i < nums.length; i++) {
            result[i] = prefix;
            prefix *= nums[i];
        }
        
        // Calculate rights and the product from the end of the array.
        int postfix = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            result[i] *= postfix;
            postfix *= nums[i];
        }
        
        return result;
    }
}
```