---
layout: post
published: true
title: "191. Number of 1 Bits"
categories: interview
tags: easy bit-manipulation
---

> 부호 없는 정수의 이진수 표현을 가져와 '1' 비트 수(해밍 가중치라고도 함)를 반환

[191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

```java
public class Solution {
    // The input must be a binary string of length 32.
    // cf. https://loosie.tistory.com/238
    public int hammingWeight(int n) {
        int num = 0;
        
        // 비트마스크 & 연산 (0일때까지 반복 -> 0이면 더 이상 1이 없다는 것이다)
        while (n != 0) {
            // 1이면 카운트 증가
            num += n & 1;
            
            // 오른쪽으로 이동
            n = n >>> 1;
        }
        
        return num;
    }
}
```