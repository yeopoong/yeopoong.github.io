---
layout: post
published: true
title: "7. Reverse Integer"
categories: interview
tags: medium math
---

> 부호 있는 32비트 정수 x가 주어지면 숫자가 반전된 x를 반환. x를 반대로 하면 값이 부호 있는 32비트 정수 범위 [-231, 231 - 1]를 벗어나게 되는 경우 0을 반환

[7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

```java
class Solution {
    public int reverse(int x) {
        int MAX_INT = Integer.MAX_VALUE;
        int MIN_INT = Integer.MIN_VALUE;
        long rev = 0;

        while (x != 0) {
            // 가장뒷자리값을 구한다.
            int digit = x % 10;
            // 한자리씩 증가시킨다.
            rev = rev * 10 + digit;
            if (rev > MAX_INT || rev < MIN_INT) {
                return 0;
            }
            x /= 10;
        }

        return (int) rev;
    }
}
```