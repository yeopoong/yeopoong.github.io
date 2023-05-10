---
layout: post
published: true
title: "81. Search in Rotated Sorted Array II"
categories: interview
tags: problems array binary-search
---

> 회전 후 배열 숫자와 정수 대상이 주어지면 대상이 숫자이면 true를 반환하고 숫자가 아니면 false를 반환

- [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

```java
class Solution {
    
    // 음수가 아닌 정수 x가 주어지면 가장 가까운 정수로 내림한 x의 제곱근을 반환합니다.
    // O(log n)
    public int mySqrt(int x) {
        
        if (x == 0 || x == 1) return x;
        
        int left = 0, right = x;
        while (left < right) {
            // mid = (left + right) / 2 can overflow if right > Integer.MAX_VALUE - left
            int mid = left + (right - left) / 2;
            
            // same thing here , mid * mid > x can overflow. replace by mid > x / mid
            if (mid > x / mid) {
                right = mid - 1; 
            } else {
                left = mid + 1;
                // if mid * mid < x but (mid + 1) * (mid + 1) > x then mid was the right answer
                if (left > x / left) {
                    return mid;
                }                
            }
        }
        
        return left;
    }
}
```
