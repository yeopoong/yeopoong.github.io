---
layout: post
published: true
title: "268. Missing Number"
categories: interview
tags: problems array hashmap
---

> 범위 [0, n]에서 n개의 고유한 숫자를 포함하는 배열 nums가 주어지면 범위에서 배열에서 누락된 유일한 숫자를 반환

- [268. Missing Number](https://leetcode.com/problems/missing-number/)

```java
class Solution {
    
    // T: O(n)
    // S: O(n)
    public int missingNumber(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        
        for (int num : nums) set.add(num);

        int last = nums.length + 1;
        
        for (int i = 0; i < last; i++) {
            if (!set.contains(i)) {
                return i;
            }
        }
        
        return -1;
    }
}
```

```java
class Solution {
    
    // T: O(n)
    // S: O(1)
    // XOR - (5 ^ 5 = 0, 0 ^ 5 = 5)
    // SUM([0..n]) - SUM(nums)
    public int missingNumber(int[] nums) {
        int res = nums.length;
        
        for (int i = 0; i < nums.length; i++) {
            res += (i - nums[i]);
        }
        
        return res;
    }
}
```