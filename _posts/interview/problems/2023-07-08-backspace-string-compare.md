---
layout: post
published: true
title: "844. Backspace String Compare"
categories: interview
tags: easy stack
---

> 두 문자열 s와 t가 주어지면 둘 다 빈 텍스트 편집기에 입력했을 때 같으면 true를 반환. '#'은 백스페이스 문자를 의미

[844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

```java
class Solution {
    // Time Complexity: O(M + N)
    // Space Complexity: O(M + N)
    public boolean backspaceCompare(String s, String t) {
        return build(s).equals(build(t));
    }
    
    public String build(String str) {
        Stack<Character> set = new Stack<>();
        
        for (char c : str.toCharArray()) {
            if (c != '#') {
                set.push(c);
            } else if (!set.empty()) {
                set.pop();
            }
        }
        
        return set.toString();
    }
}
```