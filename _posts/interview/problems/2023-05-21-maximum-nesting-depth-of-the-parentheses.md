---
layout: post
published: true
title: "1614. Maximum Nesting Depth of the Parentheses"
categories: interview
tags: problems string stack
---

> 괄호의 최대 중첩 깊이

- [1614. Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)

```java
class Solution {
    
    // 괄호의 최대 중첩 깊이
    // T: O(n)
    public int maxDepth(String s) {
        int res = 0;
        
        int depth = 0;
        for (int i = 0; i < s.length(); ++i) {
            if (s.charAt(i) == '(') {
                res = Math.max(res, ++depth);
            } else if (s.charAt(i) == ')') {
                depth--;
            }
        }
        
        return res;
    }
}
```