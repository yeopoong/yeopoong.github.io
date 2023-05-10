---
layout: post
published: false
title: "5. Longest Palindromic Substring"
categories: interview
tags: problems two-pointers string longest dynamic-programming
---

> 문자열 s가 주어지면 s에서 가장 긴 회문 부분 문자열을 반환

- [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

```java
class Solution {
    
    String result;
    int maxLen;
    
    // 센터 주변 확장
    // T: O(n^2), S: O(1)
    public String longestPalindrome(String s) {
        
        for (int i = 0; i < s.length(); i++) {
            // 1. 문자열의 길이가 홀수일 경우
            getPalindrome(s, i, i);
            // 2. 문자열의 길이가 짝수일 경우
            getPalindrome(s, i, i+1);
        }
        
        return result; 
    }
    
    public void getPalindrome(String s, int left, int right) {
        int len = 0;
        
        // 팰린드롬이면 길이를 넓혀서 체크한다(인바운드와 팰린드롬 체크)
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            len = right - left + 1;
            // 현재길이가 최대길이보다 크면 결과 문자열을 업데이트 한다.
            if (len > maxLen) {
                result = s.substring(left, right + 1);
                maxLen = len;
            }
            left--;
            right++;
        }
    }
}
```