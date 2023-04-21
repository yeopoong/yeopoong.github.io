---
layout: post
published: true
title: "150. Evaluate Reverse Polish Notation"
categories: interview
tags: problems stack
---

> 표현식을 평가하고 표현식의 값을 나타내는 정수를 반환

- [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

```java
class Solution {
        
    // 표현식을 평가하고 표현식의 값을 나타내는 정수를 반환
    // 연산자: +, -, *, /
    // 표현식은 유효하다고 가정
    // T: O(n), S: O(n)
    public int evalRPN(String[] tokens) {
        
        Stack<Integer> stack = new Stack<>();
        
        for (String token : tokens) {
            
            if (!"+-*/".contains(token)) {
                stack.push(Integer.valueOf(token));
                continue;
            }
            
            int number2 = stack.pop();
            int number1 = stack.pop();
            
            int result = 0;
            
            switch (token) {
                case "+":
                    result = number1 + number2;
                    break;
                case "-":
                    result = number1 - number2;
                    break;
                case "*":
                    result = number1 * number2;
                    break;
                case "/":
                    result = number1 / number2;
                    break;
            }
            
            stack.push(result);
            
        }
        
        return stack.pop();
    }
}
```