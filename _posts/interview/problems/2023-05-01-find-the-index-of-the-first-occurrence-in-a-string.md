---
layout: post
published: true
title: "28. Find the Index of the First Occurrence in a String"
categories: interview
tags: problems string two-pointers
---

> 두 개의 문자열 needle과 haystack이 주어지면 haystack에서 needle이 처음 나타나는 인덱스를 반환하거나, needle이 haystack의 일부가 아니면 -1을 반환합니다.

- [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

```java
class Solution {
    // 문자열에서 처음 나타나는 인덱스 찾기
    // Sliding Window with two pointer
    // O (n * m)
    public int strStr(String haystack, String needle) {
        
        // 시작 포인터
        for (int i = 0; ; i++) {
            // 검색 문자열의 길이 만큼 반복
            for (int j = 0; ; j++) {
                // 모든 문자가 동일한 경우
                if (j == needle.length()) return i;
                
                // 마지막 문자열을 체크한 경우 더이상 문자열이 없다.
                if (i + j == haystack.length()) return -1;
                
                // 문자를 비교해서 다를경우 시작 인덱스를 이동한다. 
                if (needle.charAt(j) != haystack.charAt(i + j)) break;
            }
        }
    }
}
```
