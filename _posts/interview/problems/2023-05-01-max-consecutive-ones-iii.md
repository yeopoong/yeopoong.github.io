---
layout: post
published: true
title: "1004. Max Consecutive Ones III"
categories: interview
tags: problems array two-pointers
---

> 이진 배열 nums와 정수 k가 주어지면 최대 k개의 0을 뒤집을 수 있는 경우 배열에서 연속된 1의 최대 개수를 반환

- [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

```java
class Solution {
    
    // 최대 k개의 0을 뒤집을 수 있는 경우, 배열에서 최대 연속 1의 수
    // T: O(n)
    public int longestOnes(int[] nums, int k) {
        int left = 0, right = 0;
        
        for (; right < nums.length; right++) {
            // 0이 포함되면 K를 감소한다.
            if (nums[right] == 0) {
                k--;
            }
            // 허용된 수보다 많은 0이 존재하면
            if (k < 0 && nums[left++] == 0) {
                k++;
            }
        }     
        
        return right - left;
    }
}
```
