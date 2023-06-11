---
layout: post
published: true
title: "1047. Remove All Adjacent Duplicates In String"
categories: interview
tags: easy string stack
---

> 영문 소문자로 구성된 문자열에서 두 개의 인접한 동일한 문자를 반복적으로 제거

- [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

```java
class Solution {
    
    // 문자열에서 인접한 모든 중복 항목 제거
    public String removeDuplicates(String s) {
        StringBuilder result = new StringBuilder();
        
        int index = 0;
        for (char c : s.toCharArray()) {
            // 앞에 문자와 같으면 앞문자 삭제
            if (index != 0 && c == result.charAt(index - 1)) {
                result.deleteCharAt(index - 1);
                index--;
            } else {
                result.append(c);
                index++;
            }
        }
        
        return result.toString();
    }
}
```
