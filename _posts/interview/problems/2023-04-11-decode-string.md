---
layout: post
published: true
title: "394. Decode String"
categories: interview
tags: stack recursion
---

> 인코딩된 문자열이 주어지면 디코딩된 문자열을 반환  
> - k[encode_sting]

- [394. Decode String](https://leetcode.com/problems/decode-string/)

Stack Solution
```java
class Solution {
    
    // 인코딩된 문자열이 주어지면 디코딩된 문자열을 반환 
    // Using Stack
    // T: O(maxk*n), maxk는 최대숫자, n is the lengthof a given string s
    public String decodeString(String s) {
        String res = "";
        
        Stack<String> stack = new Stack<>();
        
        int num = 0;
        
        for (char c: s.toCharArray()) {
            // 숫자일 경우 문자 스트링을 숫자로 변환한다.
            if (Character.isDigit(c)) {
                num = 10 * num + (c - '0');
            // 반복할 문자열을 스택에 추가한다.
            } else if (c == '[') {
                stack.push(res);
                stack.push(Integer.toString(num));
                res = "";
                num = 0;
            // 결과 스트링을 만든다.
            } else if (c == ']') {
                int repeatTimes = Integer.parseInt(stack.pop());
                StringBuilder temp = new StringBuilder(stack.pop());
                // 반복 횟수 만큼 문자열을 생성한다.
                for (int i = 0; i < repeatTimes; i++) {
                    temp.append(res);
                }
                res = temp.toString();
            // 문자일 경우 
            } else {
                res += c;
            }
        }
        
        return res;
    }
}
```

Recursive Solution
```java
class Solution {
    
    private int pos = 0;
    
    // 인코딩된 문자열이 주어지면 디코딩된 문자열을 반환 
    // Recursion
    // T: O(maxk*n), maxk는 최대숫자, n is the lengthof a given string s
    public String decodeString(String s) {
        return helper(s);
    }
    
    public String helper(String s) {
        StringBuilder sb = new StringBuilder();
        
        int k = 0;
        for (; pos < s.length(); pos++) {
            char c = s.charAt(pos);
            // 문자열을 숫자로 컨버젼
            if (Character.isDigit(c)) {
                k = k * 10 + (c - '0');
            } else if (c == '[') {
                // 문자열을 구한다.
                ++pos;
                String sub = helper(s);
                // K번 반복해서 추가한다.
                for (; k > 0; k--) sb.append(sub); 
            } else if (c == ']') {
                break;
            } else { // letters
                sb.append(c);
            }
        }
        
        return sb.toString();
    }
}
```