---
layout: post
published: true
title: "14. Longest Common Prefix"
categories: interview
tags: string longest
---

> 문자열 배열 중에서 가장 긴 공통 접두사 문자열을 찾는 함수를 작성

[14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

```java
class Solution {
    // 가장 긴 공통 접두사
    // T: O(s), s is the sum of all characters in all strings.
    public String longestCommonPrefix(String[] strs) {
        String prefix = strs[0];
        
        for (String word : strs) {
            // prefix를 찾을 때까지 반복(시작인덱스가 0이되야 함)
            while (word.indexOf(prefix) != 0) {
                // prefix 길이를 뒤에서 부터 줄인다.
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) return "";
            }
        }
        
        return prefix;
    }
}
```
