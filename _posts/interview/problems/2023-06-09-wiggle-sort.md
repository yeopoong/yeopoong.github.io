---
layout: post
published: true
title: "280. Wiggle Sort"
categories: interview
tags: array sort
---

> 정수 배열 nums가 주어지면 nums[0] <= nums[1] >= nums[2] <= nums[3]....이 되도록 재정렬

[280. Wiggle Sort](https://leetcode.com/problems/wiggle-sort/)

```java
class Solution {

    // T: O(nlog(n))
    public void wiggleSort(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length - 1; i += 2) {
            swap(nums, i, i + 1);
        }
    }
        
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
