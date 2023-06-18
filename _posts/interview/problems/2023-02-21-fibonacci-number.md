---
layout: post
published: true
title: "509. Fibonacci Number"
categories: interview
tags: recursion memoization
---

> Fibonacci numbers: 각 숫자는 0과 1부터 시작하여 앞의 두 숫자의 합  
> F(0) = 0, F(1) = 1  
> F(n) = F(n - 1) + F(n - 2), for n > 1.  

[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

## Recursion
```java
public class Solution {
    // 점화식(Recurrence relation): F(n) = F(n-1) + F(n-2)
    // T: O(2^n)
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }
        return fib(n - 1) + fib(n - 2);
    }
}
```

## Recursion witn memoization
```java
class Solution {
    // O(2^N) : 재귀함수로 구현할 경우 (반복해서 계산되는 부분 때문)
    // 점화식(Recurrence relation): F(n) = F(n-1) + F(n-2)
    // Bottom-up
    // T: O(n)
    // S: O(1)

    // Creating a hash map with 0 -> 0 and 1 -> 1 pairs
    private Map<Integer, Integer> cache = new HashMap<>(Map.of(0, 0, 1, 1));

    public int fib(int n) {
        // 종료조건
        if (cache.containsKey(n)) {
            return cache.get(n);
        }
        
        // 재귀호출
        cache.put(n, fib(n - 1) + fib(n - 2));
        
        // 결과리턴
        return cache.get(n);
    }
}
```

## Dynamic Programming
```java
class Solution {
    // 점화식(Recurrence relation): F(n) = F(n-1) + F(n-2)
    // Bottom-up
    // T: O(n)
    // S: O(1)
    public int fib(int n) {
        int a = 0, b = 1;
        int t;
        
        // A값을 리턴하는 것을 전제로한 조건
        while (n-- > 0) {
            t = a + b; // 앞 두수의 합
            a = b;
            b = t;
        }
        
        return a;
    }
}
```
