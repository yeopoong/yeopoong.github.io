---
layout: post
published: true
title: "242. Valid Anagram"
categories: interview
tags: problems string 
---

> 두 문자열 s와 t가 주어지면 t가 s의 애너그램이면 true를 반환하고 그렇지 않으면 false를 반환
> An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

```java
class Solution {
    // 각 문자의 횟수를 카운트해서 0이 아니면 아나그램이 아니다.
    public boolean isAnagram(String s, String t) {
        int[] ascii = new int[128];
        
        for (int i = 0; i < s.length(); i++) ascii[s.charAt(i)]++;
        for (int i = 0; i < t.length(); i++) ascii[t.charAt(i)]--;
        
        for (int i : ascii) {
            if (i != 0) return false;
        }
        
        return true;
    }
    
    /*
    public boolean isAnagram(String s, String t) {
        int[] alphabet = new int[26];
        
        for (int i = 0; i < s.length(); i++) alphabet[s.charAt(i) - 'a']++;
        for (int i = 0; i < t.length(); i++) alphabet[t.charAt(i) - 'a']--;
        
        for (int i : alphabet) if (i != 0) return false;
        
        return true;
    }
    */
}
```