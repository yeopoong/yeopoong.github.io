---
layout: post
published: false
title: "Binary Search"
categories: interview
tags: topics binary-search
---

## Approach

Every time you see a problem that involves a sorted array, you should consider binary search.
Time Complexity: O(log n)

```java
public int search(int[] nums, int target) {
    int mid;
    
    int left = 0, right = nums.length - 1;
    
    // 원소가 홀수일 경우 때문에 = 조건이 포함되야 한다.
    while (left <= right) {
        mid = left + (right - left) / 2;
        if (nums[mid] < target) left = mid + 1;       // 큰쪽에서 찾는다.
        else if (nums[mid] > target) right = mid - 1; // 작은데서 찾는다.
        else return mid;                              
    }
    
    return -1;
}
```

## Questions

[Easy]
- [35. Search Insert Position](/interview/2023/06/02/search-insert-position/)
- [69. Sqrt(x)](/interview/2023/05/23/sqrtx/)
- [268. Missing Number](/interview/2023/05/23/missing-number/)
- [278. First Bad Version](/interview/2023/06/21/first-bad-version/)
- [704. Binary Search](/interview/2023/05/23/binary-search/)
- [1060. Missing Element in Sorted Array](/interview/2023/05/23/missing-element-in-sorted-array/)
- [1539. Kth Missing Positive Number](/interview/2023/06/11/kth-missing-positive-number/)

[Medium]
- [33. Search in Rotated Sorted Array](/interview/2023/02/21/search-in-rotated-sorted-array/)
- [81. Search in Rotated Sorted Array II](/interview/2023/05/09/search-in-rotated-sorted-array-ii/)
- [153. Find Minimum in Rotated Sorted Array](/interview/2023/05/23/find-minimum-in-rotated-sorted-array)
- [162. Find Peak Element](/interview/2023/04/08/find-peak-element/)
- [378. Kth Smallest Element in a Sorted Matrix](/interview/2023/05/23/kth-smallest-element-in-a-sorted-matrix/)
- [528. Random Pick with Weight](/interview/2023/05/23/random-pick-with-weight/)
- [875. Koko Eating Bananas](/interview/2023/05/23/koko-eating-bananas/)
- [1182. Shortest Distance to Target Color](/interview/2023/05/27/shortest-distance-to-target-color/)
- [1901. Find a Peak Element II](/interview/2023/05/28/find-a-peak-element-ii/)