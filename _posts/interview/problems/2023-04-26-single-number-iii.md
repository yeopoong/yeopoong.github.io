---
layout: post
published: true
title: "260. Single Number III"
categories: interview
tags: array bit-manipulation
---

> 정확히 두 개의 요소가 한 번만 나타나고 다른 모든 요소는 정확히 두 번 나타나는 정수 배열 nums에서 한 번만 나타나는 두 요소 찾기

- [260. Single Number III](https://leetcode.com/problems/single-number-iii/)

```java
class Solution {
    
    // 한 번만 나타나는 두 요소를 찾으십시오.
    // T: O(n), S: O(n)
    public int[] singleNumber(int[] nums) {
        int[] output = new int[2];
        
        Map<Integer, Integer> map = new HashMap();
        for (int n : nums) {
            map.put(n, map.getOrDefault(n, 0) + 1);
        }

        int idx = 0;
        for (Map.Entry<Integer, Integer> item : map.entrySet()) {
            if (item.getValue() == 1) {
                output[idx++] = item.getKey();
            }
        }

        return output;
    }
}
```