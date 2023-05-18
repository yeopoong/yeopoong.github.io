---
layout: post
published: true
title: "80. Remove Duplicates from Sorted Array II"
categories: interview
tags: problems array two-pointers
---

> 정렬된 배열에서 2개 이상의 중복을 제거하고 nums의 첫 번째 k 슬롯에 최종 결과를 배치한 후 k를 반환

- [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

```java
class Solution {
    
    // 정렬된 배열에서 중복 제거
    // nums의 첫 번째 k 슬롯에 최종 결과를 배치한 후 k를 반환
    public int removeDuplicates(int[] nums) {
        
        // Initialize the counter and the second pointer.
        int j = 1, count = 1;
        
        // Start from the second element of the array and process elements one by one.
        for (int i = 1; i < nums.length; i++) {
            // 중복이면 카운트 증가
            if (nums[i] == nums[i - 1]) {
                count++;
            } else {
                count = 1;
            }
            
            // For a count <= 2, we copy the element over thus overwriting the element at index "j" in the array
            if (count <= 2) {
                nums[j++] = nums[i];
            }
        }
        
        return j;
    }
}
```