---
layout: post
published: true
title: "209. Minimum Size Subarray Sum"
categories: interview
tags: medium sliding-window prefix-sum
---

> 합계가 target보다 크거나 같은 하위 배열의 최소 길이를 반환

[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

```java
class Solution {
    
    // 합이 target 보다 큰 부분배열의 최소 길이 
    // O(n)
    public int minSubArrayLen(int target, int[] nums) {
        int min = Integer.MAX_VALUE;
        
        //Two pointer
        int left = 0, right = 0; 
        
        int sum = 0; 
        while (right < nums.length) {
            sum += nums[right];

            // target보다 합이 크면
            while (sum >= target) {
                // 부분배열 길이의 최소값을 구함 
                min = Math.min(min, right - left + 1);
                
                // 합을 감소하고 왼쪽으로 이동
                sum -= nums[left++];
            }
            
            right++;
        }

        // if there is no such subarray, return 0
        return (min == Integer.MAX_VALUE) ? 0 : min;
    }
}
```
