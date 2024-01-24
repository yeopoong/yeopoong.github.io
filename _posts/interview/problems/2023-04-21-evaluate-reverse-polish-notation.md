---
layout: post
published: true
title: "150. Evaluate Reverse Polish Notation"
categories: interview
tags: medium stack
---

> 표현식을 평가하고 표현식의 값을 나타내는 정수를 반환

[150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

```java
class Solution {
        
    // 표현식을 평가하고 표현식의 값을 나타내는 정수를 반환
    // 연산자: +, -, *, /
    // 표현식은 유효하다고 가정
    // T: O(n), S: O(n)
    // Solution: 연산의 순서가 중요하므로 스택을 사용하여 해결할 수 있다.
    public int evalRPN(String[] tokens) {
        
        Stack<Integer> stack = new Stack<>();
        
        for (String token : tokens) {
            
            // 숫자이면 스택에 추가
            if (!"+-*/".contains(token)) {
                stack.push(Integer.valueOf(token));
                continue;
            }
            
            // 가장 최근 숫자 두개를 연산하고 스텍에 다시 추가한다.
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