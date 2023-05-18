---
layout: post
published: true
title: "26. Remove Duplicates from Sorted Array"
categories: interview
tags: problems array two-pointers
---

> 정렬된 배열에서 중복 제거하고 재배치 한 후 고유한 요소의 수를 반환

- [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

```java
class Solution {
    // 정렬된 배열에서 중복 제거하고 재배치 한 후 고유한 요소의 수를 반환
    // O(n)
    public int removeDuplicates(int[] nums) {
        int insertIndex = 1;
        
        for (int i = 1; i < nums.length; i++) {
            // 중복이 아니면
            if (nums[i - 1] != nums[i]) {
                // 현재값을 앞에서 부터 입력하고 인덱스를 증가시킨다. 
                nums[insertIndex++] = nums[i];
            }
        }
        
        return insertIndex;
    }
}
```