---
layout: post
published: true
title: "1137. N-th Tribonacci Number"
categories: interview
tags: easy dynamic-programming
---

> Tribonacci 수열 Tn은 다음과 같이 정의됩니다.  n이 주어지면 Tn의 값을 반환  
> T0 = ​​0, T1 = 1, T2 = 1 및 Tn+3 = Tn + Tn+1 + Tn+2(n >= 0인 경우)

[1137. N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/)

```java
class Solution {
    
    // F(n+3) = F(n) + F(n+1) + F(n+2)
    public int tribonacci(int n) {
        if (n < 3) return n == 0 ? 0 : 1;

        int x = 0, y = 1, z = 1;
        int tmp;
        for (int i = 3; i <= n; ++i) {
            tmp = x + y + z;
            x = y;
            y = z;
            z = tmp;
        }
        
        return z;
    }
}
```
