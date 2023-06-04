---
layout: post
published: false
title: "300. Longest Increasing Subsequence"
categories: interview
tags: array longest dynamic-programming dfs
---

> 정수 배열 nums가 주어지면 가장 긴 엄격하게 증가하는 하위 시퀀스의 길이를 반환

- [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

```java
class Solution {
    private int max = 0;
    
    // 가장 긴 증가하는 서브배열의 길이
    // Brute Force with DFS: O(2^n)
    // DFS with cache: O(n^2)
    public int lengthOfLIS(int[] nums) {
        int max = 1;
        
        int[] LIS = new int[nums.length];
        Arrays.fill(LIS, 1);
        
        // 마지막 요소부터 시작한다(Two Pointer: i, j) 
        // [1,2,4,3]
        for (int i = nums.length - 2; i >= 0; i--) {
            for (int j = i + 1; j < nums.length; j++) {
                // 다음값이 클 경우에 최대 길이를 비교해서 갱신한다.
                if (nums[i] < nums[j]) {
                    LIS[i] = Math.max(LIS[i], 1 + LIS[j]);
                }
            }
            max = Math.max(max, LIS[i]);
        }
        
        return max; 
    }
}
```