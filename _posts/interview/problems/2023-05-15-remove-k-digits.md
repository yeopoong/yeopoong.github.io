---
layout: post
published: true
title: "402. Remove K Digits"
categories: interview
tags: monotonic-stack
---

> 음수가 아닌 정수 num을 나타내는 문자열 num과 정수 k가 주어지면 num에서 k 자리를 제거한 후 가능한 가장 작은 정수를 반환  
> - 큰 숫자순으로 선택해서 제거해야 하므로 스택에 큰숫자 순서로 저장한다: Monotonic Increasing Stack

- [402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

```java
class Solution {
    
    // num에서 k 자리를 제거한 후 가장 작은 정수
    // 스택에 작은 숫자 순서로 입력하고 꺼낸다.
    // T: O(n), S: O(n)
    public String removeKdigits(String num, int k) {
        String smallest = "";
        
        if (num.length() == k) return "0";
        
        // Monotonic Increasing Stack
        Stack<Character> stack = new Stack<>();
        
        // 스택에 큰 숫자를 넣는다.
        for (char c: num.toCharArray()) {
            // 아직 제거할 숫자가 남아 있고 스택에 더 큰 숫자가 존재하면 스택에서 꺼낸다.
            while (k > 0 && !stack.isEmpty() && stack.peek() > c) {
                stack.pop();
                k--;
            }
            stack.push(c);
        }
        
        while (k-- > 0) stack.pop();
        
        // Stack to String
        while (!stack.isEmpty()) {
            smallest = stack.pop() + smallest;
        }
        
        // Remove leading 0
        while (smallest.length() > 1 && smallest.charAt(0) == '0') {
            smallest = smallest.substring(1);
        }
        
        return smallest;
    }
}
```