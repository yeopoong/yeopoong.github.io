---
layout: post
published: true
title: "2330. Valid Palindrome IV"
categories: interview
tags: medium palindrome
---

> 문자열에서 하나 또는 두 개의 문자를 변경해서 회문으로 만들 수 있으면 true를 반환하고 그렇지 않으면 false를 반환

[2330. Valid Palindrome IV](https://leetcode.com/problems/valid-palindrome-iv/)

```java
class Solution {
    
    // O(n) time | O(1) space
    public boolean makePalindrome(String s) {
        int miss = 0;
        
        int left = 0, right = s.length() - 1;
        
        while (left < right)  {
            if (s.charAt(left++) != s.charAt(right--)) {
                miss++;
            }
        }
        
        return miss < 3;
    }
}
```