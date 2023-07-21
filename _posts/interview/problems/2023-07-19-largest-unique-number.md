---
layout: post
published: true
title: "1133. Largest Unique Number"
categories: interview
tags: easy array
---

> 정수 배열 nums가 주어지면 한 번만 발생하는 가장 큰 정수를 반환

[1133. Largest Unique Number](https://leetcode.com/problems/largest-unique-number/)

```java
class Solution {
    public int largestUniqueNumber(int[] nums) {
        int result = -1;
        
        Map<Integer, Integer> count = new HashMap<>();
        
        // Store counts of each element
        for (int i : nums) {
            count.put(i, count.getOrDefault(i, 0) + 1);
        }
        
        for (Map.Entry<Integer, Integer> entry : count.entrySet()) {
            // If count of the integer is 1 get maximum.
            if (entry.getValue() == 1) {
                result = Math.max(result, entry.getKey());
            }
        }
        
        return result;
    }
}
```