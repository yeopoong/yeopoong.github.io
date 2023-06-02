---
layout: post
published: true
title: "35. Search Insert Position"
categories: interview
tags: problems array binary-search
---

> 개별 정수의 정렬된 배열과 대상 값이 주어지면 대상이 발견되면 인덱스를 반환  
> 그렇지 않은 경우 순서대로 삽입된 인덱스를 반환

- [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

```java
class Solution {
    // Binary Search
    // T: O(log n)
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int pivot;
        
        while (left <= right) {
            pivot = left + (right - left) / 2;
            if (target < nums[pivot]) right = pivot - 1;
            else if (target > nums[pivot]) left = pivot + 1;
            else return pivot; 
        }
        
        return left;
    }
}
```
