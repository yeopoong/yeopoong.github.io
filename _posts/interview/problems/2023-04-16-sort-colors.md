---
layout: post
published: true
title: "75. Sort Colors"
categories: interview
tags: maximum array dynamic-programming
---

> 빨간색, 흰색 또는 파란색으로 칠해진 n개의 객체가 있는 배열 nums가 주어지면 동일한 색상의 객체가 인접하도록 빨간색, 흰색, 파란색 순서로 색상을 정렬  
> Two Pointer로 비교하면서 0은 앞으로 2는 뒤로 보낸다.

- [75. Sort Colors](https://leetcode.com/problems/sort-colors/)

```java
class Solution {
    // 0은 앞으로 2는 뒤로 보낸다. 
    // O(n)
    public void sortColors(int[] nums) {
        int zeroIndex = 0, twoIndex = nums.length - 1;
        int currIndex = 0;
        
        while (currIndex <= twoIndex) {
            if (nums[currIndex] == 0) { // 0은 앞으로 보낸다.
                swap(nums, zeroIndex++, currIndex++);
            } else if (nums[currIndex] == 2) { // 2는 뒤로 보낸다. 
                // 뒤에서 온 값은 다시 비교해서 처리해야 한다. 
                swap(nums, twoIndex--, currIndex); 
            } else {
                currIndex++;
            }
        }
    }

    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```