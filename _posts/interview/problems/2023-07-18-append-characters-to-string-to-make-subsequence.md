---
layout: post
published: true
title: "2486. Append Characters to String to Make Subsequence"
categories: interview
tags: medium string
---

> t가 s의 하위 시퀀스가 ​​되도록 s 끝에 추가해야 하는 최소 문자 수를 반환

[2486. Append Characters to String to Make Subsequence](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence/)

```java
class Solution {
    public int appendCharacters(String s, String t) {
        int j = 0;
        
        for (int i = 0; i < s.length() && j < t.length(); i++) {
            // 앞에서부터 순서대로 동일한 문자를 카운트한다.
            j += (s.charAt(i) == t.charAt(j)) ? 1 : 0;
        }
        
        return t.length() - j;
    }
}
```