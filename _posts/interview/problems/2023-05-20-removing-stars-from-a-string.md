---
layout: post
published: true
title: "2390. Removing Stars From a String"
categories: interview
tags: string stack
---

> 가장 높은 고도 찾기

- [2390. Removing Stars From a String](https://leetcode.com/problems/removing-stars-from-a-string/)

```java
class Solution {
    
    // 문자열에서 별 제거
    // T: O(n)
    public String removeStars(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '*') {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }

        StringBuilder answer = new StringBuilder();
        while (!stack.isEmpty()) {
            answer.append(stack.pop());
        }

        return answer.reverse().toString();
    }
}
```