---
layout: post
published: true
title: "1668. Maximum Repeating Substring"
categories: interview
tags: easy string
---

> 문자열 시퀀스와 단어가 주어지면 단어의 최대 반복 값을 시퀀스로 반환

[1668. Maximum Repeating Substring](https://leetcode.com/problems/maximum-repeating-substring/)

```java
class Solution {
    // T: O(n^2)
    // S: O(n)
    public int maxRepeating(String sequence, String word) {
        if (!sequence.contains(word)) return 0;
        
        var quest = word;
        var count = 1;
            
        while (sequence.contains(quest)) {
            //concatenation of substring
            quest = quest + word;        
            if (sequence.contains(quest)) {
                //increment count only if substring is present
                count = count + 1;  
            }
        }
        
        return count;
    }
}
```