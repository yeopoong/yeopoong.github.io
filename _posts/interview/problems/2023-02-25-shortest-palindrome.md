---
layout: post
published: false
title: "214. Shortest Palindrome"
categories: interview
tags: problems palindrome
---

- [214. Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/)
<script src="https://gist.github.com/yeopoong/a7f6c98070ce19ca6dcf18c26ad61594.js"></script>

```java
class Solution {
    // 앞에 문자를 추가하여 찾을 수 있는 가장 짧은 회문
    // T: O(n^2)
    public String shortestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        
        // 문자를 뒤집는다.
        StringBuilder sb = new StringBuilder();
        for (int i = s.length() - 1; i >= 0; i--) {
            sb.append(s.charAt(i));
        }
        
        String t = sb.toString();
        for (int i = 0; i <= t.length(); i++) {
            // 뒤집은 문자열의 부분문자열로 원래 문자열이 시작되는 부분을 찾는다.
            if (s.startsWith(t.substring(i))) {
                // 누락된 부분을 앞에 추가해 준다.
                return t.substring(0, i) + s;
            }
        }
        
        return t + s;
    }
}
```