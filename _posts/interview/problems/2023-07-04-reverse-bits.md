---
layout: post
published: true
title: "190. Reverse Bits"
categories: interview
tags: easy bit-manipulation
---

> 주어진 32비트 부호 없는 정수의 반전

[190. Reverse Bits](https://leetcode.com/problems/reverse-bits/)

가장 오른쪽 비트를 구해서 결과비트에 더하고 왼쪽으로 시프트 시킨다.

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int reverse = 0;
        
        for (int i = 0; i < 32; i++) {
            // 왼쪽으로 한칸씩 옴기고 마지막 자리에 원본값의 마지막 자리를 추가한다.
            reverse = (reverse << 1) + (n & 1);
            // 오른쪽으로 한칸 옮겨서 다음 자리를 1의 자리로 만든다.
            n >>= 1;
        } 
        
        return reverse;
    }
}
```