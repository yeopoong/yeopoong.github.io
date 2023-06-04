---
layout: post
published: true
title: "32. Longest Valid Parentheses"
categories: interview
tags: stack longest 
---

> 문자 '(' 및 ')'만 포함하는 문자열이 주어지면 가장 긴 유효한(올바른 형식의) 괄호 하위 문자열의 길이를 반환

- [32. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

```java
class Solution {
    
    // 가장 긴 유효한 괄호 하위 문자열의 길이
    // T: O(n)
    public int longestValidParentheses(String s) {
        int max = 0;
        
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                // 스택이 비어 있으면 문자열이 유효하지 않으므로 인덱스값을 추가한다.
                if (stack.empty()) {
                    stack.push(i);
                } else {
                // 문자열이 유효하면 문자열의 길이를 계산하고 최대값과 비교한다. 
                    max = Math.max(max, i - stack.peek());
                }
            }
        }
        
        return max;
    }
}
```