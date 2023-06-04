---
layout: post
published: true
title: "189. Rotate Array"
categories: interview
tags: array
---

> 정수 배열 nums가 주어지면 배열을 k 단계만큼 오른쪽으로 회전

- [189. Rotate Array](https://leetcode.com/problems/rotate-array/)

```java
class Solution {
    // 전체를 뒤집고, 경계 앞뒤로 각각 뒤집는다.
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        
        /*
        Original List                   : 1 2 3 4 5 6 7
        After reversing all numbers     : 7 6 5 4 3 2 1
        After reversing first k numbers : 5 6 7 4 3 2 1
        After revering last n-k numbers : 5 6 7 1 2 3 4 --> Result
        */
        reverse(nums, 0, n - 1); // 전체
        reverse(nums, 0, k - 1); // 앞쪽
        reverse(nums, k, n - 1); // 뒤쪽
    }

    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```
