---
layout: post
published: true
title: "186. Reverse Words in a String II"
categories: interview
tags: easy linked-list two-pointers
---

> 문자 배열 s가 주어지면 단어의 순서를 반대로 바꿉다.

[186. Reverse Words in a String II](https://leetcode.com/problems/reverse-words-in-a-string-ii/)

```java
class Solution {
    // 전체 문자열을 뒤집은 다음 각 단어를 뒤집습니다.
    // T: O(n)
    public void reverseWords(char[] s) {
        // 1, reverse the whole sentence
        reverse(s, 0, s.length - 1);
        
        // 2, reverse each word
        int start = 0;
        int end = -1;
        for (int i = 0; i < s.length; i++) {
            if (s[i] == ' ') {
                reverse(s, start, i - 1);
                start = i + 1;
            }
        }
        
        // 3, reverse the last word, if there is only one word this will solve the corner case
        reverse(s, start, s.length - 1);
    }

    public void reverse(char[] s, int start, int end) {
        while (start < end) {
            char temp = s[start];
            s[start] = s[end];
            s[end] = temp;
            start++;
            end--;
        }
    }
}
```
