---
layout: post
published: true
title: "387. First Unique Character in a String"
categories: interview
tags: easy string hashmap
---

> 문자열이 주어지면 그 안에서 반복되지 않는 첫 번째 문자를 찾고 해당 인덱스를 반환

[387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

```java
class Solution {
    // 각 문자의 횟수를 카운트하고 그 값이 1인 문자의 인덱스를 리턴한다.
    // O(n)
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> countMap = new HashMap<>(); 
        
        // build hash map : character and how often it appears
        for (char ch : s.toCharArray()) {
            countMap.put(ch, countMap.getOrDefault(ch, 0) + 1);
        }
        
        // find the index
        for (int index = 0; index < s.length(); index++) {
            if (countMap.get(s.charAt(index)) == 1) {
                return index; 
            }
        }
        
        return -1;
    }
}
```

```java
class Solution {
    // 각 문자의 횟수를 카운트하고 그 값이 1인 문자의 인덱스를 리턴한다.
    // O(n)
    public int firstUniqChar(String s) {
        int freq[] = new int[26];
        
        for (int i = 0; i < s.length(); i ++) {
            freq[s.charAt(i) - 'a']++;
        }
        
        for (int i = 0; i < s.length(); i ++) {
            if (freq[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }
        
        return -1;
    }
}
```
