---
layout: post
published: true
title: "81. Search in Rotated Sorted Array II"
categories: interview
tags: medium binary-search
---

> 회전 후 배열 숫자와 정수 대상이 주어지면 대상이 숫자이면 true를 반환하고 숫자가 아니면 false를 반환

- [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

```java
class Solution {
    
    public boolean search(int[] nums, int target) {
        int start = 0, end = nums.length - 1, mid = -1;
        while (start <= end) {
            mid = (start + end) / 2;
            if (nums[mid] == target) {
                return true;
            }
            //If we know for sure right side is sorted or left side is unsorted
            if (nums[mid] < nums[end] || nums[mid] < nums[start]) {
                if (target > nums[mid] && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            //If we know for sure left side is sorted or right side is unsorted
            } else if (nums[mid] > nums[start] || nums[mid] > nums[end]) {
                if (target < nums[mid] && target >= nums[start]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            //If we get here, that means nums[start] == nums[mid] == nums[end], then shifting out
            //any of the two sides won't change the result but can help remove duplicate from
            //consideration, here we just use end-- but left++ works too
            } else {
                end--;
            }
        }
        
        return false;
    }
}
```

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        i = 0
        j = len(nums) - 1
        
        while i <= j:
            mid = i + (j - i) // 2
            if nums[mid] == target:
                return True
            elif nums[mid] == nums[i] and nums[mid] == nums[j]:
                i = i + 1
                j = j - 1
            elif nums[mid] >= nums[i]:
                if target >= nums[i] and target < nums[mid]:
                    j = mid - 1
                else:
                    i = mid + 1
            elif nums[mid] <= nums[j]:
                if target > nums[mid] and target <= nums[j]:
                    i = mid + 1
                else:
                    j = mid - 1
        return False
```
