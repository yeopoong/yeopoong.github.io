---
layout: post
published: true
title: "283. Move Zeroes"
categories: interview
tags: easy two-pointers array
---

> 정수 배열 nums가 주어지면 0이 아닌 요소의 상대적인 순서를 유지하면서 모든 0을 끝으로 이동

[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

```java
class Solution {
    // 0 이 아닌 숫자를 앞에서 부터 채워 넣는다.
    // T: O(n), S: O(1)
    public void moveZeroes(int[] nums) {
        // one pointer for non-zero elements
        int left = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[left++] = nums[i];
                //reverse(nums, left++, i);
            }
        }
        
        // 스왑 대신 나머지값들을 0으로 변경한다.
        for (int i = left; i < nums.length; i++) {
            nums[i] = 0;
        }
    }
    
    public void reverse(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```