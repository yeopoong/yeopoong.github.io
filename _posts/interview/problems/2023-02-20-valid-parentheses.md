---
layout: post
published: true
title: "20. Valid Parentheses"
categories: interview
tags: easy stack 
---

> 입력 문자열(괄호)이 유효한지 확인 

[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

괄호의 순서의 쌍을 체크해야 하므로 스택을 이용한다.

Edge Case  
닫힌 괄호를 만났을때 만약,
1. 스택이 공백이거나 
2. 최상위값이 문자와 매치되지 않으면  
유효하지 않은거다.

```java
class Solution {
    // 입력 문자열(괄호)이 유효한지 확인 
    // T: O(n), S: O(n)
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (char c : s.toCharArray()) {
            //열린 괄호를 만나면 매치되는 괄호를 스택에 넣어서 닫힌 괄호를 만났을때 체크한다.
            if (c == '(') {
                stack.push(')');
            } else if (c == '{') {
                stack.push('}');
            } else if (c == '[') {
                stack.push(']');
                
            // * 닫힌 괄호를 만났을때 스택이 공백이거나 최상위 값이 문자와 매치되지 않으면 유효하지 않은거다.
            } else if (stack.isEmpty() || stack.pop() != c) {
                return false;
            }
        }
        
        return stack.isEmpty();
    }
}
```