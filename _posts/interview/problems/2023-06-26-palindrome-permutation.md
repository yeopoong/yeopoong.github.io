---
layout: post
published: true
title: "266. Palindrome Permutation"
categories: interview
tags: easy palindrome
---

> 문자열 s가 주어지면 문자열의 순열이 회문을 형성할 수 있으면 true를 반환하고 그렇지 않으면 false를 반환

[266. Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation/)

팰린드롬이 될려면 중복되지 않는 문자가 1개 이하여야 한다.

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        int count = 0;
        
        int[] map = new int[128];
        
        for (char c: s.toCharArray()) {
            map[c]++;
            if (map[c] % 2 == 0)
                count--;
            else
                count++;
        }
        
        return count <= 1;
    }
}
```