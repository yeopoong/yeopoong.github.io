---
layout: post
published: true
title: "1207. Unique Number of Occurrences"
categories: interview
tags: problems array hashmap
---

> 정수 배열이 주어지면 배열의 각 값의 발생 횟수가 고유하면 true를 반환하고 그렇지 않으면 false를 반환

- [1207. Unique Number of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences/)

```java
class Solution {
    
    // 고유한 발생 수
    // T: O(n)
    // S: O(n)
    public boolean uniqueOccurrences(int[] arr) {
        // Store the frequency of elements in the unordered map.
        Map<Integer, Integer> freq = new HashMap<>();
        
        for (int num : arr) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }
        
        // Store the frequency count of elements in the unordered set.
        Set<Integer> freqSet = new HashSet<>(freq.values());
        
        // If the set size is equal to the map size, 
        // It implies frequency counts are unique.
        return freq.size() == freqSet.size();
    }
}
```