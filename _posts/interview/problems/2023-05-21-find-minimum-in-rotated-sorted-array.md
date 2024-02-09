---
layout: post
published: true
title: "153. Find Minimum in Rotated Sorted Array"
categories: interview
tags: medium array binary-search
---

> 고유 요소의 정렬된 회전 배열이 주어지면 이 배열의 최소 요소를 반환

[153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

```java
class Solution {
    
    // 정렬된 회전 배열에서 최소 요소 찾기: Binary Search
    // O(log n)
    public int findMin(int[] nums) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            // 증가구간(오른쪽 값이 크면): 최소값은 왼쪽에 있다.
            if (nums[mid] < nums[right]) {
                right = mid;
            // 감소구간(오른쪽 값이 작으면): 최소값은 오른쪽에 있다.
            } else {
                left = mid + 1;
            }
        }
        
        return nums[right];
    }
}
```