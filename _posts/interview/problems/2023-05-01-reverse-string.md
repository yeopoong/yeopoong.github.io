---
layout: post
published: true
title: "344. Reverse String"
categories: interview
tags: string two-pointers
---

> 문자 배열로 주어진 문자열을 반전시키는 함수를 작성

[344. Reverse String](https://leetcode.com/problems/reverse-string/)

```java
class Solution {
    // Two Pointers
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            swap(s, left++, right--);
        }
    }
    
    public void swap(char[] s, int left, int right) {
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp; 
    }
}
```
