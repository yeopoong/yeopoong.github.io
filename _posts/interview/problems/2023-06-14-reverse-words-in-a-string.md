---
layout: post
published: true
title: "151. Reverse Words in a String"
categories: interview
tags: easy string
---

> 단일 공백으로 연결된 단어의 문자열을 역순으로 반환

[151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

```java
class Solution {
    
    // 입력 문자열 s가 주어지면 단어의 순서를 반대로 바꿉니다.
    // T: O(n)
    public String reverseWords(String s) {
        StringBuilder result = new StringBuilder();
        
        String[] words = s.trim().split(" ");
        
        for (int i = words.length - 1; i >= 0; i--) {
            if (!words[i].isEmpty()) {
                result.append(words[i]).append(" ");
            }
        }
        
        return result.toString().trim();
    }
}
```
