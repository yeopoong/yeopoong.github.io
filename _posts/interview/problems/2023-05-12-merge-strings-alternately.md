---
layout: post
published: true
title: "1768. Merge Strings Alternately"
categories: interview
tags: string two-pointers
---

> 두 개의 문자열 word1과 word2가 주어지면, word1부터 번갈아 가며 문자를 추가하여 문자열을 병합  
> 문자열이 다른 문자열보다 길면 병합된 문자열 끝에 추가 문자를 추가

- [1768. Merge Strings Alternately](https://leetcode.com/problems/merge-strings-alternately/)

```java
class Solution {
    
    // 문자열을 번갈아 병합
    // T: O(m + n)
    public String mergeAlternately(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        
        StringBuilder result = new StringBuilder();
        int i = 0, j = 0;

        while (i < m || j < n) {
            if (i < m) {
                result.append(word1.charAt(i++));
            }
            
            if (j < n) {
                result.append(word2.charAt(j++));
            }
        }

        return result.toString();
    }
}
```