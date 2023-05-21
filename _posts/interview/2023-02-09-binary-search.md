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
    int mid;
    
    int left = 0, right = nums.length - 1;
    
    // 원소가 홀수 일 경우 때문에 = 조건이 포함되야 한다.
    while (left <= right) {
        mid = left + (right - left) / 2;
        if (nums[mid] < target) left = mid + 1;
        else if (nums[mid] > target) right = mid - 1;
        else return mid;
    }
    
    return -1;
}
```

[Easy]
- [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)
- [704. Binary Search](https://leetcode.com/problems/binary-search/)
- [268. Missing Number](https://leetcode.com/problems/missing-number/)
- [1060. Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/)

[Medium]
- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)
- [153. Find Minimum in Rotated Sorted Array](problems/2023-05-21-find-minimum-in-rotated-sorted-array.md)
- [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)
- [1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/)
- [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
- [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)
