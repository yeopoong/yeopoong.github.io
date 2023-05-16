---
layout: post
published: true
title: "166. Fraction to Recurring Decimal"
categories: interview
tags: problems string math
---

> 분수의 분자와 분모를 나타내는 두 개의 정수가 주어지면 분수를 문자열 형식으로 반환

- [166. Fraction to Recurring Decimal](https://leetcode.com/problems/fraction-to-recurring-decimal/)

중요한 것은 음의 정수, 가능한 오버플로 등을 포함하여 이 문제를 생각하면서 모든 엣지 케이스를 고려하는 것

```java
class Solution {
    
    // 분수의 분자와 분모를 나타내는 두 개의 정수가 주어지면 분수를 문자열 형식으로 반환
    public String fractionToDecimal(int numerator, int denominator) {
        StringBuilder res = new StringBuilder();
        
        if (numerator == 0) {
            return "0";
        }
        
        // "+" or "-"
        res.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        
        // integral part
        res.append(num / den);
        num %= den;
        if (num == 0) {
            return res.toString();
        }
        
        // fractional part
        res.append(".");
        HashMap<Long, Integer> map = new HashMap<Long, Integer>();
        map.put(num, res.length());
        while (num != 0) {
            num *= 10;
            res.append(num / den);
            num %= den;
            if (map.containsKey(num)) {
                int index = map.get(num);
                res.insert(index, "(");
                res.append(")");
                break;
            }
            else {
                map.put(num, res.length());
            }
        }
        
        return res.toString();
    }
}
```