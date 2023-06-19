---
layout: post
published: true
title: "163. Missing Ranges"
categories: interview
tags: easy interval
---

> [lower, upper] 범위의 정렬된 정수 배열에서 누락된 모든 숫자를 정확히 포함하는 범위의 가장 짧은 정렬 목록을 반환

[163. Missing Ranges](https://leetcode.com/problems/missing-ranges/)

```java
class Solution {
    
    // 누락된 범위
    // T: O(n)
    public List<List<Integer>> findMissingRanges(int[] nums, int lower, int upper) {
        List<List<Integer>> result = new ArrayList<>();
        
        int prev = lower - 1;
        for (int i = 0; i <= nums.length; i++) {
            int curr = (i < nums.length) ? nums[i] : upper + 1;
            if (prev + 1 <= curr - 1) {
                result.add(Arrays.asList(prev + 1, curr - 1));
            }
            prev = curr;
        }
        
        return result;
    }
}
```
