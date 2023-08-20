---
layout: post
published: true
title: "338. Counting Bits"
categories: interview
tags: easy bit-manipulation
---

> 정수 n이 주어지면 각 i(0 <= i <= n)에 대해 ans[i]가 i의 이진 표현에서 1의 개수가 되도록 길이 n + 1의 배열 ans를 반환

[338. Counting Bits](https://leetcode.com/problems/counting-bits/)

```java
public class Solution {
    
    // T: O(nlogn)
    public int[] countBits(int n) {
        int[] ans = new int[n + 1];
        
        for (int x = 0; x <= n; ++x) {
            ans[x] = popCount(x);
        }
        
        return ans;
    }
    
    private int popCount(int x) {
        int count;
        
        for (count = 0; x != 0; ++count) {
            x &= x - 1; // 0이 아닌 최하위 비트를 0으로 만들기
        }
        
        return count;
    }

}
```