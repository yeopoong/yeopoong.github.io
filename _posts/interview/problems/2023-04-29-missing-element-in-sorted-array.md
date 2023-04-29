---
layout: post
published: true
title: "1060. Missing Element in Sorted Array"
categories: interview
tags: problems array binary-search
---

> 오름차순으로 정렬된 정수 배열 nums 가 주어지면 배열의 가장 왼쪽 숫자부터 시작하여 k번째 누락된 숫자를 반환  

- [1060. Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/)

 ```java
class Solution {
    // 배열의 가장 왼쪽 숫자부터 시작하여 k번째 누락된 숫자를 반환
    // O(n)
    public int missingElement(int[] nums, int k) {
        for (int i = 1; i < nums.length; i++) {
            // 두 요소간의 갭: 존재하는 숫자의 개수
            int gap = nums[i] - nums[i-1] - 1;
            if (gap < k) {
                k -= gap;
            } else {
                return nums[i-1] + k;
            }
        }
        
        // 마지막까지 찾지 못한 경우
        return nums[nums.length-1] + k;
    }
}
```