---
layout: post
published: true
title: "10. Regular Expression Matching"
categories: interview
tags: dfs recursion string
---

> 입력 문자열 s와 패턴 p가 주어지면 '.'을 지원하는 정규식 일치를 구현  
> '.' Matches any single character.​​​​  
> '*' Matches zero or more of the preceding element.  

- [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

```java
class Solution {
    
    boolean[][] cache;
    
    // 정규식 일치: 문자열이 패턴에 매칭되는지 체크 
    public boolean isMatch(String s, String p) {
        cache = new boolean[s.length() + 1][p.length() + 1];

        return dfs(s, p, 0, 0);
    }

    // TOP-Down Memoization
    // T: O(sp)
    private boolean dfs(String s, String p, int i, int j) {
        if (cache[i][j] != false) return cache[i][j];

        if (i >= s.length() && j >= p.length()) return true;

        if (j >= p.length()) return false;

        boolean match = i < s.length() && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.');

        if (j + 1 < p.length() && p.charAt(j + 1) == '*') {
            cache[i][j] = dfs(s, p, i, j + 2) || (match && dfs(s, p, i + 1, j));
        } else {
            cache[i][j] = match && dfs(s, p, i + 1, j + 1);
        }

        return cache[i][j];
    }
}
```