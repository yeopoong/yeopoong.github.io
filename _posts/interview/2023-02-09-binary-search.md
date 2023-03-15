---
layout: post
published: false
title: "Binary Search"
categories: interview
tags: interview binary-search
---

## Binary Search

T: O(log n)
Every time you see a problem that involves a sorted array, you should consider binary search.

```java
public int search(int[] nums, int target) {
    int pivot;
    int left = 0, right = nums.length - 1;
    
    // 원소가 홀수 일 경우 때문에 = 조건이 포함되야 한다.
    while (left <= right) {
        pivot = left + (right - left) / 2;
        if (target < nums[pivot]) right = pivot - 1;
        else if (target > nums[pivot]) left = pivot + 1;
        else return pivot; 
    }
    
    return -1;
}
```

[Easy]
- [704. Binary Search](https://leetcode.com/problems/binary-search/)
- [060. Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/)

[Medium]
- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)