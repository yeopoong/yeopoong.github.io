---
layout: post
published: true
title: "202. Happy Number"
categories: interview
tags: problems hashmap math
---

> Happy Number: 자릿수 제곱의 합이 1 이 되는 수

- [202. Happy Number](https://leetcode.com/problems/happy-number/)

```java
class Solution {
    // Happy Number: 자릿수 제곱의 합이 1 이 되는 수
    public boolean isHappy(int n) {
        //반복체크
        Set<Integer> seen = new HashSet<>();
        
        while (n != 1 && !seen.contains(n)) {
            seen.add(n);
            n = getNext(n);
        }
        
        return n == 1;
    }
    
    private int getNext(int n) {
        int totalSum = 0;
        
        while (n > 0) {
            //1의 자리
            int d = n % 10;
            
            //10의 자리
            n = n / 10;
            
            totalSum += d * d;
        }
        
        return totalSum;
    }
}
```