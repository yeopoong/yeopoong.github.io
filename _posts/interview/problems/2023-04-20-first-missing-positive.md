---
layout: post
published: true
title: "41. First Missing Positive"
categories: interview
tags: backtracking
---

> 정렬되지 않은 정수 배열 nums가 주어지면 누락된 가장 작은 양의 정수를 반환

- [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

```java
class Solution {
    
    // 정렬되지 않은 정수 배열 nums가 주어지면 누락된 가장 작은 양의 정수를 반환
    public int firstMissingPositive(int[] nums) {
        int n = nums.length; 
        
        int size = 0;

        while (n > 0) {
            n = n >> 1;
            size++;
        }
        
        n = nums.length;
        int pivot = 0;
        
        for (int i = 0; i < n; i++) {
            if (nums[i] <= 0 || nums[i] > n) {
                int temp = nums[i];
                nums[i] = nums[pivot];
                nums[pivot] = temp;
                pivot++;
            }
        }
        
        for (int i = 0; i < pivot; i++) {
            nums[i] = 0;
        }
        
        for (int i = pivot; i < n; i++) {
            nums[(nums[i] - 1) & ((1 << size) - 1)] |= (1 << size);
        }
        
        for (int i= 0; i < n; i++) {
            if ((nums[i] & (1 << size)) == 0) {
                return i + 1;
            }
        }
        
        return n + 1;
    }
}
```