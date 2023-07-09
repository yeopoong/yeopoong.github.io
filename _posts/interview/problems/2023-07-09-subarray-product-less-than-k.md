---
layout: post
published: true
title: "713. Subarray Product Less Than K"
categories: interview
tags: medium sliding-window
---

> 정수 nums와 정수 k의 배열이 주어지면 하위 배열의 모든 요소의 곱이 k보다 엄격하게 작은 연속 하위 배열의 수를 반환

[713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

```java
class Solution {
    // K보다 작은 부분 배열의 곱
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        // 양수의 곱이 1보다 작을 수 없다.
        if (k <= 1) return 0;
        
        int prod = 1, count = 0;
        
        // Two Pointer
        for (int left = 0, right = 0; right < nums.length; right++) {
            prod *= nums[right];
            
            // K보다 클 경우 왼쪽 포인터를 이동하고 곱에서 제외한다.
            while (prod >= k) {
                prod /= nums[left++];
            }
            
            //Each step introduces x new subarrays, where x is the size of the current window (right - left + 1);
            //for window (5, 2), when 6 is introduced, it add 3 new subarray: (5, (2, (6)))
            count += right - left + 1;
        }
        
        return count;
    }
}
```