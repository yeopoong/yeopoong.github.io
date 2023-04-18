---
layout: post
published: true
title: "8. String to Integer (atoi)"
categories: interview
tags: problems string
---

> 문자열을 부호 있는 32비트 정수로 변환하는 myAtoi(string s) 함수를 구현

- [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

```java
class Solution {
    
    // T: O(n), S: O(1)
    public int myAtoi(String str) {
        int sign = 1, total = 0;
        
        int index = 0;
        int length = str.length();

        //1. Empty string
        if (length == 0) return 0;
    
        //2. Remove leading whitespaces
        while (index < length && str.charAt(index) == ' ') index++;
    
        //3. Handle signs
        if (index < length && (str.charAt(index) == '+' || str.charAt(index) == '-')) {
            sign = (str.charAt(index) == '+') ? 1 : -1;
            index++;
        }
        
        //4. Convert number and avoid overflow
        while (index < length && Character.isDigit(str.charAt(index))) {
            int digit = str.charAt(index) - '0';

            //check if total will be overflow after 10 times
            //2147483647: 214748364 = (INT_MAX / 10)
            if (Integer.MAX_VALUE/10 < total || (Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE %10 < digit)) {
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }

            //append current digit to the result
            total = 10 * total + digit;
            index++;
        }

        return total * sign;
    }
}
```