---
layout: post
published: true
title: "136. Single Number"
categories: interview
tags: array bit-manipulation
---

> 정수 배열이 주어지면 모든 원소 중에서 한번만 존재하는 원소 찾기

- [136. Single Number](https://leetcode.com/problems/single-number/)

```java
class Solution {
    // 모든 원소 중에서 한번만 존재하는 원소 찾기
    // XOR 연산을 사용하면 여러개의 값 중에서 동일한 값들을 제거할 수 있다(동일한 값의 순서는 상관없다)
    // XOR 연산으로 암호화 할 수 있다.
    // T: O(n), S: O(1)
    public int singleNumber(int[] nums) {
        int result = 0;
        
        // 0 XOR A = A,  A XOR A = 0
        for (int n : nums) {
            result ^= n;
        }
        
        return result;
    }
}
```