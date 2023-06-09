---
layout: post
published: true
title: "58. Length of Last Word"
categories: interview
tags: string
---

> 단어와 공백으로 구성된 문자열 s가 주어지면 문자열의 마지막 단어 길이를 반환

[58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

```java
class Solution {
    // 마지막 단어의 길이
    // T: O(n)
    public int lengthOfLastWord(String s) {
        int length = 0;
        
        int p = s.length() - 1;
        while (p >= 0) {
            // we're in the middle of the last word
            if (s.charAt(p) != ' ') {
                length++;
            } else if (length > 0) {
                break;
            }
            p--;
        }
        
        return length;
    }
}
```
