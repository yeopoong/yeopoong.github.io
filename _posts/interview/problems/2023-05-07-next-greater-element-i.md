---
layout: post
published: true
title: "496. Next Greater Element I"
categories: interview
tags: array stack
---

> ans[i]가 다음으로 큰 요소가 되도록 길이 nums1.length의 배열 ans를 반환

[496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

```java
class Solution {
    
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] res = new int[nums1.length];
        
        int counter = 0;
        
        for (int i: nums1) {
            res[counter++] = ans(i, nums2);
        }
        
        return res;
    }
    
    private int ans(int i, int[] nums) {
        for (int n = 0; n < nums.length; n++) {
            // 해당 숫자 찾기
            if (nums[n] == i) {
                // Find the next greater element
                for (int j = n + 1; j < nums.length; j++) {
                    if (nums[j] > i) return nums[j];
                }
            }
        }
        
        return -1;
    }
}
```
