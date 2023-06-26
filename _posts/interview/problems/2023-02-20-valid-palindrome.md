---
layout: post
published: true
title: "125. Valid Palindrome"
categories: interview
tags: string two-pointers 
---

> 문자열 s가 주어지면 회문이면 true를 반환하고 그렇지 않으면 false를 반환

[125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

![](/assets/img/valid-palindrome.jpg)

두개의 포인터를 문자열의 시작과 끝위치로 설정하고 두 문자를 비교하면서 체크한다.

```java
class Solution {
    
    // Two Pointer
    // T: O(n)
    public boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;
        
        while (i < j) {
            char start = Character.toLowerCase(s.charAt(i));
            char end = Character.toLowerCase(s.charAt(j));
            
            if (!Character.isLetterOrDigit(start)) {
                i++;
            } else if (!Character.isLetterOrDigit(end)) {
                j--;
            } else if (start == end) {
                i++; 
                j--;
            } else {
                return false;
            }
        }
        
        return true;
    }
}