---
layout: post
published: true
title: "9. Palindrome Number"
categories: interview
tags: problems stack recursion
---

> 팰린드롬 번호: 정수 x가 주어지면 x가 회문이면 true를 반환하고 그렇지 않으면 false를 반환

- [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

```java
class Solution {
    public boolean isPalindrome(int x) {
        // 음수는 팰린드롬이 아니다.
        if (x < 0) return false;
        
        int reverse = 0;
        int num = x;
        
        // 숫자를 뒤집는다.
        while (num != 0) {
            // 뒤집기 위해서 10을 곱해서 한칸 왼쪽으로 보낸다.
            reverse *= 10;
            // 1의 자리
            reverse += num % 10;
            // 1의 자리를 지운다. 
            num /= 10;
        }
        
        return reverse == x;
    }
}
```