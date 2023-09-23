---
layout: post
published: true
title: "2278. Percentage of Letter in String"
categories: interview
tags: easy string
---

> 문자열 s와 문자가 주어지면, s에서 문자와 동일한 문자의 백분율을 가장 가까운 정수 백분율로 내림하여 반환

[2278. Percentage of Letter in String](https://leetcode.com/problems/percentage-of-letter-in-string/)

```java
class Solution {
    public int percentageLetter(String s, char letter) {
        int result = 0;
        
        int count = 0;
        for (char c: s.toCharArray()) {
            if (c == letter) count++;
        }
        
        result = (count * 100) / s.length();
        
        return result;
    }
}
```