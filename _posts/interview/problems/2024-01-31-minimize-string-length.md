---
layout: post
published: true
title: "2716. Minimize String Length"
categories: interview
tags: easy hashmap string
---

> 문자열에서 인접한 동일한 두문자를 삭제하고 최소화된 문자열의 길이를 반환

[2716. Minimize String Length](https://leetcode.com/problems/minimize-string-length/)

```java
class Solution {
    
    // 최소화된 문자열의 길이를 나타내는 정수를 반환합니다.
    public int minimizedStringLength(String s) {
        char[] chars = s.toCharArray();
        int[] counts = new int[26];
        
        int result =0;
        
        for (char c: chars) {
            counts[c-'a']++;
        }
        
        for (int i: counts) {
            if (i > 0) result++;
        }
        
        return result;
    }
}
```