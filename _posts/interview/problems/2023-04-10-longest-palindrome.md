---
layout: post
published: false
title: "409. Longest Palindrome"
categories: interview
tags: hashmap string palindrome
---

> 소문자 또는 대문자로 구성된 문자열 s가 주어지면 해당 문자로 만들 수 있는 가장 긴 회문의 길이를 반환

- [409. Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)

```java
class Solution {
    // 팰린드롬은 중복되지 않은 문자를 중간에 한번만 사용할 수 있다.
    public int longestPalindrome(String s) {
        Set<Character> set = new HashSet<>();
        
        // 짝수로 중복되지 않는 문자를 찾는다.
        for (char c: s.toCharArray()) {
            // 문자가 존재하면 지운다(찍수이면 지워진다)
            if (!set.add(c)) {
                set.remove(c);
            }
        } 
        
        // 짝수로 중복되지 않는 문자는 중간에 한번만 나올 수 있다.
        int longest = (set.size() <= 1) ? s.length() : s.length() - set.size() + 1;
        
        return longest; 
    }
}
```