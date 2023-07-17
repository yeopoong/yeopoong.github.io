---
layout: post
published: true
title: "44. Wildcard Matching"
categories: interview
tags: hard dfs recursion string
---

> '?' and '*' 를 지원하는 와일드카드 패턴 일치 구현  
> - '.' Matches any single character.​​​​  
> - '*' Matches zero or more of the preceding element.  

- [44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)

```java
class Solution {
    
    // '?' and '*' 를 지원하는 와일드카드 패턴 일치 구현
    public boolean isMatch(String str, String pattern) {
        int s = 0, p = 0, match = 0, starIdx = -1;
        
        while (s < str.length()) {
            // advancing both pointers
            if (p < pattern.length()  && (pattern.charAt(p) == '?' || str.charAt(s) == pattern.charAt(p))) {
                s++;
                p++;
            } // * found, only advancing pattern pointer
            else if (p < pattern.length() && pattern.charAt(p) == '*') {
                starIdx = p;
                match = s;
                p++;
            } // last pattern pointer was *, advancing string pointer
            else if (starIdx != -1) {
                p = starIdx + 1;
                match++;
                s = match;
            }
            // current pattern pointer is not star, last patter pointer was not *
            // characters do not match
            else {
                return false;
            }
        }
        
        // check for remaining characters in pattern
        while (p < pattern.length() && pattern.charAt(p) == '*')
            p++;
        
        return p == pattern.length();
    }
}
```