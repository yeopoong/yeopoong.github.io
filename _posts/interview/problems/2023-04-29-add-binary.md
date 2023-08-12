---
layout: post
published: true
title: "67. Add Binary"
categories: interview
tags: easy simulation
---

> 두 개의 이진 문자열 a와 b가 주어지면 합계를 이진 문자열로 반환

[67. Add Binary](https://leetcode.com/problems/add-binary/)

```java
class Solution {
    
    // 두 개의 이진 문자열 a와 b가 주어지면 합계를 이진 문자열로 반환
    public String addBinary(String a, String b) {
            
        StringBuilder res = new StringBuilder();
        int carry = 0;
        
        // 뒤에서부터 처리한다.
        int i = a.length() - 1, j = b.length() -1;
            
        while (i >= 0 || j >= 0) {
            int total = carry;
            
            if (j >= 0) total += b.charAt(j--) - '0';
            if (i >= 0) total += a.charAt(i--) - '0';
            
            res.append(total % 2);
            carry = total / 2;
        }
            
        if (carry != 0) res.append(carry);
            
        return res.reverse().toString();
    }
}
```
