---
layout: post
published: true
title: "1657. Determine if Two Strings Are Close"
categories: interview
tags: string hashamp
---

> 두 개의 문자열, word1과 word2가 주어지면 word1과 word2가 가깝다면 true를 반환하고 그렇지 않으면 false를 반환  
> - Operation 1: Swap any two existing characters  
> - Operation 2: Transform every occurrence of one existing character into another existing character

[1657. Determine if Two Strings Are Close](https://leetcode.com/problems/determine-if-two-strings-are-close/)

```java
class Solution {
    
    // 두 문자열이 가까운지 확인
    public boolean closeStrings(String word1, String word2) {
        
        if (word1.length() != word2.length()) {
            return false;
        }
        
        Map<Character, Integer> word1Map = new HashMap<>();
        Map<Character, Integer> word2Map = new HashMap<>();
        
        for (char c : word1.toCharArray()) {
            word1Map.put(c, word1Map.getOrDefault(c, 0) + 1);
        }
        
        for (char c : word2.toCharArray()) {
            word2Map.put(c, word2Map.getOrDefault(c, 0) + 1);
        }
        
        if (!word1Map.keySet().equals(word2Map.keySet())) {
            return false;
        }
        
        List<Integer> word1FrequencyList = new ArrayList<>(word1Map.values());
        List<Integer> word2FrequencyList = new ArrayList<>(word2Map.values());
        
        Collections.sort(word1FrequencyList);
        Collections.sort(word2FrequencyList);
        
        return word1FrequencyList.equals(word2FrequencyList);
    }
}
```

