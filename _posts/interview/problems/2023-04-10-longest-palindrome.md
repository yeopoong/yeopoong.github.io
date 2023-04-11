---
layout: post
published: false
title: "409. Longest Palindrome"
categories: interview
tags: problems hashmap
---

- [409. Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)

```java
class Solution {
    // 팰린드롬은 중복되지 않은 문자를 중간에 한번만 사용할 수 있다.
    public int longestPalindrome(String s) {
        Set<Character> set = new HashSet<>();
        
        // 중복되지 않는 문자를 찾는다.
        for (char c: s.toCharArray()) {
            // 문자가 존재하면 지운다.
            if (!set.add(c)) {
                set.remove(c);
            }
        } 
        
        // 중복되지 않는 문자는 중간에 한번만 나올 수 있다.
        int longest = (set.size() <= 1) ? s.length() : s.length() - set.size() + 1;
        
        return longest; 
    }
}
```