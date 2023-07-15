---
layout: post
published: true
title: "161. One Edit Distance"
categories: interview
tags: medium string two-pointers
---

> 두 문자열 s와 t가 주어지면 둘 다 편집 거리만큼 떨어져 있으면 true를 반환하고 그렇지 않으면 false를 반환

[161. One Edit Distance](https://leetcode.com/problems/one-edit-distance/)

```java
class Solution {
    
    public boolean isOneEditDistance(String s, String t) {
        if (Math.abs(s.length()-t.length()) > 1) return false;
        if (s.length() == t.length()) return isOneModify(s,t);
        if (s.length() > t.length()) return isOneDel(s,t);
        
        return isOneDel(t,s);
    }
    
    public boolean isOneModify(String s,String t) {
        int diff = 0;
        
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) != t.charAt(i)) diff++;
        }
        
        return diff == 1;
    }
    
    public boolean isOneDel(String s,String t) {
        for (int i = 0, j = 0; i < s.length() && j < t.length(); i++, j++) {
            if (s.charAt(i) != t.charAt(j)) {
                return s.substring(i+1).equals(t.substring(j));
            }
        }
        
        return true;
    }
}
```