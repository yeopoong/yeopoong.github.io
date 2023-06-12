---
layout: post
published: true
title: "1539. Kth Missing Positive Number"
categories: interview
tags: easy array binary-search
---

> 증가하는 순서로 정렬된 양의 정수 배열에서 누락된 k번째 양의 정수를 반환

[1539. Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)

```java
class Solution {
    
    // K번째 누락된 양수
    // T: O(logn)
    public int findKthPositive(int[] arr, int k) {
        int left = 0, right = arr.length - 1;
        
        while (left <= right) {
            int pivot = left + (right - left) / 2;
            // If number of positive integers
            // which are missing before arr[pivot]
            // is less than k -->
            // continue to search on the right.
            if (arr[pivot] - pivot - 1 < k) {
                left = pivot + 1;
            // Otherwise, go left.
            } else {
                right = pivot - 1;
            }
        }

        // At the end of the loop, left = right + 1,
        // and the kth missing is in-between arr[right] and arr[left].
        // The number of integers missing before arr[right] is
        // arr[right] - right - 1 -->
        // the number to return is
        // arr[right] + k - (arr[right] - right - 1) = k + left
        
        return left + k;
    }
}
```
