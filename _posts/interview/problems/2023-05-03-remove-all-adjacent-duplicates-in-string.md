---
layout: post
published: true
title: "1047. Remove All Adjacent Duplicates In String"
categories: interview
tags: string stack
---

> 영문 소문자로 구성된 문자열에서 두 개의 인접한 동일한 문자를 반복적으로 제거

- [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

```java
class Solution {
    
    public String removeDuplicates(String s) {
        StringBuilder sb = new StringBuilder();
        
        int sbLength = 0;
        for (char character : s.toCharArray()) {
            if (sbLength != 0 && character == sb.charAt(sbLength - 1)) {
                sb.deleteCharAt(sbLength-- - 1);
            } else {
                sb.append(character);
                sbLength++;
            }
        }
        
        return sb.toString();
    }
}
```
