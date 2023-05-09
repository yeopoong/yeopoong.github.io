---
layout: post
published: true
title: "31. Next Permutation"
categories: interview
tags: problems array two-pointers
---

> 정수 nums의 배열이 주어지면 nums의 다음 순열을 찾습니다.

- [31. Next Permutation](https://leetcode.com/problems/next-permutation/)


```java
 class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        
        for (int i = 0; i < nums.length; i++) {
            res[i] = -1;
            for (int j = 1; j < nums.length; j++) {
                if (nums[(i + j) % nums.length] > nums[i]) {
                    res[i] = nums[(i + j) % nums.length];
                    break;
                }
            }
        }
        
        return res;
    }
}
```
