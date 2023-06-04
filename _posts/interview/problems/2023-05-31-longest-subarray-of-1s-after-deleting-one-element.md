---
layout: post
published: true
title: "1493. Longest Subarray of 1's After Deleting One Element"
categories: interview
tags: sliding-window longest
---

> 결과 배열에 1만 포함된 비어 있지 않은 가장 긴 하위 배열의 크기를 반환

- [1493. Longest Subarray of 1's After Deleting One Element](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/)

```java
class Solution {
    public int longestSubarray(int[] nums) {
        int longestWindow = 0;
        
        // Number of zero's in the window.
        int zeroCount = 0;
        
        // Left end of the window.
        int start = 0;
        
        for (int i = 0; i < nums.length; i++) {
            zeroCount += (nums[i] == 0 ? 1 : 0);
                          
            // Shrink the window until the zero counts come under the limit.
            while (zeroCount > 1) {
                zeroCount -= (nums[start] == 0 ? 1 : 0);
                start++;
            }
              
            longestWindow = Math.max(longestWindow, i - start);
        }

        return longestWindow;
    }
}
```
