---
layout: post
published: true
title: "557. Reverse Words in a String III"
categories: interview
tags: easy two-pointers
---

> 문자열 s가 주어지면 공백과 초기 단어 순서를 유지하면서 문장 내 각 단어의 문자 순서를 반대로 바꾼다.

[557. Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

```java
class Solution {
    
    // 문장 내 각 단어를 뒤집는다.
    public String reverseWords(String s) {
        String[] words = s.split(" ");
        
        for (int index = 0; index <  words.length; index++) {
            words[index] = reverse(words[index]);
        }
        
        return String.join(" ", words);
    }
    
    public String reverse(String s) {
        int start = 0, end = s.length() - 1;
        
        char[] word = s.toCharArray();
        while (start < end) {
            char temp = word[start];
            word[start++] = word[end];
            word[end--] = temp;
        }
        
        return String.valueOf(word);
    }
}
```
