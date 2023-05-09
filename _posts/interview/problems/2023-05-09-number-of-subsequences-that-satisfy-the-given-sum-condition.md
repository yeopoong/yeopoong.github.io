---
layout: post
published: true
title: "1498. Number of Subsequences That Satisfy the Given Sum Condition"
categories: interview
tags: problems array
---

> 최소 및 최대 요소의 합이 target보다 작거나 같도록 nums의 비어 있지 않은 하위 시퀀스의 수를 반환

- [1498. Number of Subsequences That Satisfy the Given Sum Condition](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/)


```java
class Solution {
    
    public int numSubseq(int[] nums, int target) {
        int n = nums.length;
        int mod = 1_000_000_007;
        Arrays.sort(nums);
        
        // Precompute the value of 2 to the power of each value.
        int[] power = new int[n];
        power[0] = 1;
        for (int i = 1; i < n; ++i) {
            power[i] = (power[i - 1] * 2) % mod;
        }
        
        int answer = 0;
        int left = 0, right = n - 1;

        while (left <= right) {
            if (nums[left] + nums[right] <= target) {
                answer += power[right - left];
                answer %= mod;
                left++;
            } else {
                right--;
            }
        }
        
        return answer;
    }
}
```
