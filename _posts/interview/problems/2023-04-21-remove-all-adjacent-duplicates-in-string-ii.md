---
layout: post
published: true
title: "1209. Remove All Adjacent Duplicates in String II"
categories: interview
tags: stack string
---

> 인접한 K개의 중복 문자를 제거하고 더 이상 K 중복 문자가 없으면 최종 문자열을 반환

- [1209. Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)

```java
class Solution {
    // 인접한 K개의 중복 문자를 제거하고 더 이상 K 중복 문자가 없으면 최종 문자열을 반환
    // Stack
    // T: O(n)
    public String removeDuplicates(String s, int k) {
        StringBuilder sb = new StringBuilder(s);
        
        Stack<Integer> counts = new Stack<>();
        for (int i = 0; i < sb.length(); ++i) {
            if (i == 0 || sb.charAt(i) != sb.charAt(i - 1)) {
                counts.push(1);
            } else {
                int incremented = counts.pop() + 1;
                if (incremented == k) {
                    sb.delete(i - k + 1, i + 1);
                    i = i - k;
                } else {
                    counts.push(incremented);
                }
            }
        }
        
        return sb.toString();
    }
}
```

```java
class Solution {
    // 인접한 K개의 중복 문자를 제거하고 더 이상 K 중복 문자가 없으면 최종 문자열을 반환
    // Brute Force
    // T: O(n^2)
    public String removeDuplicates(String s, int k) {
        StringBuilder sb = new StringBuilder(s);
        
        int length = -1;
        while (length != sb.length()) {
            length = sb.length();
            // 연속된 K개의 문자를 삭제한다.
            for (int i = 0, count = 1; i < sb.length(); ++i) {
                if (i == 0 || sb.charAt(i) != sb.charAt(i - 1)) {
                    count = 1;
                } else if (++count == k) {
                    sb.delete(i - k + 1, i + 1);
                    break;
                }
            }
        }
        
        return sb.toString();
    }
}
```