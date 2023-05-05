---
layout: post
published: true
title: "239. Sliding Window Maximum"
categories: interview
tags: problems array prefix-sum
---

> 양의 정수 배열이 주어지면 가능한 모든 홀수 길이 하위 배열의 합을 반환

- [1588. Sum of All Odd Length Subarrays](https://leetcode.com/problems/sum-of-all-odd-length-subarrays/)


```java
class Solution {
    
    // 모든 홀수 길이 하위 배열의 합
    // T: O(n^2)
    public int sumOddLengthSubarrays(int[] arr) {
        int total = 0, sum = 0;

        for (int left = 0; left < arr.length; ++left) {
            sum = 0;  
            for (int right = left; right < arr.length; ++right) {
                sum += arr[right];
                // 하위 배열의 길이가 홀수이면 총합에 더한다.
                total += (right - left + 1) % 2 == 1 ? sum : 0;
            }
        }

        return total;
    }
}
```
