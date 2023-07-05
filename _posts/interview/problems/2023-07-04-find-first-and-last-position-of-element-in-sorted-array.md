---
layout: post
published: true
title: "190. Reverse Bits"
categories: interview
tags: medium binary-search
---

> 오름차순으로 정렬된 정수 nums의 배열이 주어지면 주어진 대상 값의 시작 위치와 끝 위치를 찾습니다.

[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = new int[2];
        
        result[0] = find(nums, target, true);
        result[1] = find(nums, target, false);
        
        return result;
    }

    private int find(int[] nums, int target, boolean isFirst){
        int idx = -1;
        int start = 0, end = nums.length - 1;
        
        while (start <= end) {
            int mid = (start + end) / 2;
            if (nums[mid] > target) {
                end = mid - 1;
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                idx = mid;
                // 첫번째(앞에 또 있을 수 있다) 또는 마지막(뒤에 또 있을 수 있다) 위치를 찾는다.
                if (isFirst) {
                    end = mid - 1; 
                } else {
                    start = mid + 1;
                }
            }
        }
        
        return idx;
    }
}
```