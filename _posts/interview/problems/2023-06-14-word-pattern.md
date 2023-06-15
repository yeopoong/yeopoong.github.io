---
layout: post
published: true
title: "290. Word Pattern"
categories: interview
tags: easy hashmap
---

> 패턴과 문자열 s가 주어지면 s가 동일한 패턴을 따르는지 확인

[290. Word Pattern](https://leetcode.com/problems/word-pattern/)

```java
class Solution {
    // 패턴과 문자열 s가 주어지면 s가 동일한 패턴을 따르는지 확인
    // O(n)
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");
        
        if (words.length != pattern.length()) return false;
        
        // key:패턴, value=순서
        Map<Object, Integer> index = new HashMap();
        
        for (Integer i = 0; i < words.length; ++i) {
            // 이미 존재하는 값이 있을 경우 이전의 값을 리턴한다.
            // 따라서 같은 패턴일 경우 값이 같아야 한다. 
            if (index.put(pattern.charAt(i), i) != index.put(words[i], i)) {
                return false;
            }
        }
            
        return true;   
    }
}
```
