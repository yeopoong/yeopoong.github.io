---
layout: post
published: true
title: "1165. Single-Row Keyboard"
categories: interview
tags: easy string 
---

> 단일 행에 모든 키가 있는 특수 키보드가를 이용해서 문자열 단어를 입력하려고 합니다. 한 손가락으로 입력하는 데 걸리는 시간을 계산하는 함수를 작성

[1165. Single-Row Keyboard](https://leetcode.com/problems/single-row-keyboard/)

```java
class Solution {
    public int calculateTime(String keyboard, String word) {
        int sum = 0;
        
        int[] index = new int[26];
        
        for (int i = 0; i < keyboard.length(); ++i) {
            index[keyboard.charAt(i) - 'a'] = i;
        }
        
        int last = 0;
        for (char c : word.toCharArray()) {
            sum += Math.abs(index[c - 'a'] - last);
            last = index[c - 'a'];
        }
        
        return sum;
    }
}
```